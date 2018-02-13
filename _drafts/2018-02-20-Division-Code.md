---
layout: post
title: "코드 분리"
date: 2018-02-20 12:00
categories: Program_Language
tags: C, C++
---

코드 분리

------

> 일반적으로 하나의 파일이 하나의 기능을 담당하도록 구성



### C언어 기준

#### extern

  . 변수 혹은 함수의 자료형 및 선언 위치를 알려주는데 사용됨

  . 함수의 경우 extern 선언을 생략 가능

```c
...
  extern int num;	// int형 변수 num이 외부에 선언되어 있음
  extern void Increment(void);	// void Increment(void) 함수가 외부에 정의도어 있음
  // void Increment(void); 의 형태로 생략가능함
```



#### static

  . 전역변수에 대한 static 선언은 `외부파일` 의 접근을 차단하는 역할을 함









#### 헤더파일 포함 방법

```c#
#include <header.h>		// C의 표준 헤더파일에서 해당 파일을 찾음

#include "header.h"		// 소스파일이 저장된 디렉토리에서 헤더 파일을 찾음
```

> 









### C++ 기준

> C++은 일반적으로 클래스 선언은 헤더 파일로 구현, 멤버 함수의 정의는 .cpp로 구현함

![4](https://user-images.githubusercontent.com/29933947/36130911-8cb78bec-10b2-11e8-92bf-27e56baf8c6b.png)