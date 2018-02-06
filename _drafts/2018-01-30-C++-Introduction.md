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

  