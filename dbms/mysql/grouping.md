---
description: >-
  GROUP BY절은 결과 집합을 특정 열의 값에 따라 그룹화 하는데 사용된다.  HAVING은 GROUP BY절과 함께 사용해야 하며 그룹에
  대한 조건을 적용하는데 사용된다.
icon: '7'
---

# GROUPING

## 1️⃣ GROUP BY

TBL\_MENU 테이블에서 CATEGORY\_CODE의 값 그룹화

```sql
SELECT
       CATEGORY_CODE
  FROM TBL_MENU
  GROUP BY CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (38).png" alt=""><figcaption></figcaption></figure>

### COUNT

```sql
SELECT
       CATEGORY_CODE
     , COUNT(*)
  FROM TBL_MENU
  GROUP BY CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (39).png" alt=""><figcaption></figcaption></figure>

### SUM

```sql
SELECT
       CATEGORY_CODE
	,  SUM(MENU_PRICE)
 FROM TBL_MENU
 GROUP BY CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (40).png" alt=""><figcaption></figcaption></figure>

### AVG

```sql
SELECT
       CATEGORY_CODE
	,  AVG(MENU_PRICE)
 FROM TBL_MENU
 GROUP BY CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (41).png" alt=""><figcaption></figcaption></figure>

### 2개 이상의 그룹 생성

```sql
SELECT
       MENU_PRICE
	,  CATEGORY_CODE
  FROM TBL_MENU
  GROUP BY MENU_PRICE
         , CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (42).png" alt=""><figcaption></figcaption></figure>

## 2️⃣ HAVING

{% code title="✅ 5번 카테고리(중식)부터 8번 카테고리(커피)까지의 메뉴 카테고리 번호 조회" %}
```sql
SELECT
       CATEGORY_CODE
  FROM TBL_MENU
  GROUP BY CATEGORY_CODE
  HAVING CATEGORY_CODE BETWEEN 5 AND 8;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (43).png" alt=""><figcaption></figcaption></figure>

## 3️⃣ ROLL UP

#### 전체 총계계

마지막 열에 합계가 들어간다.

{% code title="컬럼 한 개를 활용한 ROLLUP(카테고리의 총합)" %}
```sql
SELECT
       CATEGORY_CODE
	,  SUM(MENU_PRICE)
 FROM  TBL_MENU
 GROUP BY CATEGORY_CODE
 WITH ROLLUP;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (44).png" alt=""><figcaption></figcaption></figure>

#### 부분 소계

{% code title="컬럼 두 개를 활용한 ROLLUP(같은 메뉴 가격별 총합 및 해당 메뉴 가격별 같은 카테고리의 총합)" %}
```sql
SELECT
       MENU_PRICE
     , CATEGORY_CODE
     , SUM(MENU_PRICE)
  FROM TBL_MENU
  GROUP BY MENU_PRICE
       ,  CATEGORY_CODE
  WITH ROLLUP;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (45).png" alt=""><figcaption><p>중간 소계가 나온다.</p></figcaption></figure>
