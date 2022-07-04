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

### Byte ,Word, Double Word

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

#### Integer Representation

- 10진법으로 표현
- 컴퓨터는 bits 사용해서 숫자 표현(2진법으로)
+ 예를 들어 4개의 bits는 (0~15, 1~16,...) 16가지의 경우를 표현할 수 있다.
- 주어진 integer number 범위에서 필요한 비트 수를 알 수 있고 bit sequence와 숫자의 mapping을 정의한다.

### Data Type

<p align="center">
<img width="600" src="image/image2.png">
</p>

+ memory size는 컴파일러에 따라서 다양하다.(64-bit compiler에서는 sizeof(long)이 8이고 32-bit compiler에서는 sizeof(long)이 4이다.)

### Unsigned, Signed Types Mapping

#### Unsigned Types Mapping

- 1 byte는 256개의 다른 상태를 표현할 수 있다.
- 이 8 bits를 이진수로 해석할 수 있다.

<p align="center">
<img width="600" src="image/image3.png">
</p>

#### Signed Types Mapping

1. Naive method

MSB(Most Significant Bit)를 부호(0: +, 1: -)로 해석하고 나머지는 이진수로 해석한다.
+ 0000과 1000을 해석하면 똑같이 0이어서 공간낭비가 발생한다.

2. 2의 보수법

Sign bit가 0이면 나머지는 그대로 해석하고 Sing bit가 1이면 2의 보수법을 적용한다.

<p align="center">
<img width="600" src="image/image4.png">
</p>

#### 여러 bytes에 걸친 Data Types

Data Type에 따라 차지하는 메모리 공간이 다르다.(ex) char는 1byte 차지, int는 4byte 차지 ...)

![image5](https://user-images.githubusercontent.com/108641430/177073817-63893b9d-da3c-4404-af52-c456436a7617.png)
