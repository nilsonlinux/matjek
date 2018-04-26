---
layout: post
title: "C++ 가상함수와 다중상속"
date: 2018-04-26 12:00
categories: Program_Langague
tags: C++
---

C++의 가상함수와 다중 상속에 대해 정리한다.

------



```c++
#include <iostream>
using std::cout;
using std::endl;

class Base{
    int a, b;
    public:
        virtual void func1() { cout << " func1( ... ) " << endl; }
        virtual void func2() { cout << " func2( ... ) " << endl; }
};

class Derived : public Base{
    int c, d;
    public:
        virtual void func1() { cout << " overriding func1( ... ) " << endl; }
        void func3() { cout << " func3( ... ) " << endl; }        
};

int main(void)
{
    Base* bbb = new Base();
    bbb->func1();

    Derived* ddd = new Derived();
    ddd->func1();

    return 0;
}
```

![1](https://user-images.githubusercontent.com/29933947/39279152-44a442d8-4932-11e8-9bb5-f9d35ea0a019.png)



![_ 1](https://user-images.githubusercontent.com/29933947/39279872-a186a2bc-4936-11e8-921a-594355511a69.png)



![_ 4](https://user-images.githubusercontent.com/29933947/39279885-bba7dee0-4936-11e8-861a-6dc6eb523302.png)





![_ 3](https://user-images.githubusercontent.com/29933947/39279871-a15d9cfa-4936-11e8-93fa-8cc957f1df06.png)

