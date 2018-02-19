---
layout: post
title: "C++ 복사생성자"
date: 2018-02-20 12:00
categories: Program_Language
tags: C++
---

C++ 관련 복사생성자에 대해 정리한다.

------

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

