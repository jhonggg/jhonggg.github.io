---
layout: post
title: "[나프잘 프로그래밍 입문] p59 문제 풀이"
excerpt: "나프잘 C & JAVA 프로그래밍 입문 문제 풀이"
modified: 2020-01-11
tags: [나프잘 프로그래밍 입문]
categories: "나프잘프로그래밍(입문)"
comments: true
pinned: true
image:
  feature: feature_for_nafzal.jpg
---

## 문제

> 1. 수학 점수를 입력받아서 성적을 평가하도록 고쳐 보세요.
> 2. 평균이 60점 미만이연 'F', 60점 이상 70점 미만이면 'D', 70점 이상이고 80점 미만이면 'C', 80점 이상이고 90점 미만이면 'B' 그리고 90점 이상이면 'A' 학점을 줄 수 있도록 고쳐 보세요.

### 내가 생각한 답

![p59](https://user-images.githubusercontent.com/25213941/72202402-60b45a00-34a2-11ea-9200-89b54277b461.png)


### 모범 답안

>1. 준비기호에서 기호상수 SUBJECTCOUNT = 3.0으로 고치기 : 과목개수가 세개이므로
>2. 준비기호에 mathematicsScore 변수 선언하기 : 수학점수를 저장할 변수
>3. 입력기호에 mathematicsScore 변수 추가하기
>4. 합을 구하는 처리기호에서 sum = koreanScore + englishScore + mathematicsScore

![p59_Solution](https://user-images.githubusercontent.com/25213941/72202405-6f027600-34a2-11ea-8fdc-5e3436273bed.PNG)