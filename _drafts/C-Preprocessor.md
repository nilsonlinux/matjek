---
layout: post
title: "C언어 전처리문(Preprocessor)"
categories: Program-Language
tags: C
---

C언어 전처리문 관련한 정보를 기술한다.

------

## 정의

프로그램이 컴파일 되기 전 미리 실행되는 코드로 선행처리문 이라고도 지칭함

주로 코드의 일부를 활성화/비활성화 하는데 사용됨

```mermaid
graph LR
  A[Source file] --> |Preprocessor| B[Preprocessed file]
  B --> |Compiler| C[Object file<br/> ...01010001...]
  C --> |Linker| D[Executable file]
```

## 종류

#### 파일포함

 . 프로그램에 특정 파일을 첨부하여 하나의 파일처럼 컴파일하며 첨부된 파일의 함수나 변수를 사용 가능

  `#include<stdio.h>`



#### 형태정의

 . 

#### 조건부 컴파일

 . #if, #ifdef, #ifndef, #else, #elif, #endif 등

 . 컴파일 조건에 따라 컴파일 여부가 결정되도록 함