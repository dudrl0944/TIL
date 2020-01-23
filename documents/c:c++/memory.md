# 메모리(Memory)

## in this article
* 메모리 구조
* 코드 영역
* 데이터 영역
* 스택 영역
* 힙 영역
* 스택 프레임
* [root](https://github.com/dudrl0944/TIL/blob/master/README.md)


## 메모리 구조
![image](https://github.com/dudrl0944/TIL/blob/master/documents/img/documents/c/memory_1.Layout_in_C.jpg) 

## 코드 영역 - Code(Text) Segment
object file과 실행가능한 명령어(executable instructions)를 포함하고 있다.

코드 영역은 보통 Stack과 Heap영역에서 발생하는 오버플로우로부터 overwriting되는 것을 막기 위해 밑에 위치한다.

일반적으로 텍스트 세그먼트는 텍스트 편집기, C 컴파일러, 셸 등과 같이 자주 실행되는 프로그램을 위해 하나의 복사본만 메모리에 있으면 되도록 공유 가능하다.

또한 텍스트 세그먼트는 프로그램이 실수로 지침을 수정하는 것을 방지하기 위해 읽기 전용인 경우가 많다.


## 초기화된 데이터 영역 - Initialized data segment
초기화된 데이터 세그먼트는 보통 데이터 세그먼트라 불린다.
데이터 세그먼트는 가상 주소 공간의 일부로서, 프로그래머에 의해 초기화된 전역번수와 정적변수를 포함한다.

참고로, 데이터 세그먼트는 런타임시간에 변수의 값을 변경할 수 있으므로, read-only가 아니다

이 세그먼트는 초기화된 읽기 전용 영역과 초기화된 읽기-쓰기 영역으로 더 분류될 수 있다.
This segment can be further classified into initialized read-only area and initialized read-write area.
예를 들어 C언어에서 char s[] = "hello world"로 정의된 글로벌 문자열과 메인(즉, 글로벌) 외부의 int debug=1과 같은 C언어 문장은 초기화된 읽기-쓰기 영역에 저장될 것이다.
그리고 cirr char* string과 같은 글로벌 C 문장은 문자열 "hello world"를 초기화된 읽기 전용 영역에 저장하고 문자 포인터 변수 문자열을 초기화된 읽기-쓰기 영역에 저장한다.

Ex: static int i = 10이 데이터 세그먼트에 저장되고 전역 int i = 10도 데이터 세그먼트에 저장됨
For instance the global string defined by char s[] = “hello world” in C and a C statement like int debug=1 outside the main (i.e. global) would be stored in initialized read-write area. And a global C statement like const char* string = “hello world” makes the string literal “hello world” to be stored in initialized read-only area and the character pointer variable string in initialized read-write area.

Ex: static int i = 10 will be stored in data segment and global int i = 10 will also be stored in data segment

## Uninitialized data segment
종종 `bss 세그먼트`라고 불리는 초기화 되지 않은 데이터 세그먼트는  `block started by symbol`이라는 초기 어셈블리어 연산자의 이름을 따서 명명되었다. 프로그램이 실행되지 전에 커널에 의해 이 세그먼트의 데이터가 0으로 초기화 된다.

초기화 되지 않은 데이터는 데이터 세그먼트의 끝에서 시작되며, 0으로 초기화 되어있거나 소스 코드에 명시적인 초기화가 없는 모든 글로벌 변수와 정적 변수를 포함한다.

예를 들어 `static int i;`으로 선언된 변수`i`는 BBS 세그먼트에 포함되고, 
글로벌 변수로 선언 된 `int j`또 BBS 세그먼트에 포함된다.


## Stack
스택 영역은 전통적으로 힙 영역과 인접하고 힙 영역과 반대 방향으로 메모리가 쌓인다. 스택 포인터와 힙 포인터가 만났을 때, 사용가능한 메모리가 모두 소진된 것이다.(현대적인 큰 주소 공간과 가상 메모리 기술을 통해 거의 모든 곳에 배치 될 수 있지만, 일반적으로 반대방향으로 성장한다.)

스택 영역은 LIFO구조로 프로그램의 스택을 포함하며, 일반적으로 메모리의 상단에 위치되어 딘다.
스택 영역은 일반적으로 메모리의 상위 부분에 위치하는 LIFO 구조인 프로그램 스택을 포함한다.
The stack area contains the program stack, a LIFO structure, typically located in the higher parts of memory.
이부분에 대한 문장구조를 잘 모르겠다. 나중에 다시 해석 해볼것.

with N and N  ( N 를 통해., 전치사구)
typically - 일반적으로
be placed ~어디에 위치되어 지다.(배치 된다.)


The stack area traditionally adjoined the heap area and grew the opposite direction; when the stack pointer met the heap pointer, free memory was exhausted. (With modern large address spaces and virtual memory techniques they may be placed almost anywhere, but they still typically grow opposite directions.)

The stack area contains the program stack, a LIFO structure, typically located in the higher parts of memory. On the standard PC x86 computer architecture it grows toward address zero; on some other architectures it grows the opposite direction. A “stack pointer” register tracks the top of the stack; it is adjusted each time a value is “pushed” onto the stack. The set of values pushed for one function call is termed a “stack frame”; A stack frame consists at minimum of a return address.

Stack, where automatic variables are stored, along with information that is saved each time a function is called. Each time a function is called, the address of where to return to and certain information about the caller’s environment, such as some of the machine registers, are saved on the stack. The newly called function then allocates room on the stack for its automatic and temporary variables. This is how recursive functions in C can work. Each time a recursive function calls itself, a new stack frame is used, so one set of variables doesn’t interfere with the variables from another instance of the function.


## Heap
Heap is the segment where dynamic memory allocation usually takes place.

The heap area begins at the end of the BSS segment and grows to larger addresses from there.The Heap area is managed by malloc, realloc, and free, which may use the brk and sbrk system calls to adjust its size (note that the use of brk/sbrk and a single “heap area” is not required to fulfill the contract of malloc/realloc/free; they may also be implemented using mmap to reserve potentially non-contiguous regions of virtual memory into the process’ virtual address space). The Heap area is shared by all shared libraries and dynamically loaded modules in a process.


## Stack Frame