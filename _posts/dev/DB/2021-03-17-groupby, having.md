---
layout: post
title:  "[MySQL] GROUP BY, HAVING"
subtitle:   "프로그래머스-GROUP BY, HAVING"
categories: dev
tags: db MySQL
description : >
    MySQL, 조건절 함수, 프로그래머스
---

> `MySQL`을 기준으로 SQL 기본 문법을 정리하고, <br/>
`프로그래머스`의 문제를 바탕으로 활용해보는 연재.
{:.note}

<!--more-->

* this unordered seed list will be replaced by the toc
{:toc .large-only}

## 기본 문법 

### 1. GROUP BY 함수
- 데이터를 그룹화할 필드 지정
- 주로 집계 함수 및 조건절과 함께 사용 
```sql
SELECT 필드명
FROM 테이블명
GROUP BY 필드명
```

### 2. HAVING 함수
- WHERE절에서는 집계함수를 사용할 수 없기 때문에, 그룹화된 필드의 집계를 가지고 조건 비교를 할 때 사용
```sql
SELECT 필드명 
FROM 테이블명
GROUP BY 필드명
HAVING 집계 함수 조건
```

## 문제 예시
---

**1. 동물 보호소에 들어온 동물 이름 중 두 번 이상 쓰인 이름과 해당 이름이 쓰인 횟수를 조회하는 SQL문을 작성해주세요. 이때 결과는 이름이 없는 동물은 집계에서 제외하며, 결과는 이름 순으로 조회해주세요.**

```sql
SELECT NAME, COUNT(NAME) AS COUNT
FROM ANIMAL_INS
GROUP BY NAME
HAVING COUNT(NAME) >= 2
ORDER BY NAME ASC
```

**2. 우유와 요거트를 동시에 구입한 장바구니의 아이디를 조회하는 SQL 문을 작성해주세요. 이때 결과는 장바구니의 아이디 순으로 나와야 합니다.**

```sql
WITH ID AS
(SELECT DISTINCT CART_ID, NAME FROM CART_PRODUCTS WHERE NAME = 'Yogurt' OR NAME = 'Milk')
SELECT CART_ID
FROM ID
GROUP BY CART_ID
HAVING COUNT(CART_ID) = 2
```

- `임시 테이블` : `WITH 임시 테이블 이름 AS (쿼리)`
- `DISTINCT 함수`
  - `DISTINCT(COLUMN) | DISTINCT(FIELD1, FIELD2, ...)`
  - 중복되는 데이터 제거를 위해 주로 UNIQUE한 Column이나 Tuple(Record)을 조회하는 경우에 사용
  - SELECT절에 DISTINCT라는 키워드가 있으면, MySQL은 SELECT되는 모든 Column(Tuple)들에 대해서 DISTINCT를 적용해서 결과를 출력

**3. 동물 보호소에 들어온 동물 중 고양이와 개가 각각 몇 마리인지 조회하는 SQL문을 작성해주세요. 이때 고양이를 개보다 먼저 조회해주세요.**

```sql
SELECT ANIMAL_TYPE, COUNT(ANIMAL_ID)
FROM ANIMAL_INS
WHERE ANIMAL_TYPE IN ('Cat','Dog')
GROUP BY ANIMAL_TYPE
ORDER BY FIELD(ANIMAL_TYPE, 'Cat', 'Dog')
```

- `ORDER BY FIELD(컬럼명, ‘1번째 정렬값’, ‘2번째 정렬값’, ...)` : 특정한 값을 우선적으로 정렬
  
**4. 'BTC'가 첫번째, 'ETH'가 두번째, 그외 나머지는 오름차순으로 정렬**

```sql
SELECT COIN_CD
FROM COIN
ORDER BY FIELD(COIN_CD, 'ETH', 'BTC') DESC, COIN_CD ASC
```

- `FIELD 함수` : 첫번째 파라미터의 값과 같은 값이 그 이후 파라미터의 몇번째에 있는지 index값을 반환('ETH'는 1, 'BTC'는 2, 같은 값이 없는 나머지는 0)
- 일반적인 ORDER BY 정렬은 index가 0인 파라미터를 대상으로 함

**5. 09:00부터 19:59까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.**

```sql
SELECT DATE_FORMAT(DATETIME, '%H') AS HOUR, COUNT(*)
FROM ANIMAL_OUTS
GROUP BY HOUR
HAVING HOUR >= 9 AND HOUR <= 19
ORDER BY HOUR
```

- date_format(DATETIME, '%h:%m:%s') : 날짜, 시간 표기 방식 지정
    - %a : Abbreviated weekday name (Sun..Sat)
        -%b : Abbreviated month name (Jan..Dec)
    - %c : Month, numeric (0..12)
    - %D : Day of the month with English suffix (0th, 1st, 2nd, 3rd, …)
    - %d : Day of the month, numeric (00..31)
    - %e : Day of the month, numeric (0..31)
    - %H : Hour (00..23)
    - %h : Hour (01..12)
    - %i : Minutes, numeric (00..59)
    - %j : Day of year (001..366)
    - %w : Day of the week (0=Sunday..6=Saturday)
    - %M : Month name (January..December)
    - %m : Month, numeric (00..12)
    - %p : AM or PM
    - %r : Time, 12-hour (hh:mm:ss followed by AM or PM)
    - %S : Seconds (00..59)
    - %T : Time, 24-hour (hh:mm:ss)
    - %W : Weekday name (Sunday..Saturday)

**6. 0시부터 23시까지, 각 시간대별로 입양이 몇 건이나 발생했는지 조회하는 SQL문을 작성해주세요. 이때 결과는 시간대 순으로 정렬해야 합니다.**

```sql
WITH RECURSIVE TIME AS
(
    SELECT 0 AS HOUR
    UNION ALL
    SELECT HOUR+1
    FROM TIME
    WHERE HOUR < 23
)
SELECT TIME.HOUR, COUNT(DATA.HOUR) FROM TIME
LEFT JOIN 
(SELECT DATE_FORMAT(DATETIME, '%H') AS HOUR FROM ANIMAL_OUTS) AS DATA
ON TIME.HOUR = DATA.HOUR
GROUP BY TIME.HOUR
ORDER BY TIME.HOUR ASC
```

- 1~999까지의 리스트 데이터 생성을 위한 재귀 `WITH RECURSIVE 임시테이블명 AS (쿼리)` : WITH RECURSIVE rgen AS (SELECT 1 UNION ALL SELECT n+1 FROM rgen WHERE n < 1000) SELECT * FROM rgen;
- `DAYOFWEEK(date)` : 해당 날짜의 요일을 숫자로 반환한다. 일요일은 1, 토요일은 7
- `WEEKDAY(date)` : 해당 날짜에 대한 요일을 반환한다. 월요일은 0, 일요일은 6
- `DAYOFYEAR(date)` : 해당 날짜의 1월 1일부터의 날수를 반환한다. 결과값은 1에서 366
- YEAR(date) : 해당 날짜의 년을 반환
- MONTH(date) : 해당 날짜의 월을 반환
- `DAYOFMONTH(date)` : 해당 날짜의 일을 반환한다. 결과값은 1 에서 31
- `HOUR(time)` : 해당날짜의 시간을 반환한다. 결과값은 0 에서 23
- `MINUTE(time)` : 해당날짜의 분을 반환한다. 결과값은 0 에서 59
- `SECOND(time)` : 해당날짜의 초를 반환한다. 결과값은 0 에서 59
- `DAYNAME(date)` : 해당 날짜의 요일 이름을 반환한다. 일요일은 'Sunday'
- `MONTHNAME(date)` : 해당 날짜의 월 이름을 반환한다. 2월은 'February'
- `QUARTER(date)` : 해당 날짜의 분기를 반환한다. 결과값은 1 에서 4
- `WEEK(date,first)` : 1월 1일부터 해당날가지의 주 수를 반환한다. 주의 시작을 일요일부터 할경우는 두번째 인자를 0, 월요일부터 시작할 경우는 1 을 넣는다. 결과값은 1 에서 52
- `CURDATE()` : 현재날짜를 반환한다. 숫자와 연산을 할경우 숫자로 변환된다. 형식은 'YYYY-MM-DD' 또는 YYYYMMDD
- `CURTIME()` : 현재시간을 반환한다. 숫자와 연산을 할경우 숫자로 변환된다. 형식은 'HH:MM:SS' 또는 HHMMSS
- `NOW() / SYSDATE()` : 현재날짜시간을 반환한다. 숫자와 연산을 할경우 숫자로 변환된다. 형식은 'YYYY-MM-DD HH:MM:SS' 또는 YYYYMMDDHHMMSS