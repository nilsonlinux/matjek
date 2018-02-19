---
layout: post
title: "C++ Static, Const, Explicit, Mutalbe"
date: 2018-02-20 12:00
categories: Program_Language
tags: C++
---

C++ static, const, explicit, mutable 에 대해 정리한다.

------



### explicit

  . 명시적 호출만을 허용

  . 아래 예제에서 `explicit` 선언을 한 생성자에 대해서는, 묵시적 호출을 허용하지 않아, 에러가 발생함

  . `explicit` 선언은 객체 생성 관계를 분명히 하고자 하는 경우에 사용됨

```c++
#include <iostream>
using std::cout;
using std::endl;

class First{
    public:
        explicit First(int a){
        //First(int a){
            cout << "explict First(int a)" << endl;
        }
};

int main(void)
{
    First first = 10;
    return 0;
}
```

![14](https://user-images.githubusercontent.com/29933947/36365238-f9b05bec-158b-11e8-8cd7-1be8033214bf.png)