---
layout: post
title: "C 파일 입출력"
date: 2018-01-27 00:30
categories: Program_Language
tags: c
---

C언어의 파일 입출력에 대해 정리한다.

------

  ### 파일입출력 스트림

![2](https://user-images.githubusercontent.com/29933947/35490439-f390d642-04e2-11e8-895b-09382131dfe1.png)

  . r+, w+ 등의 읽기와 쓰기가 가능한 모드도 있으나, 작업 변경 버퍼 비움 필요와 위험성으로 사용하지 않음

  . 바이너리 파일(Binary file)은 컴퓨터가 인식할 수 있는 데이터 및 주로 음원, 이미지 들의 파일

  

### 파일 입출력 기본함수

```c
#include <stdio.h>
FILE * fopen(const char * filename, const char * mode)
```

  . File : 구조체 이름

  . filename: 작업할 파일 이름

  . mode: 입출력 스트림 지정

  . 지정한 파일과의 입출력 스트림을 형성하고, 스트림 정보를 FILE 구조체 변수에 담아 변수의 주소 값을 반환

![_ 1](https://user-images.githubusercontent.com/29933947/35490156-eab03c36-04e0-11e8-9d36-1e9695cc4ec5.png)



  . fopen 함수 호출 시, FILE 구조체 변수 생성

  . 생성된 FILE 구조체 변수에는 파일에 대한 정보 담김

  .  FILE 구조체 포인터는 파일을 가리키는 '지시자' 역할



```c
#include <stdio.h>
int fclose(FILE * stream);
int fflush(FILE * stream);
```

  . 성공 시, `0` , 실패 시 `EOF` 반환

  . fclose는 파일과 연결된 스트림을 해제하는 함수

  . fclose는 운영체제가 할당한 자원의 반환, 버퍼링 되었던 데이터의 출력을 위함

  . fflush는 출력버퍼를 비우는 함수



```c
#include <stdio.h>

int filecheck(FILE ** file)
{
    if(file==NULL)
    {
        puts("파일 오픈 실패");
        return -1;
    }
}

int main(void)
{
  FILE * fpw = fopen("filefunctest.txt", "wt");
  FILE * fpr = NULL;
  char str[50];
  int ch, i;

  filecheck(&fpw);

  fputc('A', fpw);
  fputc('B', fpw);
  fputc('C', fpw);
  fputc('1', fpw);
  fputc('2', fpw);
  fputc('3', fpw);

  fputs("This is filefunc test \n", fpw);

  fclose(fpw);


  fpr=fopen("filefunctest.txt", "rt");
  filecheck(&fpr);

  for(i=0; i<6; i++)
  {
     ch = fgetc(fpw);
     printf("%c \n", ch);
  }

  fgets(str, sizeof(str), fpw);
  printf("%s", str);

  fclose(fpr);

  return 0;
}
```

![2](https://user-images.githubusercontent.com/29933947/35491350-6191dbd6-04e9-11e8-8f7d-69b563771b1e.png)



#### feof

  . 파일의 끝을 확인하는 함수

  . 파일 복사 시, 주로 사용됨

```c
#include <stdio.h>
int feof(FILE * stream);
```

  . 파일의 끝에 도달하면 0이 아닌 값을 반환함

```c
#include <stdio.h>

int main(void)
{
    FILE * src=fopen("src.txt", "rt");
    FILE * des=fopen("des.txt", "wt");
    char str[20];

    if(src==NULL || des==NULL)
    {
        puts("파일 오픈 실패");
        return -1;
    }

    while(fgets(str, sizeof(str), src) != NULL)
        fputs(str, des);

    if(feof(src)!=0)
        puts("파일 복사 완료");
    else
        puts("파일 복사 실패");

    fclose(src);
    fclose(des);

    return 0;
}
```

![3](https://user-images.githubusercontent.com/29933947/35491653-2423b8b2-04eb-11e8-93c8-bda0535dcea1.png)



####fread, fwrite

#### fprintf, fscanf

#### fseek

#### ftell













