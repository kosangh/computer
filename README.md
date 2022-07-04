# 컴퓨터구조 및 실시간운영체제

##Contents
1. Data Representation (1/2)
2. Data Representation (2/2)
3. Building and Loading Programs
4. Processor Architecture (1/2)
5. Processor Architecture (2/2)
6. Memory Subsystem (1/2)
7. Memory Subsystem (2/2)

## 1. Data Representation (1/2)

컴퓨터 시스템에는 다양한 데이터 종류가 있다. (정수, 실수, 이미지 등등)

<p align="center">
<img width="400" src="사진/image1.png">
</p>

### Bit

- 0 or 1이 들어갈 수 있는 data holder
- 컴퓨터에서 가장 작은 단위의 데이터
- 2개의 다른 상태를 표현할 수 있다.(Yes or No, On or Off, ...)

###Byte ,Word, Double Word

- Byte: 8개의 인접한 비트 sequence
+ 2^8=256개의 다른 상태를 표현할 수 있다.
+ single charcater 저장 가능
+ memory addressing의 단위

- Word: byte 2개 (16 bits)
+ 2^16개의 다른 상태를 표현할 수 있다.
+ 몇 비트 CPU냐에 따라서 processor's word size가 다르다.(32-bit CPU면 32bits)

-DWord: Word 2개 (23 bits)
+ 2^32개의 다른 상태를 표현할 수 있다.

### Integers

소수점 없는 숫자들
4byte로 표현가능
+ 특정 범위에서 integer 숫자는 유한하다.(ex) -2.1에서 2.1 사이에는 5개의 integer만 존재)
