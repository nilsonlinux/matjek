---
layout: post
title: "C++ 연산자 오버로딩"
date: 2018-02-21 12:00
categories: Program_Language
tags: C++
---

C++ 의 연산자 오버로딩에 대해 정리한다.

------

### 개요

  . 객체도 기본 자료형 변수처럼, 덧셈, 뺄셈 등 연산들을 가능하게 하는 방법

  . `operator` 키워드와 연산자를 묶어 함수의 이름을 정의

```c++
#include <iostream>

using std::endl;
using std::cout;

class Point{
    private:
        int x, y;
    public:
        Point(int _x=0, int _y=0):x(_x), y(_y){}
        void ShowPosition();
        void operator+(int val);        
};

void Point::ShowPosition(){
    cout << x << " " << y << endl;
}
void Point::operator+(int val)
{
    x += val;
    y += val;
}

int main(void)
{
    Point p(1,5);
    p.ShowPosition();

    p.operator+(10);
    // p+10;	위 행을 본 행으로 교체하여도 문제 없이 작동함
    p.ShowPosition();

    return 0;
}
```

![16](https://user-images.githubusercontent.com/29933947/36366893-8df50076-1593-11e8-9525-94265b5eebbd.png)



  . C++ 연산자 오버로딩 개념(위 예제에서)

![_ 3](https://user-images.githubusercontent.com/29933947/36368028-c521c3f4-1598-11e8-95a2-efe697aafbc1.png)



### 멤버 함수에 의한 오버로딩

```c++
#include <iostream>

using std::endl;
using std::cout;

class Point{
    private:
        int x, y;
    public:
        Point(int _x=0, int _y=0): x(_x), y(_y){}
        void ShowPosition();
        Point operator+(const Point& p) const;
};

void Point::ShowPosition(){
    cout << x << " " << y << endl;
}
Point Point::operator+(const Point& p) const{
    Point temp(x + p.x, y + p.y);
    return temp;
}

int main(void)
{
    Point p1(1, 2);
    Point p2(3, 4);
    Point p3 = p1 + p2;
    p3.ShowPosition();

    return 0;
}
```

![17](https://user-images.githubusercontent.com/29933947/36369292-1b846e4a-159e-11e8-9b6c-1ce32733b06d.png)



#### `Point Point::operator+(const Point& p) const ` 이해

  . Point 객체를 인자로 전달 받음(맨 앞 Point)

  . 함수 성능 향상을 위해 레퍼런스로 전달받음(Point &)

  . 전달 인자의 변경을 허용하지 않음 (const Point& p)

  . 함수 내에서 멤 버 변수의 조작을 할 필요 없으므로 함수 상수화(마지막 const)



#### 예제 객체 형성 및 연산 수행과정

  . 객체 생성

![_ 5](https://user-images.githubusercontent.com/29933947/36370204-8d6f55d0-15a1-11e8-9625-dea1c6ee25b7.png)



   . 연산 수행

![_ 4](https://user-images.githubusercontent.com/29933947/36370207-8f1951ec-15a1-11e8-93fc-9cdd16b917ba.png)



### 전역 함수에 의한 오버로딩



