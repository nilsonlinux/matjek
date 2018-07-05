---
layout: post
date: 2018-07-05 12:00
title: "C++ Exception Handling"
categories: Program_Language
tags: C++
---

C++ 예외처리에 대해 정리한다.

------

### 예외처리(Try, Catch, Throw)

ㆍ예외 상황을 처리하는 코드부분을 독립시켜 유지보수 및 코드 가독성을 높이기 위함



#### 기본 구성

```c++
try {
   / * 예외 발생 예상 지역 */
   throw ex; 	// 예외 전달(catch block으로)
}
catch (처리되어야 할 예외의 종류) {
   / * 예외를 처리하는 코드가 존재할 위치 */
}
```

> 전달되는 예외와 이를 받아주는 변수의 자료형은 일치해야 함



ㆍ예외의 발생 및 처리 과정

![_](https://user-images.githubusercontent.com/29933947/42308058-6d5d065a-806f-11e8-8103-436cfdc27e92.png)



```c++
#include <iostream>
using std::cout;
using std::endl;
using std::cin;

int main(void){
    int a, b;

    cout << "두 개 숫자 입력: ";
    cin >> a >> b;

    try{
        cout << "Start a try block" << endl;

        if(b==0)
            throw b;
        cout << "a/b의 몫: "<< a/b << endl;
        cout << "a/b의 나머지: "<< a%b << endl;

        cout << "End a try block" << endl;
    }
    catch(int exception){
        cout << "Start a catch block" << endl;

        cout << exception << "입력" << endl;
        cout << "입력오류! 다시 실행하세요." << endl;

        cout << "End a catch block" << endl;
    }

    cout << "감사합니다." << endl;

    return 0;
}
```

ㆍ정상 실행

![5](https://user-images.githubusercontent.com/29933947/42308109-949438ce-806f-11e8-94b3-ee238dbf75ba.png)

ㆍ예외 발생

![6](https://user-images.githubusercontent.com/29933947/42308110-95e74dce-806f-11e8-86be-482421e4c45f.png)

> 예외가 발생하면 throw 이후의 try 블록 내의 소스들은 실행되지 않는다.



#### Stack Unwinding(스택 풀기)



