---
layout: post
title: "C 구조체"
date: 2018-01-26 00:30
categories: Program_Language
tags: c
---

C 언어의 구조체에 대해 정리한다.

------

  . 하나 이상의 변수(정수형, 실수형, 포인터, 배열 등)을 묶어 새로운 자료형을 정의

```c
...  
struct person
{
  char name[20];
  char phonenum[20];
  int age;
};

typedef struct point
{
  int pos_x;
  int pos_y;
}Point;

...
 
int main(void)
{
  // 구조체 변수 선언 방법: struct type_name val_name;
  struct person p1;		
  
  // 초기화 방법1, 문자열, 정수형을 바로 대입할 수 있음
  struct person p2 = {"김철수", "010-1111-2222", 20};
  struct person p3;
  Point pos1;
  
  // 초기화 방법2, 배열에 문자열을 입력하기 위해 strcpy 함수를 사용함
  strcpy(p1.name, "홍길동");
  strcpy(p1.phonenum, "010-1234-5678");
  p1.age = 10;			// 구조체 변수 p1의 멤버변수 age에 20을 저장
  
  // 구조체 변수 멤버 변수 접근 방법
  printf("이름 입력:"); scanf("%s", p3.name);	    // 배열 멤버변수는 이름(=주소값) 접근
  printf("나이 입력:"); scanf("%d", &p3.age); // 정수형 멤버변수는 주소값 접근
  
  return 0;
}
```



### 구조체 배열 및 포인터



#### 



