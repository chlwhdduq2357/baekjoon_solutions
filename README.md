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


[3] What is the latitude and longitude stored in the hidden byte stream?
-------------

[4] What is the Korean name of the place where the coordinates point to?
Represent it as UTF-8 hex-encoded bytes.
-------------
