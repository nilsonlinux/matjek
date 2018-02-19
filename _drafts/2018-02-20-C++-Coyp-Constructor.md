---
layout: post
title: "C++ 복사생성자"
date: 2018-02-20 12:00
categories: Program_Language
tags: C++
---

C++ 관련 복사생성자에 대해 정리한다.

------

### 명시적[^1], 묵시적[^2] 초기화

[^1]: 내용이나 뜻을 분명하게 드러내 보이는
[^2]: 직접적으로 말이나 행동으로 드러내지 않고 은연중에 뜻을 나타내 보이는

```c++
#include <iostream>

using std::cout;
using std::endl;

class First{
    int val;
    public:
        First(int a){
            val = a;
        }
        void ShowData(){
            cout << val << endl;
        }
};

int main(void)
{
    int a = 10;     // 명시적 초기화
    int b(20);      // 묵시적 초기화

    First f1(10);   // 묵시적 초기화
    f1.ShowData();

    First f2=20;    // 명시적 초기화
    f2.ShowData();

    cout << "a: " << a <<endl;
    cout << "b: " << b <<endl;

    return 0;
}
```

![15](https://user-images.githubusercontent.com/29933947/36366052-b01e0b56-158f-11e8-9b13-7fb5eefa5753.png)





### 복사 생성자

#### 형태

```c++
#include <iostream>
using std::cout;
using std::endl;

class First{
    public:
        First(){
            cout << "First() 호출" << endl;
        }
        First(int a){
            cout << "First(int a) 호출" << endl;
        }
  		// 복사 생성자
  		// const 인자로 전달된 객체의 내용 변경을 허용하지 않음 (선택사항) 
  		// & 인자로 전달된 객체를 레퍼런스로 받음 (필수사항
        First(const First& a){
            cout << "First(const First& a) 호출" << endl;
        }
};

int main(void)
{
    First f1;   // call First();
    First f2(100);   // call First(int a);
    First f3(f2);   // call First(const First& a);

    return 0;
}
```

![1](https://user-images.githubusercontent.com/29933947/36382060-0d5df84a-15cb-11e8-98fc-6890f6b48201.png)

  . `&`  연산자의 경우, 생략하면 무한루프에 빠지게 됨



#### 디폴트(Default) 복사 생성자

  . 작성하지 않은 경우, 자동으로 삽입됨

  . 멤버 변수 대 맴버 변수의 복사를 수행함

  . 따라서, 클래스 마다 디폴트 복사 생성자의 정의된 형태는 다름

```c++
#include <iostream>

using std::cout;
using std::endl;

class Point{
    int x, y;
    public:
        Point(int _x, int _y){
            x = _x;
            y = _y;
        }
  		// default copy constructor
  		// 해당 함수가 없어도 정상 작동, 함수의 역할은 디폴트 복사 생성자의 역할과 동일
    	/*
        Point(const Point& p){
            x = p.x;
            y = p.y;
        }
        */
        void ShowData(){
            cout << x << " " << y << endl;
        }
};

int main(void)
{
    Point p1(10, 20);
    Point p2(p1);

    p1.ShowData();
    p2.ShowData();

    return 0;
}
```

![2](https://user-images.githubusercontent.com/29933947/36382388-0ae88a98-15cc-11e8-89b8-5d722b6a5c3e.png)



