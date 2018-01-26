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

#### 구조체 배열

```c
...
struct point
{
  int pos_x;
  int pos_y;
}

...
int main(void)
{
  struct point arr[4];
  struct point arr1[3] = {		// 초기화 방법
    {1,2},
    {3,4}    
  }
  ....
}
```

![_ 1](https://user-images.githubusercontent.com/29933947/35397649-58e387a4-0233-11e8-8a8c-73abbf42fd19.png)

#### 구조체 포인터

```c
...
strcut point pos = {10,20};
struct point * pptr = &pos;	// 포인터 변수 pptr이 구조체 변수 pos를 가리킴

// pptr이 가리키는 구조체 변수의 멤버에 값 저장
pptr->pos_x = 30; // (*pptr).pos_x = 30;
pptr->pos_y = 40; // (*pptr).pos_y = 40;
...
```

  . 포인터 변수를 구조체의 멤버로도 선언 가능함

```c
#include <stdio.h>

struct point
{
    int pos_x;
    int pos_y;
};

struct circle
{
    double radius;
    struct point * center;
};

int main()
{
    struct point cen = {2, 6};
    double rad = 2.5;
    
    struct circle ring = {rad, &cen}; // point형 구조체 변수 center의 주소값
    
    printf("원의 반지름은: %g \n", ring.radius);
    printf("원의 중심은: %d %d \n", ring.center->pos_x, ring.center->pos_y);
    
    return 0;
}
```

![2](https://user-images.githubusercontent.com/29933947/35399109-dec9e6d0-0236-11e8-8ac8-72214218193b.png)



### 함수의 인자로 전달되는 구조체

```c
#include <stdio.h>

typedef struct point
{
    int pos_x;
    int pos_y;
}Point;

// 구조체 변수의 call by value
void ShowPosition(Point pos)
{
    printf("< %d %d > \n", pos.pos_x, pos.pos_y );
}

Point CurrentPosition(void)
{
    Point cen;
    Printf("Input current pos: ");
    scanf("%d %d", &cen.pos_x, &cen.pos_y);
    
    return cen;
}

// 구조체 변수의 call by reference
void SymmetryPosition(Point * ptr)
{
    ptr->pos_x = (ptr->pos_x) * -1;
    ptr->pos_y = (ptr->pos_y) * -1;
}

int main()
{
    Point curPos = CurrentPosition();
    ShowPosition(CurPos);				// 구조체 복사

    SymmetryPosition(&curPos);			// curPos 구조체의 멤버변수 조작을 위한 주소 전달
    ShowPosition(curPos);				// 구조체 복사

    return 0;
}
```

![4](https://user-images.githubusercontent.com/29933947/35420036-a5848b08-027e-11e8-99bc-286442cf153e.png)

  . 구조체 변수를 대상으로 대입연산, 주소값 반환(&) 연산, 구조체 변수 크기 반환(sizeof) 연산 등이 허용

  . 사칙연산은 별도의 함수를 정의하여 수행해야함

```c
#include <stdio.h>

typedef struct point
{
    int pos_x;
    int pos_y;
}Point;

Point AddPosition(Point pos1, Point pos2)
{
    Point pos = {pos1.pos_x + pos2.pos_x, pos1.pos_y + pos2.pos_y};
    return pos;
}

int main()
{
    Point pos1 = { 1, 2 };
    Point pos2 = { 3, 4 };
    Point result;
    
    result = AddPosition(pos1, pos2);
    printf("<X: %2d Y: %2d >\n", result.pos_x, result.pos_y);
    
    return 0;
}
```

![5](https://user-images.githubusercontent.com/29933947/35420252-ccb935b0-027f-11e8-9456-a4bca417d3ad.png)

#### 구조체 중첩

  . 구조체의 멤버변수로 구조체 선언 가능

```c
#include <stdio.h>

typedef struct point
{
    int pos_x;
    int pos_y;
}Point;

typedef struct circle
{
    Point cen;
    double rad;
}Circle;

void ShowCircleInfo(Circle * cptr)
{
    printf("[ %d %d ] \n", (cptr->cen).pos_x, (cptr->cen).pos_y);
    printf("radius: %g \n\n", cptr->rad);
}

int main()
{
    Circle c1 = {{1, 2}, 2.5};
    Circle c2 = {3, 4, 5.5};
    
    ShowCircleInfo(&c1);
    ShowCircleInfo(&c2);
    
    return 0;
}
```

![6](https://user-images.githubusercontent.com/29933947/35420598-c75e7b78-0281-11e8-8864-cda11c0800a4.png)



### 공용체(union)



### 열거형(enum)

