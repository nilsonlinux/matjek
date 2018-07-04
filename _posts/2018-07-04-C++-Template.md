---
layout: post
title: "C++ Template"
data: 2018-07-04 12:00
categories: Program_Language
tags: C++
---

C++ Template에 대해 정리한다.

-------

ㆍ



```c++
#include <iostream>
#include <cstring>

using std::cout;
using std::endl;

template <typename T>   // 타입에 상관없이 덧셈 연산 수행
T Add(T a, T b){
    return a+b;
}

template <typename T1, typename T2>     // 둘 이상의 타입에 대응
void ShowData(T1 a, T2 b){
    cout << "[ " << a << ", " << b << " ]" << endl;    
}

template <typename T>
int SizeOf(T a){
    return sizeof(a);
}

// 정확한 표현 
// template <> int SizeOf<char *>(char* a)
template <>             // 함수 템플릿 특수화 선언
int SizeOf(const char * a){   // 전달 인자가 char*인 경우에는 이 함수 호출
    return strlen(a);
}

int main(void){
    int i=10;
    const char* str = "Hello!";

    cout << "--------------------------" << endl;
    // 인자에 상관없는 덧셈 연산    
    cout << Add(10, 20) << endl;
    cout << Add(1.1, 2.2) << endl;

    cout << "--------------------------" << endl;
    // 서로 다른 두개의 타입에 대한 처리
    ShowData(1, 2);
    ShowData(3, 2.5);

    cout << "--------------------------" << endl;
    // 특수한 타입에 대하여 별도 연산(함수 템플릿 특수화)
    cout << SizeOf(i) << endl;
    cout << SizeOf(str) << endl;

    return 0;
}
```

![1](https://user-images.githubusercontent.com/29933947/42253619-787e23f4-7f7d-11e8-8d02-6e199b24e15b.png)





```c++
#include <iostream>
using std::cout;
using std::endl;

template <typename T>
class Data{
    private:
        T data;
    public:
        Data(T d);
        void SetData(T d);
        T Getdata();
};

template <typename T>
Data<T>::Data(T d){
    data=d;
}

template <typename T>
void Data<T>::SetData(T d){
    data=d;
}

template <typename T>
T Data<T>::Getdata(){
    return data;
}

int main(void){
    Data<int> d1(0);        // T를 int로 간주하고 객체를 생성함
    d1.SetData(100);

    Data<char> d2('c');     // T를 char로 간주하고 객체를 생성함

    cout << d1.Getdata() << endl;
    cout << d2.Getdata() << endl;

    return 0;
}
```

![5](https://user-images.githubusercontent.com/29933947/42253635-876a07b6-7f7d-11e8-823e-ae4150a8ae7a.png)











```c++
/*

// =============== 아래 프로그램을 Template화 =================

#include <iostream>
using std::cout;
using std::endl;

class Stack{
    private:
        int topIdx;     // 마지막 입력된 위치의 인덱스
        char* stackPtr; // 스택포인터
    public:
        Stack(int s=10);
        ~Stack();
        void Push(const char& pushValue);
        char Pop();
};

Stack::Stack(int len){
    topIdx=-1;                  // 스택 인덱스 초기화
    stackPtr=new char[len];     // 데이터 저장 위한 배열 선언    
}

Stack::~Stack(){
    delete [] stackPtr;    
}

void Stack::Push(const char& pushValue){    // 스택에 데이터 입력
    stackPtr[++topIdx] = pushValue;
}

char Stack::Pop(){                          // 스택에서 데이터 꺼냄
    return stackPtr[topIdx--];
}

int main(){
    Stack stack(10);
    stack.Push('A');
    stack.Push('B');
    stack.Push('C');

    for(int i=0; i<3; i++){
        cout << stack.Pop() << endl;
    }

    return 0;
}

*/

#include <iostream>
using std::cout;
using std::endl;

template <typename T>
class Stack{
    private:
        int topIdx;     // 마지막 입력된 위치의 인덱스
        T* stackPtr; // 스택포인터
    public:
        Stack(int s=10);
        ~Stack();
        void Push(const T& pushValue);
        T Pop();
};

template <typename T>
Stack<T>::Stack(int len){
    topIdx=-1;                  // 스택 인덱스 초기화
    stackPtr=new T[len];        // 데이터 저장 위한 배열 선언    
}

template <typename T>
Stack<T>::~Stack(){
    delete [] stackPtr;    
}

template <typename T>
void Stack<T>::Push(const T& pushValue){    // 스택에 데이터 입력
    stackPtr[++topIdx] = pushValue;
}

template <typename T>
T Stack<T>::Pop(){                          // 스택에서 데이터 꺼냄
    return stackPtr[topIdx--];
}

int main(){
    Stack<char> stack1(10);
    stack1.Push('A');
    stack1.Push('B');
    stack1.Push('C');

    for(int i=0; i<3; i++){
        cout << stack1.Pop() << endl;
    }

    Stack<int> stack2(10);
    stack2.Push(100);
    stack2.Push(200);
    stack2.Push(300);

    for(int i=0; i<3; i++){
        cout << stack2.Pop() << endl;
    }

    return 0;
}
```

![3](https://user-images.githubusercontent.com/29933947/42253634-85e5cbdc-7f7d-11e8-848e-daa5a6599380.png)