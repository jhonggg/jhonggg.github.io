---
layout: post
title: "[Algorithm] Selection Sort, Bubble Sort, Insertion Sort, Quick Sort"
excerpt: "algorithm basic"
modified: 2020-02-04
tags: ["algorithm basic"]
comments: true
pinned: true
categories: "algorithm"
image:
feature: 
---

# 선택정렬(Selection Sort)
{% highlight c %}
//1_selectionSort.c
/**************************************************************************
 * 파일   명칭 : 1_selectionSort.c
 * 기       능 : 10개의 숫자를 선택정렬한다.
 *               (선택정렬 : 가장 작은 값을 선택해서 앞으로 보내는 정렬 방식)
 * 함수   명칭 : main
 * 출       력 : 10개의 숫자
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/02/03
**************************************************************************/
#include <stdio.h>

#define MAX 10
#define SWAP(a, b, temp) ((temp)=(a), (a)=(b), (b)=(temp))

void Arrage(int(*numbers));
void Output(int(*numbers));

int main(int argv, char* argc[]) {
    //1. 수를 입력한다.
	int numbers[MAX] = {1,10,5,8,7,6,4,3,2,9};
    //2. 수를 정렬한다.
	Arrage(numbers);
    //3. 수를 출력한다.
	Output(numbers);
	return 0;
}

void Arrage(int(*numbers)) {

	int temp;
	int index;
	for (int i = 0; i < MAX; i++) {
		min = 9999;
		for (int j = i; j < MAX; j++) {
			if (min > numbers[j]) {
				min = numbers[j];
				index = j;	
			}
		}
		SWAP(numbers[i], numbers[index], temp);
	}
}

void Output(int(*numbers)) {
	for (int i = 0; i < MAX; i++) {
		printf("%d ", numbers[i]);
	}
	printf("\n");
}
{% endhighlight %}

# 버블정렬(Bubble Sort)
{% highlight c %}
//2_bubbleSort.c
/**************************************************************************
 * 파일   명칭 : 2_bubbleSort.c
 * 기       능 : 10개의 숫자를 버블정렬한다.
 *               (버블정렬 : 우측값과 비교하며 정렬하는 방식)
 * 함수   명칭 : main
 * 출       력 : 10개의 숫자
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/02/03
**************************************************************************/
#include <stdio.h>

#define MAX 10
#define SWAP(a, b, temp) ((temp)=(a)),((a)=(b)),((b)=(temp))
void bubbleSort(int(*numbers));
void output(int(*numbers));

int main(int argc, char* argv[]) {

	int numbers[MAX] = { 1,10,5,8,7,6,4,3,2,9 };
	bubbleSort(numbers);
	output(numbers);

	return 0;
}

void bubbleSort(int(*numbers)) {

	int temp = 0;
	int j = 0;
	for (int i = 0; i < MAX; i++) {
		for (int j = 0; j < (MAX - 1) - i; j++) {
			if (numbers[j] > numbers[j+1]) {
				SWAP(numbers[j], numbers[j+1], temp);
			}
			printf("\n");
		}
	}
}
void output(int(*numbers)) {
	for (int i = 0; i < MAX; i++) {
		printf("%d ", numbers[i]);
	}
	printf("\n");
}
{% endhighlight %}

# 삽입정렬(Insertion Sort)
{% highlight c %}
//3_insertionSort.c
/**************************************************************************
 * 파일   명칭 : 3_insertionSort.c
 * 기       능 : 10개의 숫자를 삽입정렬한다.
 *               (삽입정렬 : 우측 숫자와 비교하여 정렬하지만 이미 탐색한 곳은
 *                정렬이 되있음을 가정함)
 * 함수   명칭 : main
 * 출       력 : 10개의 숫자
 * 입       력 : 없음
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/02/03
**************************************************************************/
#include <stdio.h>

#define MAX 10
#define SWAP(a, b, temp) ((temp)=(a)),((a)=(b)),((b)=(temp))
void insertionSort(int(*numbers));
void output(int(*numbers));

int main(int argc, char* argv[]) {

	int numbers[MAX] = { 1,10,5,8,7,6,4,3,2,9 };
	insertionSort(numbers);
	output(numbers);

	return 0;
}

void insertionSort(int(*numbers)) {
    int j = 0;
	int temp = 0;
	for (int i = 0; i < MAX-1; i++) {
        j = i;
        while(numbers[j] > numbers[j+1]){
            SWAP(numbers[j], numbers[j+1], temp);
            j--;
        }
	}
}
void output(int(*numbers)) {
	for (int i = 0; i < MAX; i++) {
		printf("%d ", numbers[i]);
	}
	printf("\n");
}
{% endhighlight %}

# 퀵 정렬(Quick Sort)
{% highlight c %}
//5_2_quickSort.c
/**************************************************************************
 * 파일   명칭 : 5_2_quickSort.c
 * 기       능 : N개의 수가 주어졌을 때, 이를 오름차순으로 정렬는 프로그램
 * 함수   명칭 : main
 * 출       력 : N개의 숫자
 * 입       력 : 행렬크기, 크기에 따른 원소
 * 작   성  자 : 채 종 홍
 * 작성   일자 : 2020/02/03
**************************************************************************/
/*
백준 온라인
https://www.acmicpc.net/problem/2750

* 입력

첫째 줄에 수의 개수 N(1 ≤ N ≤ 1,000)이 주어진다. 
둘째 줄부터 N개의 줄에는 숫자가 주어진다. 
이 수는 절댓값이 1,000보다 작거나 같은 정수이다. 
수는 중복되지 않는다.

* 출력
첫째 줄부터 N개의 줄에 오름차순으로 정렬한 결과를 
한 줄에 하나씩 출력한다.

*/
#include <stdio.h>

#define MAX 1000000
#define SWAP(a,b,temp) ((temp)=(a)),((a)=(b)),((b)=(temp))

void input(int(*numbers), int size);
void quickSort(int(*numbers), int size, int start, int end);
void output(int(*numbers), int size);

int main(int argc, char* argv[]) {

	int(*numbers);
	int size = 0;
	int start = 0;
	scanf("%d", &size);
    
	int end = size - 1;
	numbers = (int*)malloc(sizeof(int) * size);
	input(numbers, size);

	quickSort(numbers, size, start, end);
	output(numbers, size);

	free(numbers);
	return 0;
}

void input(int(*numbers), int size) {
    scanf("%d", numbers + i);
    /*
	for (int i = 0; i < size; i++) {
		while (1) {
			scanf("%d", numbers + i);
			if (numbers[i] >= 1 && numbers[i] <= MAX) {
				break;
			}
		}
	}
    */
}
void quickSort(int(*numbers), int size, int start, int end) {
	
	if (start >= end) {
		return;
	}

	int key = start;
	int low = start + 1;
	int high = end;
	int temp;

	while (low <= high) {
		while (numbers[low] <= numbers[key]) {
			low++;
		}
		while (numbers[high] >= numbers[key] && high > start) {
			high--;
		}

		if (low > high) {
			SWAP(numbers[high], numbers[key], temp);
		}
		else {
			SWAP(numbers[low], numbers[high], temp);
		}
	}
	quickSort(numbers, size, start, high - 1);
	quickSort(numbers, size, high + 1, end);
}
void output(int(*numbers), int size) {
	for (int i = 0; i < size; i++) {
		printf("%d\n", numbers[i]);
	}
}
{% endhighlight %}
