---
layout: post
title:  "[MySQL] SUM, MAX, MIN"
subtitle:   "프로그래머스-SUM, MAX, MIN"
categories: dev
tags: db MySQL
comments: true
---

> `MySQL`을 기준으로 SQL 기본 문법을 정리하고, <br/>
`프로그래머스`의 문제를 바탕으로 활용해보는 연재.
{:.note}

* this ordered seed list will be replaced by the toc
{:toc .large-only}

## 기본 문법 

### 1. SUM 함수
- 테이블에서 해당 필드의 합계
```sql
SELECT SUM(필드명) 
FROM 테이블명
```

### 2. MAX 함수
- 테이블에서 해당 필드의 최댓값
```sql
SELECT MAX(필드명) 
FROM 테이블명
```

### 3. MIN 함수
- 테이블에서 해당 필드의 최솟값
```sql
SELECT MIN(필드명) 
FROM 테이블명
```

### 4. COUNT 함수
- 테이블에서 해당 필드의 갯수
- `COUNT(필드명)` : NULL 값은 제외하고 COUNT
- `COUNT(*)` : NULL도 포함하여 전부 COUNT

```sql
SELECT COUNT(필드명) 
FROM 테이블명
WHERE 조건
```

### 5. AVG 함수
- 테이블에서 해당 필드의 평균값
```sql
SELECT AVG(필드명) 
FROM 테이블명
```

## 문제 예시
---

**1. 동물 보호소에 가장 먼저 들어온 동물은 언제 들어왔는지 조회**

```sql
SELECT MIN(DATETIME)
FROM ANIMAL_INS
```

**2. 동물 보호소에 들어온 동물의 이름은 몇 개인지 조회. <br/>이때 이름이 NULL인 경우는 집계하지 않으며 중복되는 이름은 하나로 칩니다.**

```sql
SELECT COUNT(DISTINCT(NAME))
FROM ANIMAL_INS
```

- `DISTINCT 함수` : 중복을 제거한 열의 갯수를 반환