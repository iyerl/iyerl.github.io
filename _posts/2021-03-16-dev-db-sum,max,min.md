---
layout: post
title:  "[MySQL] SUM, MAX, MIN"
subtitle:   "프로그래머스-SUM, MAX, MIN"
categories: dev
tags: db sum max min count avg
comments: true
---
## SERIES
> `MySQL`을 기준으로 SQL 기본 문법을 정리하고, <br/>
`프로그래머스`의 문제를 바탕으로 활용해보는 연재.

<br/>

- 목차
  - [SELECT문](./2021-03-15-dev-db-select.md)
  - [SUM, MAX, MIN 집계 함수](./2021-03-16-dev-db-sum,max,min.md)
<br/>

---
## 기본 문법 
<br/>

### SUM 함수
- 테이블에서 해당 필드의 합계
```SQL
SELECT SUM(필드명) 
FROM 테이블명
```
<br/>

### MAX 함수
- 테이블에서 해당 필드의 최댓값
```SQL
SELECT MAX(필드명) 
FROM 테이블명
```
<br/>

### MIN 함수
- 테이블에서 해당 필드의 최솟값
```SQL
SELECT MIN(필드명) 
FROM 테이블명
```
<br/>

### COUNT 함수
- 테이블에서 해당 필드의 갯수
- `COUNT(필드명)` : NULL 값은 제외하고 COUNT
- `COUNT(*)` : NULL도 포함하여 전부 COUNT

```SQL
SELECT COUNT(필드명) 
FROM 테이블명
WHERE 조건
```
<br/>

### AVG 함수
- 테이블에서 해당 필드의 평균값
```SQL
SELECT AVG(필드명) 
FROM 테이블명
```
<br/>

## 문제 예시
---

### 1. 동물 보호소에 가장 먼저 들어온 동물은 언제 들어왔는지 조회

```SQL
SELECT MIN(DATETIME)
FROM ANIMAL_INS
```

### 2. 동물 보호소에 들어온 동물의 이름은 몇 개인지 조회. <br/>이때 이름이 NULL인 경우는 집계하지 않으며 중복되는 이름은 하나로 칩니다.

```SQL
SELECT COUNT(DISTINCT(NAME))
FROM ANIMAL_INS
```

- `DISTINCT 함수` : 중복을 제거한 열의 갯수를 반환