---
layout: post
title:  "[MySQL] SELECT"
subtitle:   "프로그래머스-SELECT"
categories: dev
tags: db select
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
```SQL
SELECT 필드명 
FROM 테이블명
WHERE 조건
ORDER BY 정렬할 필드명 ASC/DESC
LIMIT 표시할 상위 레코드 수
```
<br/>

## 문제 예시
---


### 1. 동물 보호소에 가장 먼저 들어온 동물의 이름을 조회

```SQL
SELECT NAME FROM ANIMAL_INS
ORDER BY DATETIME ASC
LIMIT 1
```