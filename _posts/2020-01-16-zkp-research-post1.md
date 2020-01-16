---
layout: post
title: "[Research] Introducing Sonic: A Practical zk-SNARK with a Nearly Trustless Setup 해석본"
excerpt: "Sonic: A Practical zk-SNARK 해석본"
modified: 2020-01-16
tags: ["Zero-Knowldge-Proof", "영지식 증명", "Sonic", "zkSNRK"]
comments: true
pinned: true
categories: "Zero-Knowledge-Proof Research"
image:
  feature: feature_for_nafzal.jpg
---

# 들어가기 전
해당 포스트는 [link](https://www.benthamsgaze.org/2019/02/07/introducing-sonic-a-practical-zk-snark-with-a-nearly-trustless-setup/)를 해석하고 안에 있는 부록들을 연구한 내용입니다. 참고 바랍니다.

# 믿을 수 없는 구조를 가진 실용적인 zk-SNARK Sonic 소개

 해당 포스트는 Mary Maller, Sean Bowe, Markulf Kohlwess 그리고 Sarah Meiklejohn이 만든 [새로운 zk-SNARK인 sonic](https://eprint.iacr.org/2019/099)에 대해 의논하고자 한다. 다른 SNARKs와 달리 Sonic은 각 circuit에 대한 신뢰된 구조이 필요한 것이 아니라 모든 회로에 대해 단일 구조만 요구한다. 또한, Sonic에 대한 설정은 절대 끝날 일이 없고, 이는 더 많은 기여를 축적하고 지속적으로 확보할 수 있다.

 이러한 특성은 신뢰할 수 있는 당사자가 없거나 기밀 정보를 누설하지 않고 데이터를 검증할 필요가 있는 모든 시스템에 이상적으로 만든다. 이 구조는 매우 실용적이다.

 ## More and zk-SNARKs

 zk-SNARKs는 다른 모든 [영지식 증명](https://blog.cryptographyengineering.com/2014/11/27/zero-knowledge-proofs-illustrated-primer/)과 마찬가지로 사용자가 검증 가능한 계산 또는 익명 인증과 같이 데이터의 유효성을 입증해야 하는 애플리케이션을 구축하는데 사용되는 도구다. 또한, zk-SNARKs는 영지식 증명 구축에 대해 알려진 모든 기술 중 가장 작은 입증 크기와 검증 시간을 갖는다. 단, 일반적으로 시스템을 구현한 행위자에 의해 부정 데이터가 입력될 가능성을 도입하여 신뢰할 수 있는 구조 프로세스를 요구한다. 예를 들어, Zcash는 개인 소유의 암호화폐 트랜잭션을 전송하기 위해 zk-SNARKs를 사용한다. 만약 그들의 구조가 손상됬다면, 소수의 사용자들은 적발없이 무제한의 통화 공급을 생성할 수 있다.

>### zk-SNARKs의 특성

>😊 많은 암호화 프로토콜 구축에 사용할 수 있음
>😊 입증 크기가 매우 작음
>😊 검증이 매우 빠름
>😊 증명 시간이 평균적임
>😕 신뢰된 구조가 필요
>😕 보안은 비표준 암호화인거 같음

2018년도, [Groth 외 연구진](https://eprint.iacr.org/2018/280)들은 Updateability 하고 보편적인 구조를 구축할 수 있는 zk-SNARK를 선보였다. 아래에서는 이러한 속성들을 설명하고 속성들이 신뢰할 수 있는 구조 주위의 보안 문제를 완화하는데 도움이 된다고 주장한다.

## Updateability

Updateability이란 시스템이 가동된 후를 포하여 모든 사용자가 언제든지 파라미터를 업데이트 할 수 있다는 것을 의미한다. 정직한 사용자 한 명이 참여한 후에는 어떤 당사자도 부정 데이터를 입증할 수 없다. 이러한 특성은 신뢰할 수 없는 사용자가 파라미터 자체를 업테이트할 수 있고 해당 지점부터 매개변수에 대한 개인 신뢰도를 가질 수 있다는 것을 의미한다. 해당 업데이트된 증명은 짧고 검증이 빠르다.

![pic 1, Updatability](https://www.benthamsgaze.org/wp-content/uploads/2019/02/updatable.png)

## Universality

Universality는 같은 파라미터들을 zk-SNARK를 사용한 모든 용도에서 사용할 수 있다는 의미한다. 따라서 오픈 소스 구현에 글로벌 파라미터를 포함하거나 Ethereum의 모든 Smart Contract에 동일한 파라미터를 사용할 수 있다고 상상할 수 있다.

![pic 2, Universality](https://www.benthamsgaze.org/wp-content/uploads/2019/02/universal.png)

# 왜 Sonic을 사용하는가?

Sonic은 보편적이고, 업데이트 가능하며 작은 글로벌 파라미터 집합(MB 순서)이다. 증명 크기들은 작고(256bytes) 검증 시간은 문서 상에서 가장 빠른 zk-SNARK와 경쟁적이다. 그것은 특히 동일한 zk-SNARK가 다수의 다른 증명자들에 의해 운영되고 다수의 다른 당사자들에 의해 검증되는 시스템에 적합하다. 이것은 정확히 다수 블록체인들의 상황이다.

[Groth 외 연구진들의 설계](https://eprint.iacr.org/2018/280)에 비해 Sonic의 장점은 더 작은 글로벌 파라미터 집합들을 사용한다는 것이다. 그 결과, 소닉의 파라미터를 개인용 노트북에서 저장, 업데이트 및 검증할 수 있었다. 그런데 Groth 외 연구진들이 공개한 파라미터들은 이러한 작업을 수행하기 위해 분산된 컴퓨터 세트가 필요할 정도로 저장, 업데이트 및 검증하는 데 비용이 많이 든다. 또한, Groth 외 연구질들의 zk-SNARK를 특정 용도과 함께 사용하기 위해 일부 당사자는 용도 별 파라미터를 얻기 위해 값비싼(신뢰할 수도 없는) 파생 프로세스를 글로벌 파라미터에 실행해야 한다. Sonic은 어떤 파생 과정도 요구하지 않는다.

Bulletproofs([Bootle 외 연구진들](https://eprint.iacr.org/2016/263)에 의해 도입되고 [Bünz 외 연구진들](https://eprint.iacr.org/2017/1066)에 의해 개선됨)에 비해 Sonic은 증명 크기가 더 작고 검증 연산도 훨씬 더 작다. Bulletproof 검증은 기초 용도의 크기에 따라 크기가 달라지는 계산을 요구한다. 반면에 Sonic은 어떤 용도에 대해서도 일정한 크기의 검증기를 가지고 있다. Bulltetproofs는 완전히 신뢰할 수 있는 구조인 반면 Sonic은 덜 신뢰적인 구조이다. 또한, Bulletproofs은 Sonic보다 더 표준적인 가정에 근거하여 보안을 강화한다. 전체적으로 Bulletproofs는 작은 용도에서 좋고 Sonic은 큰 용도에서 더 좋다.

Sonic은 zk-STARKs에 서로 다른 용도에 사용된다. STARKs는 postquantum 보안을 가능하게 하고 완전히 신뢰할 수 있는 구조지만 오버헤드가 높다. 크기가 작은 용도의 경우에도 현재 STARK 증명 크기는 최소 40KB이다. 이러한 특성은 STARK가 일회성 비용으로 실행되는 용도에 더 적합하며 동일한 프로그램에 대한 복수의 증명서가 실행, 저장 및 검증되는 용도에는 덜 적합하다.