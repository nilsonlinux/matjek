---
layout: posts
title: "C언어 정리-배열,포인터"
date: 2018-01-22 19:00
Categories: Program-Language
Tags: C
---

C언어 배열, 포인터 관련 내용 정리

------

#### 배열의 크기 

```c
int arr1[4] = {1,2,3};

arr1_length = sizeof(arr1) / sizeof(int);
```



#### 문자열 변수 표현

```c
char str[] = "Hello World";
```

![_ 1](https://user-images.githubusercontent.com/29933947/35223224-e8553ab2-ffc3-11e7-8683-bfce4d5f5a38.png)

 . ''\0''은 "NULL 문자", 해당 문자의 아스키 코드 값은 "0"

 . 저장된 데이터에 널문자가 존재하면 해당 데이터는 문자열로 취급함



#### 포인터

##### 정의

 . 메모리 직접 접근이 가능한 연산(주소값)

```c
int *ptr;
int num;

ptr = &num;
```

  . int * : int형 변수의 주소 값 저장을 위한 포인터 변수

  . ptr : 포인터 변수 이름

  . &num : int형 변수 num의 주소 값을 반환

##### 포인터형

```c
type * ptr;
type* ptr;
type *ptr;
```

  . type형 변수의 주소 값을 저장하는 포인터 변수

  . type은 int, double ... etc

  . 주소 값은 동일 시스템 내에선 크기가 동일(8bit, 16bit, 32bit, 64bit ... etc)

  . 포인터 변수가 가리키는 메모리의 접근 기준(몇 바이트를 접근할지)을 위해 "포인터형(type형)"을 선언

##### 연산자 '*'

```c
int num = 100;
int *pnum = &num;
*pnum += 20;
printf("number is %d \n", *pnum);
```

  . '*' 연산자는 포인터가 가리키는 메모리 공간에 접근 시 사용하는 연산자



#### 배열과 포인터 관계

  . 'arr[10]' 배열에서 배열의 이름인 'arr' 은 '포인터 상수'

  . 포인터 상수는, 포인터 변수와 달리 주소 값의 변경이 불가능함

  . 배열의 이름을 피연산자로 하는 * 연산 가능

  . 포인터 변수 ptr은 ptr[0], ptr[1] .. 등의 배열형태로 사용 가능

```c
#include <stdio.h>

int main(void)
{
	int arr[2] = {10, 20};
	int * ptr = arr; //int * ptr = arr[]
	
	printf("%d %d \n", ptr[0], arr[0]);
	printf("%d %d \n", ptr[1], arr[1]);	
	printf("%d %d \n", *ptr, *arr);	
}	
```

![1](https://user-images.githubusercontent.com/29933947/35225697-5c834782-ffcc-11e7-8053-3d11a4bbf9f0.png)

##### *(++ptr) vs *(ptr+1)

  . 두 연산은 모두, 현재 ptr이 가리키는 위치에서 4바이트(int형일 경우) 떨어진 메모리 공간을 가리킴

  . *(++ptr)은 ptr이 가리키는 주소값 자체를 증가시킴

  . *(ptr+1)은 ptr이 가리키는 위치에서 4바이트 떨어진 메모리 공간만을 가리킴

```c
#include <stdio.h>

int main(void)
{
	int arr[3] = {10, 20, 30};
	int * ptr = arr; //int * ptr = arr[]
	
	printf("\n");
	printf("*ptr: %d \n", *ptr);
	printf("ptr: %p \n", ptr);

	printf("\n");	
	printf("*(++ptr): %d \n", *(++ptr));
	printf("ptr after *(++ptr): %p \n", ptr);
	
	printf("\n");
	printf("*(ptr+1): %d \n", *(ptr+1));
	printf("ptr after *(ptr+1): %p \n", ptr);
	
	return 0;
}	
```

![4](https://user-images.githubusercontent.com/29933947/35227458-8138aab8-ffd1-11e7-8b16-ebabd990ffbd.png)



#### arr[i] ==  *(arr+i)

```c
..

int arr[3] = {10, 20, 30}
int * ptr=arr;

//동일 표현
arr[0], arr[1], arr[2]
*(arr+0), *(arr+1), *(arr+2)
ptr[0], ptr[1], ptr[2]
*(ptr+0), *(ptr+1), *(ptr+2)
```



#### 배열 혹은 포인터 선언에 의한 문자열

```c
#include <stdio.h>

int main(void)
{
 	char str1[] = "This is String"; // 변수 형태 문자열
  	char * str2 = "That is String";	// 상수 형태 문자열
  
  	printf("initial value: %s %s \n",str1, str2);
  	
  	str2 = "It is not String"; // 가리키는 대상 변경 가능, str1은 변경 불가
  	printf("change str2: %s\n", str2);
  
  	str1[0] = 'A';
  	//str2[0] = 'A'; // 컴파일 시 에러
  	
  	printf("after changing characther on s1: %s %s \n",str1, str2);
   	return 0;
}
```

![1](https://user-images.githubusercontent.com/29933947/35253634-de1fc650-0029-11e8-9ecc-934e3afcdc9b.png)

![_ 1](https://user-images.githubusercontent.com/29933947/35253451-da3e6aec-0028-11e8-93ec-79bd0eb7d1a0.png)

![_ 2](https://user-images.githubusercontent.com/29933947/35253458-dee89c16-0028-11e8-8dac-56ddc3795312.png)



   . ""로 묶인 문자열은 메모리에 저장되면 그 주소 값을 반환함

   . 따라서  printf("Hello World") 는 printf(0x123456)의 형태로 호출됨

   . ex) printf(0x123456) ....... void printf(char * str)



#### 포인터 배열

```c
#include <stdio.h>

int main(void)
{
   	int num1=10, num2=20, num3=30;
   	
   	// 포인터 배열
 	int * arr[3]={&num1, &num2, &num3};
   	char * strArr[3] = {"String", "Array", "Test"};

   	printf("*arr[0]: %d \n", *arr[0]);
   	printf("*arr[1]: %d \n", *arr[1]);
   	printf("*arr[2]: %d \n", *arr[2]);
   	
   	printf("strArr[0]: %s \n", strArr[0]);
   	printf("strArr[1]: %s \n", strArr[1]);
   	printf("strArr[2]: %s \n", strArr[2]);
   	
   	return 0;
}
```

![2](https://user-images.githubusercontent.com/29933947/35254481-ba76f27e-002d-11e8-9847-1ab97e44ddfb.png)

![_ 3](https://user-images.githubusercontent.com/29933947/35254402-65e48b0e-002d-11e8-871c-d378c2fc3ba0.png)
![_ 4](https://user-images.githubusercontent.com/29933947/35254404-66161b42-002d-11e8-9594-d34036e6d86c.png)

#### 함수 인자의 배열 전달



