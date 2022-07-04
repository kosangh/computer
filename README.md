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

![image1](https://user-images.githubusercontent.com/108641430/177073992-66ea2b16-0da6-4192-a30f-9637582291ab.png)

### Bit

- 0 or 1이 들어갈 수 있는 data holder
- 컴퓨터에서 가장 작은 단위의 데이터
- 2개의 다른 상태를 표현할 수 있다.(Yes or No, On or Off, ...)

### Byte ,Word, Double Word

- Byte: 8개의 인접한 비트 sequence
 2^8=256개의 다른 상태를 표현할 수 있다.
 single charcater 저장 가능
 memory addressing의 단위

- Word: byte 2개 (16 bits)
+ 2^16개의 다른 상태를 표현할 수 있다.
+ 몇 비트 CPU냐에 따라서 processor's word size가 다르다.(32-bit CPU면 32bits)

- DWord: Word 2개 (23 bits)
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

![image2](https://user-images.githubusercontent.com/108641430/177074008-212da9dd-d281-45cb-8cf5-b61f18c04497.png)

+ memory size는 컴파일러에 따라서 다양하다.(64-bit compiler에서는 sizeof(long)이 8이고 32-bit compiler에서는 sizeof(long)이 4이다.)

### Unsigned, Signed Types Mapping

#### Unsigned Types Mapping

- 1 byte는 256개의 다른 상태를 표현할 수 있다.
- 이 8 bits를 이진수로 해석할 수 있다.

![image3](https://user-images.githubusercontent.com/108641430/177074028-a424beed-d7fe-4041-a8ed-2d4769b8e6f9.png)

#### Signed Types Mapping

1. Naive method

MSB(Most Significant Bit)를 부호(0: +, 1: -)로 해석하고 나머지는 이진수로 해석한다.
+ 0000과 1000을 해석하면 똑같이 0이어서 공간낭비가 발생한다.

2. 2의 보수법

Sign bit가 0이면 나머지는 그대로 해석하고 Sing bit가 1이면 2의 보수법을 적용한다.

![image4](https://user-images.githubusercontent.com/108641430/177074047-33b6a344-444f-472e-9345-e41ce4ebe44a.png)

### 여러 bytes에 걸친 Data Types

Data Type에 따라 차지하는 메모리 공간이 다르다.(ex) char는 1byte 차지, int는 4byte 차지 ...)

![image5](https://user-images.githubusercontent.com/108641430/177073817-63893b9d-da3c-4404-af52-c456436a7617.png)

### Byte Ordering

같은 Memory layout이 Endianness에 따라서 다르게 해석된다.

![image6](https://user-images.githubusercontent.com/108641430/177074256-5539bf47-3e28-4721-85d8-26eae4dd63b8.png)

(위의 예에서 Big-Endian은 매우 큰 수로 해석)

#### Checking Endianness

![image7](https://user-images.githubusercontent.com/108641430/177074386-da48a015-3cd8-4101-82ef-69cd323caf91.png)

- Little-Endian 출력: 01 00 00 00
- Big-Endian 출력: 00 00 00 01

### Integer Overflow and Underflow

- Overflow: Data type의 범위보다 커져서 넘어갈 때 발생한다.

![image](https://user-images.githubusercontent.com/108641430/177074613-4e7748a4-66dc-4ed6-9462-387649f3b6f2.png)

- Underflow: Data type의 범위보다 작아질 때 발생한다.

![image](https://user-images.githubusercontent.com/108641430/177074674-7c7f447f-fee3-4ea8-818e-c187e9b94512.png)

(범위 벗어나지 않게 하는게 매우 중요하다.)

### Hex Code

- 한 byte는 2개의 half byte로 쪼개질 수 있다.
- 한 half byte는 16진수(0~F)로 표현될 수 있다.

![image](https://user-images.githubusercontent.com/108641430/177075001-f7f94979-68e8-4754-9c04-18f079a83c58.png)
