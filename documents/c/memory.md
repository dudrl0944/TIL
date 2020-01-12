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
Uninitialized data segment, often called the “bss” segment, named after an ancient assembler operator that stood for “block started by symbol.” Data in this segment is initialized by the kernel to arithmetic 0 before the program starts executing

uninitialized data starts at the end of the data segment and contains all global variables and static variables that are initialized to zero or do not have explicit initialization in source code.

For instance a variable declared static int i; would be contained in the BSS segment.
For instance a global variable declared int j; would be contained in the BSS segment.


## Stack
The stack area traditionally adjoined the heap area and grew the opposite direction; when the stack pointer met the heap pointer, free memory was exhausted. (With modern large address spaces and virtual memory techniques they may be placed almost anywhere, but they still typically grow opposite directions.)

The stack area contains the program stack, a LIFO structure, typically located in the higher parts of memory. On the standard PC x86 computer architecture it grows toward address zero; on some other architectures it grows the opposite direction. A “stack pointer” register tracks the top of the stack; it is adjusted each time a value is “pushed” onto the stack. The set of values pushed for one function call is termed a “stack frame”; A stack frame consists at minimum of a return address.

Stack, where automatic variables are stored, along with information that is saved each time a function is called. Each time a function is called, the address of where to return to and certain information about the caller’s environment, such as some of the machine registers, are saved on the stack. The newly called function then allocates room on the stack for its automatic and temporary variables. This is how recursive functions in C can work. Each time a recursive function calls itself, a new stack frame is used, so one set of variables doesn’t interfere with the variables from another instance of the function.


## Heap
Heap is the segment where dynamic memory allocation usually takes place.

The heap area begins at the end of the BSS segment and grows to larger addresses from there.The Heap area is managed by malloc, realloc, and free, which may use the brk and sbrk system calls to adjust its size (note that the use of brk/sbrk and a single “heap area” is not required to fulfill the contract of malloc/realloc/free; they may also be implemented using mmap to reserve potentially non-contiguous regions of virtual memory into the process’ virtual address space). The Heap area is shared by all shared libraries and dynamically loaded modules in a process.


## Stack Frame