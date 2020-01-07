# 포인터(Pointer)
[cppreference.com의 Pointer](https://en.cppreference.com/w/cpp/language/pointer) 문서와 해당 [블로그](https://easy-develop.tistory.com/36?category=866404)를 참고하여 정리하였습니다.

## In this article

- [포인터 문법(pointer syntax)](#포인터-문법pointer-syntax)
- [포인터 연산자(pointer operator)](#포인터-연산자pointer-operator)
- [맴버 접근 연산자(member access operators)](#맴버-접근-연산자member-access-operators)
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

## 맴버 접근 연산자(member access operators)
|연산자 이름(operator name)|문법(Systax)|Overloadable|Prototype examples (for `class T`) - Inside class definition|Prototype examples (for `class T`) - Outside class definition|
|---------------------------|------------|-------------|----------|-------|
|subscript|`a[b]`|Yes|`R& T::operator[] (S b);`|`N/A`|
|indirection|`*a`|Yes|`R& T::operator* ();`|`R& operator* (T a);`|
|address-of|`&a`|Yes|`R& T::operator& ();`|`R& operator& (T a);`|
|member of object|`a.b`|No|`N/A`|`N/A`|
|member of pointer|`a->b`|Yes|`R& T::operator->();`|`N/A`|
|pointer to member of object|`a.*b`|No|`N/A`|`N/A`|
|pointer to member of pointer|`a->*b`|Yes|`R& T::operator->&(S b)`|`R& operator->* (T a, S b)`|



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
a 	: 123					&a 	: -403981576
pa 	: -403981576				ppa 	: -403981584
*pa 	: 123					*ppa 	: -403981584
*pa 	: 123					**ppa 	: 123 
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
A pointer to object can be initialized with the return value of the [address-of operator](https://en.cppreference.com/w/cpp/language/operator_member_access) applied to any expression of object type, including another pointer type:

객체에 대한 포인터는 다른 포인터 유형을 포함하여 객체 유형의 모든 표현식에 적용된 주소 연산자의 반환 값으로 초기화 할 수 있습니다.


```c
int n;
int* np = &n; // pointer to int
int* const* npp = &np; // non-const pointer to const pointer to non-const int
 
int a[2];
int (*ap)[2] = &a; // pointer to array of int
 
struct S { int n; };
S s = {1};
int* sp = &s.n; // pointer to the int that is a member of s
```

Pointers may appear as operands to the built-in indirection operator (unary operator*), which returns the [lvalue expression](https://en.cppreference.com/w/cpp/language/value_category) identifying the pointed-to object:


포인터는 내장된 indirection연산자(단항 연산자 *)에 대한 피연산자로 나타날 수 있습니다. 이 연산자는 지정된 객체를 식별하는 lvalue 식을 반환합니다.


```c
int n;
int* p = &n;     // pointer to n
int& r = *p;     // reference is bound to the lvalue expression that identifies n
r = 7;           // stores the int 7 in n
std::cout << *p; // lvalue-to-rvalue implicit conversion reads the value from n
```


Pointers to class objects may also appear as the left-hand operands of the member access operators operator-> and operator->*.

Because of the array-to-pointer implicit conversion, pointer to the first element of an array can be initialized with an expression of array type:

클래스 객체에 대한 포인터는 멤버 액세스 연산자 operator-> 및 operator-> *의 왼쪽 피연산자로 나타날 수도 있습니다.

배열에서 포인터로의 암시 적 변환으로 인해 배열의 첫 번째 요소에 대한 포인터는 배열 유형의 표현식으로 초기화 될 수 있습니다.


```c
int a[2];
int* p1 = a; // pointer to the first element a[0] (an int) of the array a
 
int b[6][3][8];
int (*p2)[3][8] = b; // pointer to the first element b[0] of the array b,
                     // which is an array of 3 arrays of 8 ints
                     
```

Because of the derived-to-base implicit conversion for pointers, pointer to a base class can be initialized with the address of a derived class:

포인터에 대한 파생 된 기본 암시 적 변환으로 인해 파생 클래스의 주소를 사용하여 기본 클래스에 대한 포인터를 초기화 할 수 있습니다.


```c
struct Base {};
struct Derived : Base {};
 
Derived d;
Base* p = &d;
```


If Derived is polymorphic, such pointer may be used to make virtual function calls.
Certain addition, subtraction, increment, and decrement operators are defined for pointers to elements of arrays: such pointers satisfy the LegacyRandomAccessIterator requirements and allow the C++ library algorithms to work with raw arrays.

Comparison operators are defined for pointers to objects in some situations: two pointers that represent the same address compare equal, two null pointer values compare equal, pointers to elements of the same array compare the same as the array indexes of those elements, and pointers to non-static data members with the same member access compare in order of declaration of those members.

Many implementations also provide strict total ordering of pointers of random origin, e.g. if they are implemented as addresses within continuous virtual address space. Those implementations that do not (e.g. where not all bits of the pointer are part of a memory address and have to be ignored for comparison, or an additional calculation is required or otherwise pointer and integer is not a 1 to 1 relationship), provide a specialization of std::less for pointers that has that guarantee. This makes it possible to use all pointers of random origin as keys in standard associative containers such as std::set or std::map.

Derived가 다형성 인 경우 이러한 포인터를 사용하여 가상 함수를 호출 할 수 있습니다.
특정 덧셈, 뺄셈, 증분 및 감소 연산자는 배열 요소에 대한 포인터에 대해 정의됩니다. 이러한 포인터는 LegacyRandomAccessIterator 요구 사항을 충족하고 C ++ 라이브러리 알고리즘이 원시 배열과 함께 작동 할 수 있도록합니다.


비교 연산자는 일부 상황에서 객체에 대한 포인터에 대해 정의됩니다. 동일한 주소를 나타내는 두 개의 포인터가 같고, 두 개의 널 포인터 값이 같고, 동일한 배열의 요소에 대한 포인터가 해당 요소의 배열 색인과 동일합니다. 동일한 멤버 액세스 권한을 가진 비 정적 데이터 멤버는 해당 멤버의 선언 순서를 비교합니다.

많은 구현은 또한 임의의 원점 포인터의 엄격한 총 정렬을 제공합니다. 연속 가상 주소 공간 내에서 주소로 구현 된 경우 (예를 들어, 포인터의 모든 비트가 메모리 주소의 일부가 아니며 비교를 위해 무시되거나, 추가 계산이 필요하거나 그렇지 않으면 포인터와 정수가 1 : 1 관계가 아닌 경우) 구현 std :: less의 전문화는 그 보증이있는 포인터에 적합합니다. 이를 통해 표준 원점 컨테이너 (예 : std :: set 또는 std :: map)에서 임의 원점의 모든 포인터를 키로 사용할 수 있습니다.
`To Do`

## void형 포인터(pointer to void)
Pointer to object of any type can be implicitly converted to pointer to void (optionally cv-qualified); the pointer value is unchanged. The reverse conversion, which requires static_cast or explicit cast, yields the original pointer value:

임의의 유형의 객체에 대한 포인터는 암시 적으로 void에 대한 포인터로 변환 될 수 있습니다 (선택적으로 cv 규정). 포인터 값은 변경되지 않습니다. static_cast 또는 명시 적 캐스트가 필요한 역변환은 원래 포인터 값을 생성합니다.

```c
int n = 1;
int* p1 = &n;
void* pv = p1;
int* p2 = static_cast<int*>(pv);
std::cout << *p2 << '\n'; // prints 1
```

If the original pointer is pointing to a base class subobject within an object of some polymorphic type, dynamic_cast may be used to obtain a void* that is pointing at the complete object of the most derived type.


원래 포인터가 다형성 유형의 객체 내에서 기본 클래스 하위 객체를 가리키는 경우, dynamic_cast를 사용하여 가장 파생 된 유형의 전체 객체를 가리키는 void *를 얻을 수 있습니다.

Pointers to void are used to pass objects of unknown type, which is common in C interfaces: std::malloc returns void*, std::qsort expects a user-provided callback that accepts two const void* arguments. pthread_create expects a user-provided callback that accepts and returns void*. In all cases, it is the caller's responsibility to cast the pointer to the correct type before use.


void에 대한 포인터는 C 인터페이스에서 일반적으로 알 수없는 유형의 객체를 전달하는 데 사용됩니다. std :: malloc은 void *를 반환하고 std :: qsort는 두 개의 const void * 인수를 허용하는 사용자 제공 콜백을 기대합니다. pthread_create는 void *를 받아서 리턴하는 사용자 제공 콜백을 예상합니다. 모든 경우에, 사용하기 전에 포인터를 올바른 유형으로 캐스트하는 것은 호출자의 책임입니다.

## 함수에 대한 포인터(pointer to functions)
A pointer to function can be initialized with an address of a non-member function or a static member function. Because of the function-to-pointer implicit conversion, the address-of operator is optional:

```c
void f(int);
void (*p1)(int) = &f;
void (*p2)(int) = f; // same as &f
```

Unlike functions or references to functions, pointers to functions are objects and thus can be stored in arrays, copied, assigned, etc.

A pointer to function can be used as the left-hand operand of the function call operator, this invokes the pointed-to function:


```c
int f(int n)
{
    std::cout << n << '\n';
    return n * n;
}
 
int main()
{
    int (*p)(int) = f;
    int x = p(7);
}
```

Dereferencing a function pointer yields the lvalue identifying the pointed-to function:

```c
int f();
int (*p)() = f;  // pointer p is pointing to f
int (&r)() = *p; // the lvalue that identifies f is bound to a reference
r();             // function f invoked through lvalue reference
(*p)();          // function f invoked through the function lvalue
p();             // function f invoked directly through the pointer
```

A pointer to function may be initialized from an overload set which may include functions, function template specializations, and function templates, if only one overload matches the type of the pointer (see address of an overloaded function for more detail):

```c
template<typename T> T f(T n) { return n; }
double f(double n) { return n; }
 
int main()
{
    int (*p)(int) = f; // instantiates and selects f<int>
}
```

Equality comparison operators are defined for pointers to functions (they compare equal if pointing to the same function).

## 데이터 멤버에 대한 포인터(pointer to data members)
A pointer to non-static member object m which is a member of class C can be initialized with the expression &C::m exactly. Expressions such as &(C::m) or &m inside C's member function do not form pointers to members.

Such pointer may be used as the right-hand operand of the pointer-to-member access operators operator.* and operator->*:



```c
struct C { int m; };
 
int main()
{
    int C::* p = &C::m;          // pointer to data member m of class C
    C c = {7};
    std::cout << c.*p << '\n';   // prints 7
    C* cp = &c;
    cp->m = 10;
    std::cout << cp->*p << '\n'; // prints 10
}
```

Pointer to data member of an accessible unambiguous non-virtual base class can be implicitly converted to pointer to the same data member of a derived class:

```c
struct Base { int m; };
struct Derived : Base {};
 
int main()
{
    int Base::* bp = &Base::m;
    int Derived::* dp = bp;
    Derived d;
    d.m = 1;
    std::cout << d.*dp << ' ' << d.*bp << '\n'; // prints 1 1
}
```
Conversion in the opposite direction, from a pointer to data member of a derived class to a pointer to data member of an unambiguous non-virtual base class, is allowed with static_cast and explicit cast, even if the base class does not have that member (but the most-derived class does, when the pointer is used for access):

```c
struct Base {};
struct Derived : Base { int m; };
 
int main()
{
    int Derived::* dp = &Derived::m;
    int Base::* bp = static_cast<int Base::*>(dp);
 
    Derived d;
    d.m = 7;
    std::cout << d.*bp << '\n'; // okay: prints 7
 
    Base b;
    std::cout << b.*bp << '\n'; // undefined behavior
}
```

The pointed-to type of a pointer-to-member may be a pointer-to-member itself: pointers to members can be multilevel, and can be cv-qualifed differently at every level. Mixed multi-level combinations of pointers and pointers-to-members are also allowed:


```c
struct A
{
    int m;
    // const pointer to non-const member
    int A::* const p;
};
 
int main()
{
    // non-const pointer to data member which is a const pointer to non-const member
    int A::* const A::* p1 = &A::p;
 
    const A a = {1, &A::m};
    std::cout << a.*(a.*p1) << '\n'; // prints 1
 
    // regular non-const pointer to a const pointer-to-member
    int A::* const* p2 = &a.p;
    std::cout << a.**p2 << '\n'; // prints 1
}
```



## 멤버 함수에 대한 포인터(pointer to member functions)
A pointer to non-static member function f which is a member of class C can be initialized with the expression &C::f exactly. Expressions such as &(C::f) or &f inside C's member function do not form pointers to member functions.

Such pointer may be used as the right-hand operand of the pointer-to-member access operators operator.* and operator->*. The resulting expression can be used only as the left-hand operand of a function-call operator:

```c
struct C
{
    void f(int n) { std::cout << n << '\n'; }
};
 
int main()
{
    void (C::* p)(int) = &C::f; // pointer to member function f of class C
    C c;
    (c.*p)(1);                  // prints 1
    C* cp = &c;
    (cp->*p)(2);                // prints 2
}
```

Pointer to member function of a base class can be implicitly converted to pointer to the same member function of a derived class:

```c
struct Base
{
    void f(int n) { std::cout << n << '\n'; }
};
struct Derived : Base {};
 
int main()
{
    void (Base::* bp)(int) = &Base::f;
    void (Derived::* dp)(int) = bp;
    Derived d;
    (d.*dp)(1);
    (d.*bp)(2);
}
```
Conversion in the opposite direction, from a pointer to member function of a derived class to a pointer to member function of an unambiguous non-virtual base class, is allowed with static_cast and explicit cast, even if the base class does not have that member function (but the most-derived class does, when the pointer is used for access):


```c
struct Base {};
struct Derived : Base
{
    void f(int n) { std::cout << n << '\n'; }
};
 
int main()
{
    void (Derived::* dp)(int) = &Derived::f;
    void (Base::* bp)(int) = static_cast<void (Base::*)(int)>(dp);
 
    Derived d;
    (d.*bp)(1); // okay: prints 1
 
    Base b;
    (b.*bp)(2); // undefined behavior
}
```
Pointers to member functions may be used as callbacks or as function objects, often after applying std::mem_fn or std::bind:

```c
#include <iostream>
#include <string>
#include <algorithm>
#include <functional>
 
int main()
{
    std::vector<std::string> v = {"a", "ab", "abc"};
    std::vector<std::size_t> l;
    transform(v.begin(), v.end(), std::back_inserter(l),
              std::mem_fn(&std::string::size));
    for(std::size_t n : l)
        std::cout << n << ' ';
}
```

output:

```
1 2 3
```

## 널 포인트(null pointer)
Pointers of every type have a special value known as null pointer value of that type. A pointer whose value is null does not point to an object or a function (dereferencing a null pointer is undefined behavior), and compares equal to all pointers of the same type whose value is also null.


모든 유형의 포인터에는 해당 유형의 널 포인터 값으로 알려진 특수 값이 있습니다. 값이 null 인 포인터는 객체 또는 함수를 가리 키지 않으며 (널 포인터를 정의하는 것은 정의되지 않은 동작 임) 값이 null 인 동일한 유형의 모든 포인터와 동일합니다.

To initialize a pointer to null or to assign the null value to an existing pointer, the null pointer literal nullptr, the null pointer constant NULL, or the implicit conversion from the integer value ​0​ may be used.


널 (null)에 대한 포인터를 초기화하거나 기존 포인터에 널 (NULL) 값을 지정하기 위해 널 포인터 리터럴 nullptr, 널 포인터 상수 NULL 또는 정수 값 0에서 내재 된 변환을 사용할 수 있습니다.

Zero- and value-initialization also initialize pointers to their null values.


제로 및 값 초기화는 또한 널값에 대한 포인터를 초기화합니다.

Null pointers can be used to indicate the absence of an object (e.g. function::target()), or as other error condition indicators (e.g. dynamic_cast). In general, a function that receives a pointer argument almost always needs to check if the value is null and handle that case differently (for example, the delete expression does nothing when a null pointer is passed).

널 포인터는 객체가 없음을 나타내는 데 (예 : function :: target ()) 또는 다른 오류 조건 표시기 (예 : dynamic_cast)로 사용할 수 있습니다. 일반적으로 포인터 인수를받는 함수는 거의 항상 값이 null인지 확인하고 해당 경우를 다르게 처리해야합니다 (예를 들어, delete 식은 null 포인터가 전달 될 때 아무 작업도 수행하지 않습니다).



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




