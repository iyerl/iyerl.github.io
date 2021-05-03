---
layout: post
title:  "[MySQL] IS NULL, IS NOT NULL"
subtitle:   "프로그래머스-IS NULL, IS NOT NULL"
categories: dev
tags: db MySQL
description : >
    MySQL, null 판별 함수, 프로그래머스
---

> `MySQL`을 기준으로 SQL 기본 문법을 정리하고, <br/>
`프로그래머스`의 문제를 바탕으로 활용해보는 연재.
{:.note}

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc .large-only}

## 기본 문법 

### 1. IS NULL 함수
- 값이 null이면 True를 반환

### 2. IS NOT NULL 함수
- 값이 null이 아니면 True를 반환

## 문제 예시
---

**1. 동물 보호소에 들어온 동물 중, 이름이 있는 동물의 ID를 조회하는 SQL 문을 작성해주세요. 단, ID는 오름차순 정렬되어야 합니다.**

```sql
SELECT ANIMAL_ID
FROM ANIMAL_INS
WHERE NAME IS NOT NULL
ORDER BY ANIMAL_ID ASC
```

**2. 동물의 생물 종, 이름, 성별 및 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 프로그래밍을 모르는 사람들은 NULL이라는 기호를 모르기 때문에, 이름이 없는 동물의 이름은 No name으로 표시해 주세요.**

```sql
SELECT ANIMAL_TYPE, IFNULL(NAME, 'No name') AS NAME, SEX_UPON_INTAKE
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```