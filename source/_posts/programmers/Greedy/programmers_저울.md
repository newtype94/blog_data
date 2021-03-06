---
title: programmers 저울
date: 2020-03-06 17:31:13
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 고득점 Kit
  - 탐욕법(Greedy)
---

[문제 링크](https://programmers.co.kr/learn/courses/30/lessons/42886)

# 분류 / 레벨 / 언어

탐욕법(Greedy) / LV.3 / Javscript

# 설명

## 공간 복잡도 절약

문제의 요구사항은
주어진 추들을 다양하게 합산해도 도저히 만들 수 없는
무게들 중 최소값을 찾는 것이다.

운이 좋게도, 무게들은 모두 양의 정수이다.
양의 정수는 1부터 시작해서 간격이 1이다.
또한 이 세상의 모든 Array는 index가 0부터 시작해서 간격이 1이다.

추의 조합으로 나올 수 있는 양의 정수들을 배열로 만들고
배열의 앞에 0를 임의로 넣는다면
문제에서 원하는 임계점까지는 index와 value가 완전히 일치하게 된다.

따라서 배열을 메모리에 할당하지 않고
가상으로 배열이 있다고 생각하며 풀 수 있다.

구체적으로 말하면
최종적으로 체크 완료한 index(= 무게 합)을 let 변수로 두고 풀 것이다.

## Greedy 적용

앞서 말한 가상의 배열은 일단 논외로 하고 Greedy를 생각해보자.

중간 지점의 예를 들면

1. 기존의 합산 list [0,1,2,3,4,5,6]
2. 무게 5의 추를 가지고 합산 list를 늘려보자!!
3. [0,1,2,3,4,5,6] + [5,6,7,8,9,10,11]
4. 새로운 합산 list [0,1,2,3,4,5,6,7,8,9,10,11,12,13]

끝나는 지점의 예를 들면

1. 기존의 합산 list [0,1,2,3,4,5,6]
2. 무게 8의 추를 가지고 합산 list를 늘려보자??
3. [0,1,2,3,4,5,6] + [8,9,10,11,12,13,14] ??
4. 7을 커버할 수 없다.

따라서 sorted weights에서 한개씩 꺼내다가,
기존 합산 list의 마지막 값보다 새로운 추의 무게가 더 크면 break 해야한다.

## 시간 복잡도 절약

앞서 설명한 Greedy 알고리즘에서 불필요한 연산은 제거해야 한다.

1. 중복되는 값을 제거하기 위해 set 사용 => 시간 초과 발생
2. array[last_index] 보다 큰 값만 push하는 방식 => 역시나 시간 초과 발생
3. array를 운용하지 않고 최후의 값만 고려하는 방식 => 성공!!

# 전체 코드

```javascript
function solution(weights) {
  weights.sort((a, b) => a - b);

  let checked = 0;

  for (let choo of weights) {
    if (choo > checked + 1) break;
    else checked += choo;
  }
  return checked + 1;
}
```
