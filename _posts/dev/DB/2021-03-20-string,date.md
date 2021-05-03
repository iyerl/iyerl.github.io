---
layout: post
title:  "[MySQL] STRING, DATE"
subtitle:   "프로그래머스- STRING, DATE"
categories: dev
tags: db MySQL
description : >
    MySQL, 문자열/날짜 함수, 프로그래머스
---

> `MySQL`을 기준으로 SQL 기본 문법을 정리하고, <br/>
`프로그래머스`의 문제를 바탕으로 활용해보는 연재.
{:.note}

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc .large-only}

## 기본 문법 

### 1. LIKE 연산자
- 값들 중 특장 문자가 포함된 값을 조회
- `%AA%` : AA가 포함된 값을 조회
- `%A` : 맨 뒷자리가 A로 끝나는 값 조회
- `A%` : 맨 앞자리가 A로 시작하는 값 조회
    
```sql
SELECT *
FROM 테이블명
WHERE 값 LIKE 'ANNE%'
```

### 2. 논리합(AND, OR, NOT, IN) 연산자
- `AND` : 조건을 모두 충족하는 조건
- `OR` : 조건을 하나 이상 충족하는 조건
- `NOT` : 해당 요소가 아닌 조건 검색
- `IN` : IN 괄호 안의 요소와 일치하는 조건 검색
- 주로 WHERE 조건절과 함께 사용
  
```sql
SELECT *
FROM 테이블명
WHERE 조건1 IN (요소1, 요소2, ...) AND 조건2 = 'ASC'
```

### 3. EXISTS 연산자
- 쿼리에 대한 결과가 존재하면 True 반환
    
```sql
SELECT *
FROM 테이블명
WHERE EXISTS (서브 쿼리)
```

### 4. 날짜 관련 함수
- `dayofweek(date)` : 날짜를 한 주의 몇 번째 요일인지를 나타내는 숫자로 반환
- `weekday(date)` : 날짜를 한 주의 몇 번째 요일인지를 나타내는 숫자로 반환 (0 = 월요일, 1=화요일 ... 6 = 일요일)
- `DATEDIFF(가장 최근 날짜, 날짜2)` : 날짜 차이 계산
- `date_format(date,format)` : format대로 date를 출력
  
```sql
SELECT DATE_FORMAT(DATETIME, '%H')
FROM 테이블명
```

## 문제 예시
---

**1. 중성화된 동물은 SEX_UPON_INTAKE 컬럼에 'Neutered' 또는 'Spayed'라는 단어가 들어있습니다. 동물의 아이디와 이름, 중성화 여부를 아이디 순으로 조회하는 SQL문을 작성해주세요. 이때 중성화가 되어있다면 'O', 아니라면 'X'라고 표시해주세요.**

```sql
SELECT ANIMAL_ID, NAME, IF(SEX_UPON_INTAKE LIKE 'Neutered%' OR SEX_UPON_INTAKE LIKE 'Spayed%', 'O', 'X')
FROM ANIMAL_INS
```

**2. 입양을 간 동물 중, 보호 기간이 가장 길었던 동물 두 마리의 아이디와 이름을 조회하는 SQL문을 작성해주세요. 이때 결과는 보호 기간이 긴 순으로 조회해야 합니다.**

```sql
SELECT ANIMAL_OUTS.ANIMAL_ID, ANIMAL_OUTS.NAME
FROM ANIMAL_INS
INNER JOIN ANIMAL_OUTS
ON ANIMAL_INS.ANIMAL_ID = ANIMAL_OUTS.ANIMAL_ID
ORDER BY DATEDIFF(ANIMAL_OUTS.DATETIME, ANIMAL_INS.DATETIME) DESC
LIMIT 2
```
  
**3. 테이블에 등록된 모든 레코드에 대해, 각 동물의 아이디와 이름, 들어온 날짜(시각(시-분-초)을 제외한 날짜(년-월-일)만 보여주세요)를 조회하는 SQL문을 작성해주세요. 이때 결과는 아이디 순으로 조회해야 합니다.**

```sql
SELECT ANIMAL_ID, NAME, DATE_FORMAT(DATETIME, '%Y-%m-%d') AS '날짜'
FROM ANIMAL_INS
ORDER BY ANIMAL_ID
```