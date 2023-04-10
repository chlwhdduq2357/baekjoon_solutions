# Digital Forensics Assignment 1


[1] What is the valid width and height of this bitmap image file?
-------------

우선 그림 파일을 확인해본 결과 bmp 헤더를 갖고 있었다.
확장자를 bmp로 변환해주고 확인해보니 그림이 깨져있었다.

Hex editor를 이용해 파일 헤더를 살펴보고, assignment에 적힌 힌트를 통해 width 값을 변경하면 원래 사진을 복원할 수 있을 것으로 판단하였다.
그러나 정확한 width의 값을 알아내기 위해서는 header의 각 값을 자세히 살펴보아야 할것 같다는 생각이 들어, 온라인에서 쉽게 이용할 수 있는 도구를 검색해보았다.
그 결과, 다음의 사이트를 발견하였다 : https://online.officerecovery.com/

위의 사이트에 주어진 과제 파일을 업로드한 결과, 파일의 원래 가로와 세로의 크기를 알 수 있었다.

Width : 0x03F9
Hight : 0x02C7


[2] What is the key for decrypting a hidden byte stream?
-------------

사진에 주어진 16진수 값을 시간으로 변경시켜야 한다.
여러가지 시간 포맷 중에서 수업시간에 다룬 window filetime과 unix timestamp를 이용하여 시간 값을 알아낼 수 있었다.

key : 38

[3] What is the latitude and longitude stored in the hidden byte stream?
-------------

파일 내부를 hex editor로 다시 살펴본 결과, 파일 헤더 바로 아래 파일에 필요없는 문자열을 발견하였다.
이 문자열을 2번에서 구한 key값을 이용해 decoding 할 수 있을 것으로 예상하였다.
특히 저렇게 짧은 key를 사용하는 암호 알고리즘은 사실상 없으므로, 암호 알고리즘이 아닌 다른 간단한 알고리즘일 것으로 예상하였다.

그리고 38과 문자열을 XOR 연산을 통해 1차적으로 decoding한 후, 문자열의 끝부분이 '='으로 끝나는 것을 확인하고 base64 decoding해준 결과 특정한 형식의 문자열을 얻을 수 있었다.
마지막으로 TCEZP 라는 좌표를 나타내는 문자열이 존재하는지를 검색해보았는데 존재하지 않는다는 사실을 파악하였다.
그래서 마지막으로, 알파벳만 변경시킨다는 점을 이용해 ROT13을 적용시켜본 결과 NMEA 형식의 문자열을 발견할 수 있었다.

이 값을 GPRMC & GPGGA decoder에 대입하여 위도와 경도를 구할 수 있었다.


[4] What is the Korean name of the place where the coordinates point to? Represent it as UTF-8 hex-encoded bytes.
-------------

해당 좌표는 독도를 가리킨다.
eb 8f 85 eb 8f 84


