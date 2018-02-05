---
layout: post
title: "C++ 특징-C언어 대비"
date: 2018-02-16 01:00
categories: Program_Language
tags: c++
---

C++와 관련하여 C언어 대비 특징을 정리한다

------

 

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

