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

#### Byte: 8개의 인접한 비트 sequence
- 2^8=256개의 다른 상태를 표현할 수 있다.
- single charcater 저장 가능
- memory addressing의 단위

#### Word: byte 2개 (16 bits)
+ 2^16개의 다른 상태를 표현할 수 있다.
+ 몇 비트 CPU냐에 따라서 processor's word size가 다르다.(32-bit CPU면 32bits)

#### DWord: Word 2개 (23 bits)
+ 2^32개의 다른 상태를 표현할 수 있다.

### Integers

- 소수점 없는 숫자들
- 4byte로 표현가능
- 특정 범위에서 integer 숫자는 유한하다.(ex) -2.1에서 2.1 사이에는 5개의 integer만 존재)

#### Integer Representation

- 10진법으로 표현
- 컴퓨터는 bits 사용해서 숫자 표현(2진법으로)

(예를 들어 4개의 bits는 (0 ~ 15, 1 ~ 16,...) 16가지의 경우를 표현할 수 있다.)
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

(0000과 1000을 해석하면 똑같이 0이어서 공간낭비가 발생한다.)

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

## 2. Data Representation (2/2)

### Real Numbers(실수)

연속된 실직선 위의 점들이다.

![image](https://user-images.githubusercontent.com/108641430/177454072-1b09143f-ee66-4086-9791-1ed8455111fa.png)

어느 짧은 범위이든 무한한 숫자의 실수가 존재한다.
- n개의 bits로는 2^n개의 정확한 숫자들만 표현할 수 있다.
- 한정된 bits로 모든 실수를 표현할 수 없다.
- 컴퓨터에서 유한한 숫자의 실수들만 표현될 수 있다.
- 예를 들어, 코드에 0.001을 넣으면 그것의 근사값이 대신 저장된다.

![image](https://user-images.githubusercontent.com/108641430/177454407-1d3b56bb-6e4e-4fcd-b12b-92b62b222791.png)

#### Floating-Point Numbers의 부정확성

Floating-Point Numbers: 컴퓨터 시스템에서 근사화된 실수들

- 정확한 예측이 항상 가능하지 않다.

![image](https://user-images.githubusercontent.com/108641430/177454756-ddb158d0-da84-4bef-9c4f-20648913afd6.png)

- Equality check는 동작하지 않는다.

![image](https://user-images.githubusercontent.com/108641430/177454854-46dda3ee-036c-48a8-8328-cecba2283c41.png)

(부등호 check는 사용가능하지만 아주 근처의 값은 사용할지 고민해봐야 한다.)

#### IEEE 754 Standard for Floating-Point Numbers

크기가 다른 데이터 유형을 정의한다. (float: 32 bits, double: 64 bits)
+ unsigned data types가 없다.
+ 컴파일러가 바뀌어도 길이가 변하지 않는다.

32-bit float data type의 Memory layout

![image](https://user-images.githubusercontent.com/108641430/177455547-6863f29b-64a3-46d2-9839-d4973f0bcfe5.png)

##### 십진수 5.625를 Float Type으로 변환

5.626(십진수) = 101.101(2진수)

![image](https://user-images.githubusercontent.com/108641430/177455730-3b766cd8-5997-4771-bdcf-874dbf76fe03.png)

#### Floating Point Data Types

C data types

![image](https://user-images.githubusercontent.com/108641430/177455947-afac849d-5172-4670-8f4f-ab8d336a9ca4.png)

Floating-point literals
- Single precision (ex) 0.001f)
- Double precision (ex) 0.001) (Default precision)
- Quadruple precision (ex) 0.001l)

### Characters

컴퓨터는 숫자들만 표현할 수 있다.

그러므로 Characters를 컴퓨터에 가르치는 방법은 글자 하나당 특정한 숫자를 하나씩 일대일대응시킨다.

#### ASCII (American Standard Code for Information Interchange) Code

128개의 characters와 7-bits unsigned integers (0 ~ 127)을 Mapping시킨다.

![image](https://user-images.githubusercontent.com/108641430/177456662-27418e6b-f4f8-43d9-845b-cb2b1026a38d.png)

![image](https://user-images.githubusercontent.com/108641430/177456794-2293cf3a-63d0-4b46-90ad-2c312dc45e35.png)

8-bit char integer type이 ASCII Code 저장을 위해 흔하게 사용된다.
char type은 -128 ~ 127을 표현할 수 있는데 이는 ASCII를 표현하기 위해 충분하다. (오히려 MSB 1비트는 사용하지 않는다.)

### String

ASCII code 0인 NULL character ('\0')으로 끝나는 sequence of characters

![image](https://user-images.githubusercontent.com/108641430/177457386-93525b86-1c54-4e85-b4dd-1d21401556d8.png)

#### String Literal

- sequence of characters는 쌍따옴표 안에 넣는다. (ex) "I am a string")

- Compilers는 (characters의 숫자 +1('\0')) bytes를 할당한다.

- string은 그것의 stating address를 의미한다.

##### Unicode

ASCII는 한글이나 한자 같은 ASCII characters 이외의 characters를 저장하기 위해 UNICODE로 확장됐다.

![image](https://user-images.githubusercontent.com/108641430/177458340-1d43b686-278f-4b8f-bc29-676bf57e1fb1.png)

한 바이트가 UNICODE characters를 저장하기 충분하지 않기 때문에 wchar_t 같은 multibyte character types가 필요하다.

### Multimedia Data (음성, 영상, 이미지, ...)

#### A raster image data

이미지 해상도 (x, y)의 색상 코드로 표현되는 sequence of pixels

![image](https://user-images.githubusercontent.com/108641430/177458760-332c8d19-d88d-487d-9536-87fa316953d1.png)

##### Color Depth

각 pixel에 bits 숫자를 할당한다.

더 높은 color depth는 더 현실적인 이미지를 표현가능하게 한다. (file size도 커지고 memory도 더 많이 차지한다.)

![image](https://user-images.githubusercontent.com/108641430/177459027-bafb0f8c-6ca3-437a-b285-d6245edc5100.png)

#### Bitmap File (BMP)

각 픽셀마다 24 bits
8 bits for B / 8 bits for G / 8 bits for R

![image](https://user-images.githubusercontent.com/108641430/177459180-30914886-63b9-4cfe-afb2-c80e407a417d.png)
![image](https://user-images.githubusercontent.com/108641430/177459202-6a642a81-21f7-4c98-8ec1-419c3ef9cefc.png)


## 3. Building and Loading Programs

### Compiler

한 프로그래밍 언어로 쓰여진 컴퓨터 코드를 다른 언어로 번역하는 컴퓨터 프로그램이다. (ex) Python to C compiler)

프로그램을 빌드할 때 사용한다.

C compiler는 C code를 machine code로 번역한다.

![image](https://user-images.githubusercontent.com/108641430/177483920-9f5748c7-c249-4b71-884d-70a2e25ba5d4.png)

가장 유명한 C compilers
+ GNU C Compiler (현재는, GNU Compiler Collection)
+ Clang (based on LLVM(Low Level Virtual Machine))

### Three Steps of Build Process

![image](https://user-images.githubusercontent.com/108641430/177484362-7e222b1b-fc73-4641-8ad7-14d396c34301.png)

.C는 코드 / .H는 헤더 파일

#### Preprocessing(전처리)

- 주석 삭제
- 헤더 파일을 include
- 매크로를 풀어서 써줌
- 조건부 컴파일
- Line Control

![image](https://user-images.githubusercontent.com/108641430/177486331-ef7667c2-82c4-4d1f-822e-346ab0d3a617.png)

전처리된 C 파일들은 컴파일 이후 사라진다.

#### Compiling

전처리된 C 파일들은 object 파일들로 번역한다.

##### Object file

- CPU-dependent machine languages로 쓰여진다. (intel은 Arm에서 쓰지 못한다.)

- 다른 CPU architectures에서 portable하지 않다. (CPU가 달라지면 다시 해야 한다.)

- instructions와 data를 둘 다 가지고 있다.

Compiler 최적화 options

- 빠른 코드 vs 빠른 컴파일 vs 작은 object files vs ...

#### Linking

Object files(CRT와 libc 포함)를 하나의 executable file로 합친다.

+ 각 object file은 다른 object files에 calls와 접근을 가진다.

+ 그들 사이의 link가 반드시 만들어져야 한다.

CRT는 main function을 부르는 초기화 코드를 가지고 있다.

Standard C library(libc)는 (printf, scanf, ...)용 object files의 set이다.

![image](https://user-images.githubusercontent.com/108641430/177488281-d5e7b378-9567-4916-8374-ddb307289cd8.png)

#### Executable File

여러 object files에서 link된 instructions와 data

실행될 때, CRT안의 entry function이 OS에 의해 불려진다.

다른 OS들마다 다른 file formats가 있다.

+ ELF for Linux

+ PE COFF for MS Windows

![image](https://user-images.githubusercontent.com/108641430/177489118-e0d60740-a2cd-46d4-ad6f-5e33daaecc3c.png)

### Program Loading

text와 data segments를 file에서 memory로 복사한다.

초기화되지 않은 global variables를 위해 할당하고 0으로 설정한다.

dynamic memory를 위해 heap을 준비한다.

local variables와 function calls를 위해 stack을 준비한다.

![image](https://user-images.githubusercontent.com/108641430/177490111-91c9e177-dbfd-4763-9dd6-c6da44d6d1c7.png)

#### Progam in Memory

변수들과 함수들이 address space에서 그들 자신의 위치들을 가진다.

#### Text Area

Text area는 프로그램의 instructions를 저장한다. (function, loop, 코드에 박혀있는 숫자들)

![image](https://user-images.githubusercontent.com/108641430/177491011-c8439a59-19f1-4eb1-856d-92bf09646139.png)

#### Data Area

Data area는 초기화된 global variables를 저장한다.

#### BSS Area

BSS area는 초기화되지 않은(초기값이 없는) global variables를 저장한다. 

자동으로 0으로 초기화한다. (모든 비트를 0으로 밀어버린다.)

(executable file엔 없지만 로딩하면서 memory 영역에 들어간다.)

#### Heap Area

Heap area는 역동적으로 자라는 dynamic memory를 저장한다.

malloc() 함수의 memory manager에 의해 관리된다.

memory를 추가적으로 할당 가능하다. 남아있는 힙 공간이 없으면 올라가서 공간을 더 차지한다. (최대 메모리 넘어가면 올라가기만 하고 내려가지는 않는다.)

Heap area를 재사용하기 위해 free를 해주어야 한다.

#### Stack Area

stack area는 local variables를 저장한다.

local variables는 function이 샐행되는 도중에만 존재한다. (미리 memory 잡아놓을 필요가 없고 호출되면 그 때 memory를 잡는다.)

(local에 static을 붙이면 function이 끝나도 남아있기 때문에 BSS에 들어간다.)

##### Stack Frame

Stack은 function이 불려질 때 늘어나고 return될 때 수축한다.

Stack은 정리되지 않는 동안 많은 functions에 의해 재사용된다. (이것이 왜 local variables가 쓰레기값을 가지는 이유이다.)

(local variable들은 Stack을 재사용해야 하기 때문에 초기화를 해줘야 한다.)

![image](https://user-images.githubusercontent.com/108641430/177493883-21def0d1-15fb-4ee1-a41a-ec941f933215.png)

##### Risks on Stack

###### Stack overflow (safety)

Stack이 너무 자라게 되면 dynamic memory area(heap area)가 stack area에 의해 overwrite될 수도 있다.

+ 딥하게 중첩된 function calls 사용은 피한다. (ex) 재귀함수)

+ 배열들 같은 큰 local variables 사용은 피한다.

###### Stack smashing (security)

return 주소를 이상하게 하는 느낌 

해커들이 buffer overflow 기술들을 사용하여 stack에 악의적인 코드를 넣고 이를 pointing하는 함수의 반환 주소를 덮어쓴다.
