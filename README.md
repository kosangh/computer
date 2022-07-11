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

![image](https://user-images.githubusercontent.com/108641430/177495652-c338d601-b0bd-43a7-b3e2-56ab35ff0fc1.png)


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

## 4. Processor Architecture (1/2)

### HW Architecture의 종류

#### Microprocessor or CPU

계산만 해줌 (CPU와 Memory가 독립적으로 존재)

![image](https://user-images.githubusercontent.com/108641430/177903997-6a74d45c-9e71-4357-a9c3-65cd575a8ad6.png)

#### Microcontroller or SoC (system-on-a-chip)

CPU + Memory + I/O + ... (한 칩에)

![image](https://user-images.githubusercontent.com/108641430/177904257-588dc751-a59a-4bca-9649-2e2f66831ebe.png)

### ECU HW Architecture

![image](https://user-images.githubusercontent.com/108641430/177904337-f38cae0b-d678-45d3-99fd-cff7fde11b53.png)

### Bus-based Computer Architecture

System Bus

- CPU, Memory, I/O Devices를 연결한다.
- 버스는 shared medium이다. (연결된 것들을 공통적으로 볼 수 있다.)
- Bus Bandwidth(데이터 주고 받는 속도) = Bus width X Bus clock speed (ex) 초당 32bits 표현 가능 = 32bits X 초당 1bit)
- Scoreboard와 비슷하다. (모두가 동시에 볼 수 있고, CPU clocks와 같은 이닝 단위로 동기화된다.(동기화 안하면 서로 엉킨다.))

![image](https://user-images.githubusercontent.com/108641430/177905067-d9dfe8f4-5c27-488c-915b-747fdbdb64e3.png)

(Control Bus엔 Read,write 등 operations / Address Bus엔 주소 / Data Bus엔 Data(값))

### Inside a CPU

CPU는 memory instruction 읽고 그 instruction을 실행한다.

#### PC (Program Counter)

다음 명령의 주소를 가지고 있다. (지금 실행하고 있는 instruction 주소도 가지고 있다.)

(Special-purpose regusters 중 하나)

#### ALU (Arithmetic Logic Unit)

사칙연산과 logic operations(큰가 작은가 등)를 수행한다.

연산 후 연산 결과를 만들어낸다.

#### Registers

CPU architectures가 다르면 register setseh 다르다. (register 수와 naming이 다르다.)

- General-purpose registers

momory 접근에 비해 매우 빠르다. (CPU 안에 있어서)

매우 희소하다 (한정된 수의 registers)

- Special-purpose registers

특별한 기능을 가진 몇몇 CPU registers

Controllers (CPU가 대응해서 작용)

##### Ex

- PC (Program Counter)
- SP (Stack Pointer)

![image](https://user-images.githubusercontent.com/108641430/177906021-a872c8af-d70e-4e5f-afa7-42c9d7284b4b.png)

### Program Execution

PC를 memory의 시작 instruction 위치에 놓는다.

CPU가 PC에 있는 instruction을 읽고 실행한다.

PC가 자동으로 다음 명령을 읽는다.

![image](https://user-images.githubusercontent.com/108641430/177906620-ac6ef68b-1a86-4a9a-a5b6-3003dad4a7f1.png)

### Processor Architecture

Instruction Set Architecture (ISA)

- CPU가 무엇을 이해하는지 (CPU가 어떤 machine language를 이해하는지)

Microarhitecture

- 어떻게 CPU가 design되었는지

#### Instruction Set Architecture (ISA)

HW와 SW 사이의 상호작용

- Instructions
- Registers
- Memory access mode (명령 대상에 따라 매우 다름)
- Endianness (Little-endian, Big-endian, and Bi-endian(Little, Big 둘 다 사용가능))

![image](https://user-images.githubusercontent.com/108641430/177907936-6d521f29-1c7d-4369-b974-ea4a07747183.png)

다양한 ISA들을 위한 다양한 Compilers

- 같은 C code지만 다른 instructions (어떤 compiler 쓰느냐에 따라)
- Compiler 개발자는 ISA들을 완벽하게 이해해야 한다.
- Host computers ISA가 target ISA와 같을 필요가 없다. (Cross compilation)

![image](https://user-images.githubusercontent.com/108641430/177908308-df8f3eb6-f816-47ec-bc90-f64cce15b3eb.png)

##### CISC and RISC

CISC (Complex ISA)

- X86이 전형적인 예이다.

RISC (Reduced ISA)

- ARM과 MIPS가 전형적인 예이다.
- 새로 만들어진 대부분의 CPU

(기술적으론 RISC 승)

###### CISC와 RISC 비교

![image](https://user-images.githubusercontent.com/108641430/177910237-a07d5c40-eb7d-45fd-9f83-6e065b55a88e.png)

###### Two Memory Access Models

CISC는 Register-memory architecture (memory와 registers에서 작업을 수행할 수 있다.)

RISC는 Load-store architecture (register-register architecture) (오직 registers에서만 작업을 할 수 있다.)

- 3단계 (Load ; Do ; Store)
+ memory에서 registers로 values를 Load
+ registers에서 Do an operation
+ registers에서 memory로 values를 Store

![image](https://user-images.githubusercontent.com/108641430/177910833-96524afa-c703-4fa8-a0f9-94272dbeea8f.png)

( []는 memory dereferencing을 의미한다. (pointer dereferencing처럼))

#### Microarchitecture

CPU 내부가 어떻게 생겼는가

Chip-level Design

- Cache
- Pipelining
- Out-of-order execution
- ...

(같은 언어를 써도 회사마다 다르게 만들 수 있다.)

### Computer Architecture

#### Von Neumann Architecture

![image](https://user-images.githubusercontent.com/108641430/177911019-68c9e379-fa4a-48c4-92d3-9070a81b6208.png)

John Von Neumann의 이름에서 따왔다.

instructions와 Data가 한 메모리에 있다.

instructions와 data에 동시접근이 불가능하다.

CPU와 momory사이에 Bottleneck이 생긴다.

프로그램이 편하고 단순하다.

#### Havad Architecture

![image](https://user-images.githubusercontent.com/108641430/177911230-9665e588-5d22-4462-bc18-eb0ca5b20c1e.png)

Harvard Mark I computer에서 이름을 따왔다.

instructions memory와 data memory가 따로 존재한다.

instructions와 data 동시 접근이 가능하다.

CPU와 memory 사이의 bottleneck이 적다.

bandwidth가 넓어졌다.

- 현대 processors는 통합 메모리를 쓰지만 분리된 instruction과 data cache에 의해 data path와 instructions path가 구분되어 있다. (Von Neumann과 Havard architecture의 combination)

### Program Execution Time

![image](https://user-images.githubusercontent.com/108641430/177911655-19cdf4e9-bafd-49c0-92d2-0a1739bd6d10.png)

## 5. Processor Architecture (2/2)

### Moore's Law

24개월마다 CPU안의 transistors 수가 2배가 된다. (transistors를 통해 연산, 늘어날수록 연산이 빨라진다.)

- transistor

저마늄, 규소 따위의 반도체를 이용하여 전자 신호 및 전력을 증폭하거나 스위칭하는 데 사용되는 반도체소자이다. 세 개 이상의 전극이 있다.

### From Transistors to CPU

![image](https://user-images.githubusercontent.com/108641430/178199581-02e71247-0fb7-49cd-b2f3-1a9e0f9b2b6c.png)

### Simple CPU with Single Cycle Datapath

![image](https://user-images.githubusercontent.com/108641430/178199688-611bb991-1bcb-4f7c-a291-a634599d5060.png)

### 5 Stages of Datapath

![image](https://user-images.githubusercontent.com/108641430/178199900-9a59afa7-10ca-457b-bb64-a35ea30a0c9a.png)

IF (Instruction Fetch)
- PC에서 instruction을 읽는다.
- PC += 4 (4-byte RISC instruction 가정) -> 다음 instruction 실행

ID (Instruction Decode)
- instruction을 이해한다.
- registers를 읽는다.

EX (Execute)
- operation을 수행한다.
- Arithmetic/Logical Operations

MEM (Memory Access)
- memory에서 Load하거나 memory에 저장한다.

WB (Write Back)
- 적절한 registers에 결과를 작성한다.

### Pipelining

Pipelining하면 단위시간당 할 수 있는 총량이 늘어난다. -> bandwidth가 늘어난다.

![image](https://user-images.githubusercontent.com/108641430/178200593-2d96efb8-6ada-450c-b05b-bbb69a12dc41.png)

#### Pipelined Datapath

![image](https://user-images.githubusercontent.com/108641430/178200784-17757278-06e9-4186-a641-6b7a1370860a.png)

- instruction 하나 실행시키는데 5개의 cycle(stage)
- stage당 걸리는 시간이 같지 않다. (ID가 IF보다 빠름)
- stage사이에 중간중간 저장을 위해 버퍼를 넣는다.

#### Pipeline Hazards

##### Structural Hazards

HW resouce가 겹칠 수 있다.

Havard architecture가 pipelining 면에서는 더 좋다. (MEM, IF 동시에 가능)

![image](https://user-images.githubusercontent.com/108641430/178201436-9931a47f-56f9-4553-b8d2-b01e4278fa14.png)

memory나 register file에 동시 접근이 불가능하다.

##### Data Hazards

Data 의존성

+ 원하지 않는 값의 데이터가 pipelining에 의해서 미리 들어가짐.

RAW (Read After Write), WAR, WAW

![image](https://user-images.githubusercontent.com/108641430/178201967-acc1affb-a6ce-45e2-8492-83050d1d5337.png)

##### Control Hazards

Control 불확실성

+ 다음 instruction이 뭔지 모르는 상황이 발생한다.

![image](https://user-images.githubusercontent.com/108641430/178202291-80315c3e-cce5-45e5-b100-8633fc337ece.png)

### Out-Of-Order Execution

runtime에서 insturctions의 싱행 순서를 바꾼다.

![image](https://user-images.githubusercontent.com/108641430/178202671-08fd8b21-0345-4063-8775-11303697be7a.png)

Line 2는 Line 1의 결과에 의존한다. pipelining stalls 가능성이 매우 높다. => instructions 순서를 재배치하여 pipelining stalls 가능성을 낮춘다. 원래 결과와 같은 결과를 출력한다.

### Processor Performance Metrics

#### Latency (execution time)

program 실행하고 끝나는데 걸리는 시간

program 관점이다.

낮을수록 좋다.

##### Execution Time (seconds / program)

Seconds / cycle (사이클당 몇초가 걸리는가) (ex) 1Hz CPU -> 1, 10Hz CPU -> 0.1)

- Higher CPU clock frequency (더 이상 불가능)
- Energy 소비와 열 문제
- Multicore CPU가 더 많은 CPU cycles(CPU clock cycle)을 제공할 수 있다.

Cycles / instruction

- instruction 복잡도
- CISC CPU가 instuction 복잡도가 더 크다. (RISC가 유리)

instructions / program

- RISC compiler가 주어진 program에서 더 많은 instructions를 만든다. (CISC가 유리)

![image](https://user-images.githubusercontent.com/108641430/178204174-b08e48e4-d07d-414c-a75d-af2f3be16a84.png)

#### Throughput (bandwidth)

특정 시간에 실행 시킬수 있는 programs의 수

system의 관점이다.

높을수록 좋다.

MIPS (Million Instructions Per Second)
- 초당 CPU가 얼마나 많은 instructions를 실행시킬 수 있는지
- 과거엔 중요했으나 요새는 그렇게 중요하지는 않다.

![image](https://user-images.githubusercontent.com/108641430/178204766-18c95405-248a-42d9-ad35-8fd261978ae4.png)

latency와 throughput이 꼭 같이 가진 않는다. (latency 낮아진다고 throughput이 높아지지 않는다.)

(pipelining해도 latency는 그대로이고 throughput은 좋아진다.)
