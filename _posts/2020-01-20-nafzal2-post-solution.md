---
layout: post
title: "[나프잘 프로그래밍 2권] 문제풀이"
excerpt: "나프잘 C & JAVA 프로그래밍 2권 문제풀이"
modified: 2020-01-20
tags: [나프잘 프로그래밍 2권]
comments: true
pinned: true
categories: "나프잘프로그래밍(2권)"
image:
  feature: feature_for_nafzal.jpg
---

## 2권을 보면서 느낀점...일까?

(2020-01-19)
나프잘 프로그래밍 2권은 1권에서 배운 내용을 다시 한번 복습하는 개념으로 쓰여진 책인 거 같다. 문제를 이해하고 설계, 순서도, 나씨 슈나이더만 다이어그램, 구현까지 문제 하나에 대한 저자의 생각을 따라가면서 '감'이란걸 느낄 수 있었다. 이렇게 한 장, 한 장씩 넘기다보면 제일 마지막에는 문제를 내주면서 끝이 난다. 총 8 문제로 어떻게 보면 간단한 문제들을 이 책의 내용에서 소개해준 과정을 하기 위해서는 시간이 많이 걸렸다. 문제 이해가 빨리되었다 해도 기술서 작성, 순서도, 나씨-슈나이더만 다이어그램....을 그리다보면 '내가 꼭 이걸 해야되나?'하기도 한다. 금요일에서 주말까지(주말은 간간히 시간내면서) 차근차근 생각하면서 과정을 살펴보았다. 

(2020-01-20)
구현은 이제 해야된다.

## 문제
>1. 1+3+5+7+...+99까지 홀수의 합을 구하시오.
>2. 1에서 100까지 수 중 홀수의 합과 짝수의 합을 구하시오.
>3. 1+(1+2)+(1+2+3)+...+(1+2+3+4+...+100)까지의 합을 구하시오.
>4. 1-2+3-4+5...+99-100에서 합을 구하시오.
>5. 1에서 100까지 수 중에서 3의 배수와 5의 배수를 제외한 합을 구하시오.
>6. 1-(1/2)+(1/3)-...+(1/99)-(1/100) 합을 구하시오.
>7. 1-(2/3!)+(3/5!)-...-(10/19!
>8. 다음과 같은 수열을 피보나치(Fibonacci) 수열이라고 합니다.
>   1,1,2,3,5,8,13,21 ...
>   즉 앞의 두 항을 합하면 다음 항이 됩니다. 50번째 피보나치 수를 구하시오.

## 모듈 기술서, 순서도, NS-Charts

아래는 각 문제 번호에 따른 모듈 기술서, 순서도, NS-Chart이다.

### 문제 1

![9장_내부 설계(모듈 기술서) 문제 1](https://user-images.githubusercontent.com/25213941/72692518-cd4cea00-3b6f-11ea-8866-8eb0a8a40cb7.png)

(2020-01-20)

이전에 올린 모듈 기술서가 디버깅해본 결과 잘못 작성되었다. 홀수를 판단하는 분기점에서 짝수이면 합을 더하기로 되있다..;;

#### 모듈 기술서 변경 후

![p482-c9-q1-v2](https://user-images.githubusercontent.com/25213941/72702539-63940680-3b96-11ea-9d5f-099446f0a282.png)

코드는 아래와 같이 작성하였다.

{% highlight c %}

//1_oddAdder.c
/**************************************************************************
 * 파일   명칭 : oddAdder.c
 * 기       능 : 1부터 100까지의 홀수 합 계산
 * 함수   명칭 : main
 * 출       력 : 홀수합
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/01/20
**************************************************************************/
#include <stdio.h>

#define MAX 10
#define DIVIDER 2

int main(int argc, char* argv[]) {

	unsigned long oddSum = 0;
	unsigned long number = 1;
	unsigned long remainder = 0;

	//2. 수가 MAX보다 작거나 같을 때까지 반복한다.
	while (number <= MAX) {
		//2.1. 수가 홀수인지 판단한다.
		remainder = number % DIVIDER;
		if (remainder != 0) {
			//2.1.1. 홀수이면 홀수 합을 구한다.
			oddSum += number;
		}
		//1. 수를 증가한다.
		number++;
	}
	//3. 홀수 합을 출력한다.
	printf("oddSum : %d\n", oddSum);
	//4. 끝낸다.
	return 0;
}

{% endhighlight c %}

### 문제 2

![9장_내부 설계(모듈 기술서) 문제 2](https://user-images.githubusercontent.com/25213941/72692544-d938ac00-3b6f-11ea-9140-a72c5a1a5d4e.png)

(2020-01-20)

'1부터 100까지의 수 중의 합'이라는 말이 헷갈린다. 저자의 이런 말이 들어간 문제는 값을 입력받아 처리하는 문제가 있었기 때문이다. 그래서 위의 그림 또한 변경이 되어야한다.

#### 모듈 기술서 변경 후

![p482-c9-q2_v2](https://user-images.githubusercontent.com/25213941/72702537-62fb7000-3b96-11ea-9ba1-e4c00cd0306e.png)

코드는 아래와 같이 작성하였다.

{% highlight c %}
//2_oddEvenAdder.c
/**************************************************************************
 * 파일   명칭 : 2_oddEvenAdder.c
 * 기       능 : 1부터 100까지의 수 중의 홀수 합과 짝수 합을 구한다.
 * 함수   명칭 : main
 * 출       력 : 홀수합, 짝수합
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/01/20
**************************************************************************/
#include <stdio.h>
#define MAX 100
#define DIVIDER 2

int main(int argc, char *argv[]){

    unsigned long oddSum = 0;
    unsigned long evenSum = 0;
    unsigned long number = 1;
    unsigned long remainder = 0;

    //2. 수가 작거나 같을 때까지 반복한다.
    while(number <= MAX){
        //2.1. 수가 홀수인지 짝수인지 판별한다.
        remainder=number%DIVIDER;
        if(remainder != 0){
            //2.1.1. 홀수이면 홀수합을 구한다.
            oddSum+=number;
        }else{
            //2.1.2. 짝수이면 짝수합을 구한다.
            evenSum+=number;
        }
        //1. 수를 증가한다.
        number++;
    }
    //3. 홀수 합과 짝수 합을 출력한다.
    printf("oddSum : %d, evenSum : %d\n", oddSum, evenSum);
    //4. 끝낸다.
    return 0;
}
{% endhighlight %}

### 문제 3

![9장_내부 설계(모듈 기술서) 문제 3](https://user-images.githubusercontent.com/25213941/72692564-f66d7a80-3b6f-11ea-9721-c3af1f2c0342.png)

(2020-01-20)

이중 반복문을 안쓰고 설계를 해보았지만 해결하지 못하였다. 그래서 이중 반복문을 사용하는 것으로 설계를 바꾸었다.

#### 모듈 기술서 변경 후

![p482-c9-q3-v2](https://user-images.githubusercontent.com/25213941/72702538-62fb7000-3b96-11ea-98be-0463d7728a07.png)

코드는 아래와 같이 작성하였다.

{% highlight c %}
//3_sequenceAdder.c
/**************************************************************************
 * 파일   명칭 : 3_sequenceAdder.c
 * 기       능 : 1+(1+2)+(1+2+3)+...+(1+2+3+4+...+100)까지의 합을 구한다.
 * 함수   명칭 : main
 * 출       력 : 총합
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/01/20
**************************************************************************/
#include <stdio.h>

#define MAX 100

int main(int argc, char* argv[]) {

	unsigned long sum = 0;
	unsigned long temp = 0;
	unsigned long number = 1;

	//2. 수가 MAX보다 작거나 같을 때까지 반복한다.
	while (number <= MAX) {
		//2.2. 이전까지의 합을 구한다.
		for (temp = 1; temp < number; temp++) {
			sum += temp;
		}
		//2.1. 총합을 구한다.
		sum += number;
		//1. 수를 증가한다.
		number++;
	}
	//3. 총합을 출력한다.
	printf("1부터 %d까지의 순차합 : %d\n", MAX, sum);

	//4. 끝낸다.
	return 0;
}
{% endhighlight %}

### 문제 4

![9장_내부 설계(모듈 기술서) 양식 문제 4](https://user-images.githubusercontent.com/25213941/72692575-01c0a600-3b70-11ea-8d32-022d0c6a8576.png)

(2020-01-20)

일단 모듈 기술서만으로 디버깅을 했을 때 잘 수행되어 바로 구현으로 들어갔다.
코드는 아래와 같이 작성하였다.

{% highlight c %}
//4_onlyminusEven.c
/**************************************************************************
 * 파일   명칭 : 4_onlyminusEven.c
 * 기       능 : 1-2+3-4+...+99-100를 계산한다.
 * 함수   명칭 : main
 * 출       력 : 총합
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/01/20
**************************************************************************/
#include <stdio.h>

#define MAX 100
#define DIVIDER 2

int main(int argc, char* argv[]) {

	unsigned long sum = 0;
	unsigned long remainder = 0;
	unsigned long number = 1;

    //2. 수가 MAX보다 작거나 같을 때까지 반복한다.
    while(number <= MAX){
        //2.1. 짝수를 판별한다.
        remainder=number%DIVIDER;
        if(remainder==0){
            //2.1.1. 짝수이면 합을 뺀다.
            sum-=number;
        }else{
            //2.1.2. 짝수가 아니면 합을 더한다.
            sum+=number;
        }
        //1. 수를 증가한다.
        number++;
    }
    //3. 합을 출력한다.
    printf("1부터 %d까지의 합 : %d", sum);
    //4. 끝낸다.
	return 0;
}
{% endhighlight }

### 문제 5

![9장_내부 설계(모듈 기술서) 양식 문제 5](https://user-images.githubusercontent.com/25213941/72692576-01c0a600-3b70-11ea-9c42-603e48241ad8.png)

(2020-01-20)

![9장_내부 설계(모듈 기술서) 양식 문제 6](https://user-images.githubusercontent.com/25213941/72692593-1309b280-3b70-11ea-9080-624d99169201.png)
![9장_내부 설계(모듈 기술서) 양식 문제 7](https://user-images.githubusercontent.com/25213941/72692594-13a24900-3b70-11ea-9b53-26b689e92426.png)

![9장_내부 설계(모듈 기술서) 양식 문제 8](https://user-images.githubusercontent.com/25213941/72692592-1309b280-3b70-11ea-9ee1-b641f63f1285.png)

