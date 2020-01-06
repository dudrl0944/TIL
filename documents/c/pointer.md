# 포인터(Pointer)
[cppreference.com의 Pointer](https://en.cppreference.com/w/cpp/language/pointer) 문서와 해당 [블로그](https://easy-develop.tistory.com/36?category=866404)를 참고하여 정리하였습니다.

## In this article

- [포인터 문법(pointer syntax)](#포인터-문법pointer-syntax)
- [포인터 연산자(pointer operator)](#포인터-연산자pointer-operator)
- [다중포인터(multiple pointer)](#다중포인터multiple-pointer)
- [객체에 대한 포인터(pointer to obejct)](#객체에-대한-포인터pointer-to-obejct)
- [void형 포인터(pointer to void)](#void형-포인터pointer-to-void)
- [함수에 대한 포인터(pointer to functions)](#함수에-대한-포인터pointer-to-functions)
- [데이터 멤버에 대한 포인터(pointer to data members)](#데이터-멤버에-대한-포인터pointer-to-data-members)
- [멤버 함수에 대한 포인터(pointer to member functions)](#멤버-함수에-대한-포인터pointer-to-member-functions)
- [널 포인트(null pointer)](#널-포인트null-pointer)
- [허상 포인터(Dangling pointer)](#허상-포인터dangling-pointer)
- [상수(constness)](#상수constness)


## 포인터 문법(pointer syntax)
#### 포인터 선언
* 포인터 선언은 포인터 변수의 이름을 지정하고 변수가 가리키는 개체의 형식을 지정합니다. 포인터로 선언된 변수는 메모리 주소를 갖습니다.

| 포인터 선언|
|------------|
|`* attr(optional) cv(optional) declarator`|
|`nested-name-specifier * attr(optional) cv(optional) declarator`|

```c
#include <stdio.h>
 
int main()
{
    int I = 1;
    int M = 2;
    int SUM;
 
    int *K;        // 9
    int *F;        // 10
 
    K = &I;        // 12
    F = &M;        // 13
 
    SUM = *K + *F; // 15
 
    printf("SUM=%d", SUM);
 
    return 0;
}
```


## 포인터 연산자(pointer operator)
#### 변수 선언 할 때 * 연산자
* 변수를 생성할 때 변수명 앞에 *을 사용한다. 

` int *K;` int형 주소를 저장 할 수 있는 포인터 변수 k

#### 그외 * 연산자
* 포인터형 변수에 저장된 주소에 위치한 값에 접근하는데 사용된다.

` SUM = *K + *F; `

#### 연산자 &
* 오른쪽에 오는 피연산자의 주소값을 반환하는 연산자이다.

` K = &I;`


## 다중포인터(multiple pointer)
```c
//OS-Mac, 64Bit 운영체제
//int형이 8bit

#include <stdio.h>

int main(){
    int a = 123;
    int *pa;
    int **ppa;

    pa = &a;
    ppa = &pa;

    printf("%d\t\t %d\n", a, &a);
    printf("%d\t %d\n", pa, ppa);
    printf("%d\t\t %d\n", *pa, *ppa);
    printf("%d\t\t %d\n", *pa, **ppa);

    return 0;



}
```
```
출력
a 	: 123					&a 		: -403981576
pa 	: -403981576			ppa 	: -403981584
*pa : 123					*ppa 	: -403981584
*pa : 123					**ppa 	: 123 

-----------------------------------------------------



```
|주소|값||컴파일러|
|--------|------|-----|---|
| 0 |||
|....|||
| -403981576|123||a(int형 >123), pa(pointer형 > -403981576) |
|-403981584|-403981576||ppa|
|....||||
|fffffffff||||


##  객체에 대한 포인터(pointer to obejct)
`To Do`

## void형 포인터(pointer to void)
`To Do`


## 함수에 대한 포인터(pointer to functions)
`To Do`


## 데이터 멤버에 대한 포인터(pointer to data members)
`To Do`


## 멤버 함수에 대한 포인터(pointer to member functions)
`To Do`


## 널 포인트(null pointer)
`To Do`

## 허상 포인터(Dangling pointer)
[허상 포인터(Dangling pointer)](https://ko.wikipedia.org/wiki/%ED%97%88%EC%83%81_%ED%8F%AC%EC%9D%B8%ED%84%B0) 그리고 와일드 포인터(wild pointers)는 컴퓨터 프로그래밍에서 적절한 타입의 유효한 객체를 가리키고 있지 않는 포인터를 말한다.

허상 포인터는 객체 파괴시에 발생하는데, 즉 객체에 대한 참조가 포인터 값에 대한 수정 없이 삭제되거나 할당 해제돼서 포인터가 계속 할당 해제된 메모리를 가리킬 때이다. 시스템은 할당 해제된 메모리를 다른 프로세스에게 재할당하겠지만, 기존 프로그램이 허상 포인터를 역참조하면 메모리는 현재 전혀 다른 데이터를 갖고 있을 것이므로 예측할 수 없는 행동이 발생한다. 


## 상수(constness)
| syntax|예시|의미|
|-------|----|----|
|const T*	|`const int *p`|pointer to constant object(포인터가 가리키는 값이 상수)|
|T const*	|`int const* p`|pointer to constant object(포인터가 가리키는 값이 상수)|
|T* const	|`int* const p`|constant pointer to object(포인터값 자체가 상수)|
|const T* const	|`const int* const p`|constant pointer to constant object(포인터가 가리키는 값이 상수 그리고 포인터값 자체가 상수)|
|T const* const	| `int const* const p`|constant pointer to constant object(포인터가 가리키는 값이 상수 그리고 포인터값 자체가 상수)|

`외우는 Tip    (const 자료형 const) * 별표 전에 자료형 앞뒤로 const가 붙으면 자료형 object, value가 상수가 되고 자료형 * (const p) 자료형 * 이후 const가 붙으면 포인터 변수 자체가 상수가 된다.`


```c
#include <iostream>
using namespace std;

int main() {
	int num1 = 1;
	int num2 = 2;

	const int *p1 = &num1;
	int * const p2 = &num1;
	const int * const p3 = &num1;



	//int * const p2;
	//const int * const p3;

	cout<<"num1의 메모리주소 : "<<&num1<<endl;
    cout<<"num2의 메모리주소 : "<<&num2<<endl;

    cout<<"p1의 메모리주소 : "<<&p1<<endl;
    cout<<"p2의 메모리주소 : "<<&p2<<endl;
    cout<<"p3의 메모리주소 : "<<&p3<<endl;



	p1 = &num1;
	cout<<"p1의 메모리주소 : "<<p1<<endl;
	p1 = &num2;
	cout<<"p1의 메모리주소 : "<<p1<<endl;

	//*p1 = num2;
	//error : read-only variable is not assignable


	//p2 = &num2;
	//cannot assign to variable 'p2' with const-qualified type 'int *const'
    *p2 = num2;
    cout<<"num1 : "<<num1<<endl;


	//p3 = &num2; //에러 발생
	//*p3 = num2; //에러 발생

	return 0;

}

```




