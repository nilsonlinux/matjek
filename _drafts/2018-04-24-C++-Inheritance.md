---
layout: post
title: "C++ Inheritance (상속)"
date: 2018-04-24 12:00
categories: Program_Language
tags: C++
---

C++의 상속 개념 및 사용법에 관해 정리한다.

------

### 개요

> 기존에 정의한 클래스를 재활용하기 위한 방법

> 클래스의 공통되는 부분을 Base 클래스로 추상화 하고, 특징을 지닌 Derived 클래스를 정의할 수 있음

  . AA 클래스가 A 클래스를 상속할 경우

​    : B 클래스는 "A 클래스에 선언되어 있는 멤버 + B 클래스에 선언된 멤버" 를 지님

  . 상속되는 클래스 : Super class or Base class

  . 상속받는 클래스 : Sub class or Derived class



```c++
						class Base : public Derived
```

```c++
#include <iostream>
#include <cstring>

using std::endl;
using std::cout;

class Person
{
    int age;
    char name[20];

    public:
        int GetAge() const {
            return age;
        }
        const char* GetName() const {
            return name;
        }
        Person(int _age=1, char* _name="none"){
            age = _age;
            strcpy(name, _name);
        }    
};

class Student: public Person    // Person 클래스를 상속
{
    char major[20];

    public:
        Student(char* _major){
            strcpy(major, _major);
        }
        const char* GetMajor() const {
            return major;            
        }
        void ShowData() const {
            cout << "이름 :" << GetName() << endl;
            cout << "나이 :" << GetAge() << endl;
            cout << "전공 :" << GetMajor() << endl;
        }
};

int main(void)
{
    Student Lee("Computer");
    Lee.ShowData();

    return 0;
}
```

![5](https://user-images.githubusercontent.com/29933947/39176079-d3d98f5a-47e6-11e8-8ce7-97121bc009ea.png)



  . Student 객체가 처음 생성 되었을 때, 모습

![_ 1](https://user-images.githubusercontent.com/29933947/39176196-33e0a55a-47e7-11e8-987c-5148ea025b08.png)



#### 생성 및 소멸

  . 생성 과정

1. 메모리 공간 할당, 상속되는 클래스를 감안하여 메모리가 할당됨

   ![_ 2](https://user-images.githubusercontent.com/29933947/39177526-81882294-47ea-11e8-87ad-11c2306980e4.png)

2. Derived 클래스 생성자 호출

   ![_ 3](https://user-images.githubusercontent.com/29933947/39177528-82f5825c-47ea-11e8-8f4f-8ad2d8539757.png)

     : 이 때, BBB(init j) 생성자가 호출만 될 뿐, 함수의 몸체( { ... } )부분은 실행되지 않음

     : 상속하고 있는 AAA의 클래스 생성자가 우선 실행 된 후, 실행되어야 하기 때문임

     : 별 다른 선언(상속하고 있는 AAA 클래스의 어떤 생성자 호출할지 여부)가 없으면, Void 생성자 호출

     : 상속하고 있는 클래스의 특정 생성자 호출 시, `멤버 이니셜라이저` 활용

   ```c++
   BBB(int j) : AAA(j) {
      cout << " BBB(int j) call!" << endl; 
   }
   ```

   ​

3. Base 클래스 생성자 실행

   ![_ 4](https://user-images.githubusercontent.com/29933947/39177529-8456177e-47ea-11e8-8409-ef4420012c38.png)

   ​

4. Derived 클래스 생성자 실행

   ![_ 5](https://user-images.githubusercontent.com/29933947/39178519-e03d7c06-47ec-11e8-837f-9d5fc814205b.png)

   ​

```c++
#include <iostream>
#include <cstring>

using std::endl;
using std::cout;

class AAA{
    public:
        AAA(){
            cout << "AAA() call!" << endl;
        }
        AAA(int i){
            cout << "AAA(int i) call!" << endl;
        }    
};

class BBB : public AAA{
    public:
        BBB(){
            cout << "BBB() call!" << endl;
        }
        BBB(int j){
            cout << "BBB(int j) call!" << endl;
        }    
};

int main(void)
{
    cout << "객체 1 생성" << endl;
    BBB bbb1;

    cout << "객체 2 생성" << endl;
    BBB bbb2(10);

    return 0;
}
```

![6](https://user-images.githubusercontent.com/29933947/39177352-0cb60ff8-47ea-11e8-8004-9eeaba747841.png)



##### 상속 클래스 객체 생성에 따른 초기화

```c++
#include <iostream>
#include <cstring>
using std::endl;
using std::cout;

class Person
{
    int age;
    char name[20];

    public:
        int GetAge() const {
            return age;
        }
        const char* GetName() const {
            return name;
        }
        Person(int _age=1, char* _name="none"){
            age = _age;
            strcpy(name, _name);
        }    
};

class Student: public Person
{
    char major[20];

    public:
        Student(int _age, char* _name, char* _major) : Person(_age, _name){
            // age = _age;          // compile error
            // strcpy(name, _name); // compile error
            strcpy(major, _major);
        }
        const char* GetMajor() const {
            return major;            
        }
        void ShowData() const {
            cout << "이름 :" << GetName() << endl;
            cout << "나이 :" << GetAge() << endl;
            cout << "전공 :" << GetMajor() << endl;
        }
};

int main(void)
{
    Student Lee(30, "Lee Yuna", "Computer");
    Lee.ShowData();

    return 0;
}
```

![7](https://user-images.githubusercontent.com/29933947/39178643-36c5fd46-47ed-11e8-85ad-3e9085c4036a.png)



   . 위 예제에서, `compile error`  로 주석 처리된 부분을 활성화 하기 위해서는, Person 클래스의 age,     

​     name을 public 멤버로 설정해야함  → `정보은닉` 문제 발생

  . 때문에, 예제에서 처럼, `: Person(_age, _name)` 을 통해 생성자 명시적 호출

```c++
        Student(int _age, char* _name, char* _major) : Person(_age, _name){
            strcpy(major, _major);
        }
```

 

  . 소멸 과정

1.  Derived 클래스 소멸자 실행
2.  Base 클래스 소멸자 실행

```c++
#include <iostream>
#include <cstring>

using std::endl;
using std::cout;

class AAA{
    public:
        AAA(){
            cout << "AAA() call!" << endl;
        }
        ~AAA(){
            cout << " ~AAA() call!" << endl;
        }
 
};

class BBB : public AAA{
    public:
        BBB(){
            cout << "BBB() call!" << endl;
        }
        ~BBB(){
            cout << " ~BBB() call!" << endl;
        }    
};

int main(void)
{    
    BBB bbb;
    return 0;
}
```

![8](https://user-images.githubusercontent.com/29933947/39179286-e4497172-47ee-11e8-9eb4-19dc674e791f.png)

  . 상속받은 클래스에 대한 객체 소멸 시, 상속하는 클래스의 소멸자 호출!



### protected 멤버

  `protected 멤버는 외부에서 볼 때 private, 상속 관계에서는 public`

  `protected 멤버는 상속 관계에서만 접근을 허용함`



```c++
#include <iostream>
#include <cstring>

using std::endl;
using std::cout;

class AAA{
    private:
        int a;
    protected:
        int b; 
};

class BBB : public AAA{
    public:
        void SetData(){
            // a = 10; // private member, Compile Error
            b = 20; // protected member, working
        }    
};

int main(void)
{    
    AAA aaa;
    // aaa.a = 10; // private member, Compile Error
    // aaa.b = 20; // protected member, Compile Error

    BBB bbb;
    bbb.SetData();   

    return 0;
}
```



### 상속 형태

![_ 6](https://user-images.githubusercontent.com/29933947/39181318-3eb9ee7a-47f4-11e8-8427-daceb535cbba.png)

  . 각각의 상속은 본인보다 접근 권한이 넓은 것을 본인하고 동일하게 맞춤





### 상속 조건

#### IS-A 관계

![_ 7](https://user-images.githubusercontent.com/29933947/39181888-0820b46e-47f6-11e8-8a3e-d269b8494e0b.png)



#### HAS-A 관계

![_ 8](https://user-images.githubusercontent.com/29933947/39182054-82bbeca2-47f6-11e8-971f-75375f767e53.png)

```c++
#include <iostream>
using std::endl;
using std::cout;

class Cudgel{
    public:
        void Swing(){ cout << "Swing a cudgel!" << endl; }    
};

class Police : public Cudgel
{
    public:
        void UseWeapon(){ Swing(); }
};

int main()
{
    Police p1;
    p1.UseWeapon();
    return 0;
}
```

![9](https://user-images.githubusercontent.com/29933947/39182401-c0c95f56-47f7-11e8-8f6c-4e10bfa08e11.png)



##### HAS-A 관계와 유사한 역할을 하는 포함관계-1

```c++
#include <iostream>
using std::endl;
using std::cout;

class Cudgel{
    public:
        void Swing(){ cout << "Swing a cudgel!" << endl; }    
};

class Police
{
    Cudgel cud;     // 클래스 객체를 멤버화
    public:
        void UseWeapon(){ cud.Swing(); }
};

int main()
{
    Police p1;
    p1.UseWeapon();
    return 0;
}
```

![10](https://user-images.githubusercontent.com/29933947/39183183-24b9b95a-47fa-11e8-883f-5910502c21d2.png)



![_ 9](https://user-images.githubusercontent.com/29933947/39183485-1eb75674-47fb-11e8-8af5-65444a9b711c.png)



##### HAS-A 관계와 유사한 역할을 하는 포함관계-2

```c++
#include <iostream>
using std::endl;
using std::cout;

class Cudgel{
    public:
        void Swing(){ cout << "Swing a cudgel!" << endl; }    
};

class Police
{
    Cudgel* cud;     // 클래스 객체를 멤버화
    public:
        Police(){
            cud = new Cudgel;            
        }
        ~Police(){
            delete cud;
        }
        void UseWeapon(){ cud->Swing(); }
};

int main()
{
    Police p1;
    p1.UseWeapon();
    return 0;
}
```

![11](https://user-images.githubusercontent.com/29933947/39183184-24e63cdc-47fa-11e8-826d-2da314025d80.png)



![_ 10](https://user-images.githubusercontent.com/29933947/39183504-312de2dc-47fb-11e8-82df-157de38c9b2f.png)







### 상속된 객체와 포인터



