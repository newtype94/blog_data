---
title: programmers sql STRING, DATE
date: 2020-05-27 21:33:14
tags:
  - 알고리즘
  - 프로그래머스
category:
  - 프로그래머스 sql Kit
---

[문제 링크](https://programmers.co.kr/learn/courses/30/parts/17047)

# 루시와 엘라 찾기

```sql
SELECT ANIMAL_ID, NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
WHERE NAME IN ("Lucy", "Ella", "Pickle", "Rogan", "Sabrina", "Mitty")
ORDER BY ANIMAL_ID
```

# 이름에 el이 들어가는 동물 찾기

```sql
SELECT ANIMAL_ID, NAME
FROM ANIMAL_INS
WHERE ANIMAL_TYPE = "Dog" AND NAME LIKE "%el%"
ORDER BY NAME
```

# 중성화 여부 파악하기

```sql
SELECT ANIMAL_ID, NAME,
  CASE
    WHEN SEX_UPON_INTAKE LIKE "Neutered%"
      OR SEX_UPON_INTAKE LIKE "Spayed%"
    THEN "O"
    ELSE "X"
  END AS 중성화
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```

# 오랜 기간 보호한 동물(2)

```sql
SELECT A.ANIMAL_ID, A.NAME
FROM ANIMAL_INS A RIGHT JOIN ANIMAL_OUTS B ON A.ANIMAL_ID = B.ANIMAL_ID
ORDER BY B.DATETIME - A.DATETIME DESC
LIMIT 2
```

# DATETIME에서 DATE로 형 변환

```sql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, "%Y-%m-%d") AS 날짜
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```
