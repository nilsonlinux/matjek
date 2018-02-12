---
layout: post
title: "C++ 특징-C언어 대비"
date: 2018-02-16 01:00
categories: Program_Language
tags: c++
---

C++와 관련하여 C언어 대비 특징을 정리한다

------

### 입출력 형태 변화

#### 출력 형태

```c++
#include <iostream.h>
// 입출력을 위한 헤더파일, C언어의 stdio.h 역할

int main(void)
{
  cout << "Hello World!" << endl;
  // 출력은 `cout << 출력 대상` 의 형태  
  // endl 은 개행 문자를 포함하고 있음
  // endl 은 출력 버퍼를 비움
  
  cout << "Hello" << "World!" << endl;
  cout << 1 << 'c' << "Hello World" << endl;
  // 출력의 대상은 정수, 실수, 문자열이 가능하고, 연속적으로 출력 대상을 지정할 수 있음
  
  return 0;
}
```



```c++
// C++ 새 기준

#include <iostream>
// .h 를 생략 가능

int main(void)
{
  std::cout << "Hello World!" << std::endl;
  // std:: 형태
  
  std::cout << "Hello" << "World!" << std::endl;
  std::cout << 1 << 'c' << "Hello World" << std::endl;  
  
  return 0;
}
```



#### 입력 형태

```c++
#include <iostream.h>

int main(void)
{
  int num1, num2;  
  
  cout << "첫 번째 숫자 입력: ";
  cin >> num1;
  // 입력은 `cin >> 입력 대상` 의 형태
  // 입력에 C언어의 scanf와 같이 형태 지정 등의 작업이 필요하지 않음
  // 연속적인 입력일 경우, 입력 대상을 연속적으로 지정해 주면 됨
  // ex) cin >> num1 >> num2 >> num3 
  //     -> num1 입력 후, num2 입력 받음, num2 입력 후, num3 입력 받음
  
  cout << "두 번째 숫자 입력: ";
  cin >> num2;
  
  int result = num1 + num2;
  cout << "덧셈 결과: " << result << endl;
  
  return 0;  
}
```



```c++
// C++ 새 기준

#include <iostream>

int main(void)
{
  int num1, num2;  
  
  std::cout << "첫 번째 숫자 입력: ";
  std::cin >> num1;
  
  std::cout << "두 번째 숫자 입력: ";
  std::cin >> num2;
  
  int result = num1 + num2;
  std::cout << "덧셈 결과: " << result << std::endl;
  
  return 0;  
}
```

![2](https://user-images.githubusercontent.com/29933947/35849209-2b3addae-0b64-11e8-90a4-8725e5c4c040.png)



```c++
#include <iostream>

int main(void)
{
    int num1=1, num2=10;
    int sum=0;
    char name[100];
    
    std::cout << "실행자 이름은?: ";
    std::cin >> name;
  	// 정수형, 실수형, 배열 등 데이터 형태에 따른 입출력 형식의 변화 없음  
  
    std::cout << "실행자: " << name << std::endl;
    
    std::cout << "첫 번째 수: " << num1 << " 두 번째 수: " << num2 << std::endl;
    
  	// 변수 선언을 임의 위치에 할 수 있음   
    for(int i=num1+1; i<num2; i++)
        sum += i;
    
    std::cout << "사이값 합: " << sum << std::endl;
    return 0;
}    
```

![3](https://user-images.githubusercontent.com/29933947/35849628-9ba44b1a-0b65-11e8-8148-eef5eadd153f.png)



### 함수 오버로딩

  . Function Overloading

  . C++ 은 함수 이름이 동일하여도, 매개 변수의 타입, 개수로 함수를 구분할 수 있음

```c++
#include <iostream>

void func(void){
    std::cout << " func(void)" << std::endl;
}

void func(char c){
    std::cout << " func(char c)" << std::endl;
}

void func(int a, int b){
    std::cout << " func(int a, int b)" << std::endl;
}

int main(void){
    func();
    func('a');
    func(10, 20);

    return 0;
}
```

![1](https://user-images.githubusercontent.com/29933947/36084457-bf19a190-1000-11e8-987b-da8e1ee1631f.png)



### 디폴트 매개 변수

  . Default 매개 변수

  . 함수 호출 시, 인자가 전달되지 않을 경우, 미리 정의된 디폴트 매개 변수의 값으로 명령을 수행

  . 함수 선언이 함수의 정의 이전에 존재할 경우, 디폴트 매개 변수는 선언 부분에 있어야 함

```c++
#include <iostream>

// 함수 선언이 main 뒤에 있을 경우, default 선언은 main 앞쪽에 필요함
int volume(int length=9, int width=8, int height= 7);

int main()
{
    std::cout << " [10, 10, 10]     :" << volume(10, 10, 10) << std::endl;
    std::cout << " [10, 10, def]    :" << volume(10, 10) << std::endl;
    std::cout << " [10, def, def]   :" << volume(10) << std::endl;    

    return 0;
}

int volume(int length, int width, int height)
{
    return length * width * height;
}
```

![2](https://user-images.githubusercontent.com/29933947/36084456-beef1470-1000-11e8-9d07-08b6d79d2b31.png)



#### 주의해야할 디폴트 매개변수 선언(함수 오버로딩)

```c++
#include <iostream>

// 함수 선언이 main 뒤에 있을 경우, default 선언은 main 앞쪽에 필요함
int func(int a = 10){
    return a;
}

int func(){
    return 20;
}

int main()
{
    std::cout << func() << std::endl;
    // 해당 호출은, func(), func(int a = 10) 모두 호출 가능함, 주의 필요
    
    return 0;
}
```

![3](https://user-images.githubusercontent.com/29933947/36084346-bf089496-0fff-11e8-899a-97fb0bd77c24.png)



### 인 라인 함수

  . `프로그램 라인 안으로 들어간 함수` , 함수 호출 문장이 함수의 몸체 부분으로 완전히 대체되는 현상 (in-line)

  .  C언어의 매크로(전처리기)와 같은 역할

  . 함수 호출 과정이 사라져, 성능 향상의 여지가 있음

  . 단, 함수의 구현이 까다롭고, 디버깅이 어려움

```c++
#include <iostream>

inline int SQUARE(int x)
{
    return x*x;
}

int main(void)
{
    std::cout << SQUARE(10) <<std::endl;
    // SQUARE는 inline 함수로서, 위의 문장은 컴파일 시
    // std std::cout << (10)*(10) <<std::endl; 로 대체되어 수행됨

    return 0;
}
```

![4](https://user-images.githubusercontent.com/29933947/36084449-acf584ca-1000-11e8-82b5-27ad95175767.png)



### 네임 스페이스(namespace)

  . namespace 공간이름{} 형태로 구성

  . 네임 스페이스 공간이 다르면 같은 이름의 변수, 함수의 선언이 허용됨

  . `::`  = 범위 지정 연산자(scope resolution operator), 지정된 네임 스페이스의 함수를 호출하기 위한 명령

```c++
#include <iostream>

namespace A_COM
{
    void func(void);
}

namespace B_COM
{
    void func(void);
}

int main(void)
{
    // A_COM 으로 지정된 네임 스페이스에 선언되어 있는 func() 함수를 호출
    A_COM::func();    
    B_COM::func();

    return 0;
}

namespace A_COM
{
    void func(void)
    {
      	// std 로 지정된 네임 스페이스에 선언되어 있는 cout, endl 를 참조
        std::cout << "A 회사에서 정의한 함수" << std::endl;
    }
}

namespace B_COM
{
    void func(void)
    {
        std::cout << "B 회사에서 정의한 함수" << std::endl;
    }
}
```

![5](https://user-images.githubusercontent.com/29933947/36084714-1e990c6c-1003-11e8-8c16-a8179c71e04e.png)



#### Using 선언

  . 반복적으로 사용할 네임 스페이스를 default로 선언하여 사용하기 위함

```c++
#include <iostream>

namespace A_COM
{
    void func(void);
}

// func 이라는 이름을 참조하는 코드에서, A_COM 네임 스페이스에 선언된 func을 참조하도록 함
using A_COM::func;

int main(void)
{
    func();
    
    return 0;
}
```

 

 . 지역변수와 동일한 이름의 전역변수를 사용의 편의를 위함

```c++
#include <iostream>

int val=10;

using std::cout;
using std::endl;

int main(void){
    int val = 1;
	
  	// 전역변수 접근
    ::val += 1;

    cout << " 지역변수 val의 값 : " << val << endl;
    cout << " 전역변수 val의 값 : " << ::val << endl;

    return 0;
}
```

![6](https://user-images.githubusercontent.com/29933947/36084886-b4e8675c-1004-11e8-822c-f76de374a17c.png)



