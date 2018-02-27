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

```c++
... 
int a = 10 + 20;		// 일반산술연산
Point p3 = p1 + p2;		// 객체의 경우, 연산자 오버로딩 함수 호출
...
```

  . `operator` 키워드와 연산자를 묶어 함수의 이름을 정의

##### 주의할 점

> 잘못 사용하거나 남용할 경우, 프로그램을 복잡하고 이해하기 어렵게 만들 수 있음

> 연산자의 우선 순위, 결합성을 바꿀 수 없음

> 디폴트 매개 변수 설정 불가능

> 디폴트 연산자들의 기본 기능을 빼앗을 수 없음 ex) + → A + B + C (이항연산을 삼항연산으로 변경 불가능)



```c++
#include <iostream>

using std::endl;
using std::cout;

class Point{
    private:
        int x, y;
    public:
  		// `:` 멤버 이니셜라이져(member initializer) 활용한 생성자 초기화
        Point(int _x=0, int _y=0):x(_x), y(_y){}
        void ShowPosition();
        void operator+(int val);        
};

void Point::ShowPosition(){
    cout << x << " " << y << endl;
}

// 연산자 오버로딩
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
  	// 이 때, p가 기본 자료형 변수라면 단순 덧셈 연산
    // p가 객체라면, p.operator+(10) 으로 변경하여 수행
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

![_ 3](https://user-images.githubusercontent.com/29933947/36707783-3c2223c0-1bb3-11e8-92d1-1f4004ca1125.png)



  . 일반적으로 전역 함수에서 객체 멤버로의 접근(private 멤버로의 외부 함수에서 접근)은 불가능

  . 따라서, 전역 함수에서 연산자 오버로딩을 통한 객체 멤버의 조작을 위해서 `friend` 키워드를 활용함

  . 전역 함수에 의한 오버로딩은 최소화 하는 것이 바람직

```c++
#include <iostream>

using std::endl;
using std::cout;

class Point{
    private:
        int x;
        int y;
    public:
        Point(int _x=0, int _y=0):x(_x), y(_y){}
        void ShowData();
        // 외부에서 객체 멤버로의 접근을 위한 fried 선언
        friend Point operator+(const Point& p1, const Point& p2);     
};

void Point::ShowData(){
    cout << x << "  " << y << endl;
}

// 전역함수에 의한 연산자 오버로딩
Point operator+(const Point& p1, const Point& p2)
{
    Point temp(p1.x + p2.x, p1.y + p2.y);
    return temp;
}

int main(void)
{
    Point p1(10, 20);
    Point p2(20, 10);
    Point p3 = p1 + p2;
    p3.ShowData();  // Point p3 = operator+(p1, p2);

    return 0;
}
```

![4](https://user-images.githubusercontent.com/29933947/36711224-a0334e40-1bc5-11e8-9f3e-e0559352ae45.png)





### 단항 연산자의 오버로딩

![_ 1](https://user-images.githubusercontent.com/29933947/36733734-d3ea6c56-1c14-11e8-9c04-c11e528624b6.png)

```c++
#include <iostream>

using std::endl;
using std::cout;

class Point{
    private:
        int x;
        int y;
    public:
        Point(int _x=0, int _y=0):x(_x), y(_y){}
        void ShowData();
        Point& operator++();
        // 외부에서 객체 멤버로의 접근을 위한 fried 선언
        friend Point& operator--(Point& p);     
};

void Point::ShowData(){
    cout << x << "  " << y << endl;
}

Point& Point::operator++()  // 멤버 변수에 의한 오버로딩
{
    x++;
    y++;
    return *this;		// Class Point로 인해 만들어진 객체 자신을 리턴
}
/* 
   이미 증가연산을 수행하였는데, 객체 자신을 리턴하는 이유 
   만약 자신을 리턴하지 않는다면,
   ++(++p); 
   (++p).ShowData();
   와 같은 연산과 연결되어 수행하는 명령을 실행할 수 없어 컴파일 에러가 발생함
*/

// 전역함수에 의한 연산자 오버로딩
Point& operator--(Point& p)
{
    p.x--;
    p.y--;
    return p;
}

int main(void)
{
    Point p(10, 20);
    ++p;    //  객체 p의 x, y 값을 1 씩 증가
    p.ShowData();

    --p;    //  객체 p의 x, y 값을 1 씩 감소
    p.ShowData();

    ++(++p);    //  객체 p의 x, y 값을 2 씩 증가
    p.ShowData();

    --(--p);    //  객체 p의 x, y 값을 2 씩 감소
    p.ShowData();

    return 0;
}
```

![1](https://user-images.githubusercontent.com/29933947/36733516-3782eaf0-1c14-11e8-9684-e10fa9cc0bfa.png)



  . 위 예제에서 연산자 오버로딩 시, 참조형`Point&` 를 리턴하는 이유

![_ 2](https://user-images.githubusercontent.com/29933947/36734451-e5f631f8-1c16-11e8-97bc-49587629d876.png)



#### 선 연산과 후연산

