---
description: >-
  JOIN은 두 개 이상의 테이블을 관련 있는 컬럼을 통해 결합하는데 사용된다.  두 개 이상 테이블은 반드시 연관 있는 컬럼이 존재해야 하며
  이를 통해 JOIN된    테이블들의 컬럼을 모두 활용할 수 있다
icon: '6'
---

# JOIN

## 1️⃣ ALIAS(별칭)

SQL문의 컬럼 또는 테이블에 별칭을 달아줄 수 있다. 이러한 별칭은 ALIAS라고 한다.

```sql
SELECT
       MENU_CODE AS 'code'
     , MENU_NAME name
     , MENU_PRICE 'price'
  FROM TBL_MENU
  ORDER BY MENU_PRICE;
```

<figure><img src="../../.gitbook/assets/image (21).png" alt=""><figcaption></figcaption></figure>

### 테이블 별칭

테이블에 별칭을 작성할 수 있으며 어떤 테이블 소속인지를 쉽게 알 수 있게 한다.\
<mark style="color:red;">테이블 별칭은 AS를 써도 되고 생략도 가능하다.</mark>

```sql
SELECT
       A.CATEGORY_CODE
     , A.MENU_NAME
  FROM TBL_MENU A 
  ORDER BY A.CATEGORY_CODE,
           A.MENU_NAME;
```

## 2️⃣ INNER JOIN

두 테이블의 <mark style="color:red;">교집합</mark>을 반환하는 SQL  JOIN\
**INNER JOIN INNER** 키워드는 **생략이 가능**하다.\
<mark style="background-color:yellow;">**ON을 활용한 JOIN :**</mark> 컬럼명이 같거나 다를 경우 _<mark style="color:red;">ON으로 서로 연관있는 컬럼에 대한 조건을 작성하여 JOIN</mark>_

<figure><img src="../../.gitbook/assets/image (25).png" alt=""><figcaption><p>tbl_category<br></p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (27).png" alt=""><figcaption><p>tbl_menu</p></figcaption></figure>

```sql
SELECT
       A.MENU_NAME
	 , B.CATEGORY_NAME
  FROM TBL_MENU A
--  INNER JOIN TBL_CATEGORY B ON A.CATEGORY_CODE = B.CATEGORY_CODE;
  JOIN TBL_CATEGORY B ON A.CATEGORY_CODE = B.CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (22).png" alt=""><figcaption></figcaption></figure>

## 3️⃣ USING

<mark style="background-color:yellow;">컬럼명이 같을 경우</mark> **USING**으로 _서로 연관있는 컬럼에 대한 조건을 작&#xC131;_&#xD558;여 JOIN

```sql
SELECT
       A.MENU_NAME
     , B.CATEGORY_NAME
  FROM TBL_MENU A
  INNER JOIN TBL_CATEGORY B USING(CATEGORY_CODE);
```



## 4️⃣ LEFT JOIN

동일한 column으로 하나로 합쳐지고 left 쪽(A)의 모든 데이터를 포함하고 B의 데이터는 null로 표시.

<figure><img src="../../.gitbook/assets/image (29).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
       A.CATEGORY_CODE
     , B.MENU_NAME
  FROM TBL_CATEGORY A
  LEFT JOIN TBL_MENU B ON A.CATEGORY_CODE = B.CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (31).png" alt=""><figcaption><p>tbl_category</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (32).png" alt=""><figcaption><p>tbl_menu</p></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (33).png" alt=""><figcaption></figcaption></figure>

## 5️⃣ RIGHT JOIN

동일한 column으로 하나로 합쳐지고 right쪽(B)의 모든 데이터를 포함하고 A의 데이터는 null로 표시.

<figure><img src="../../.gitbook/assets/image (30).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
       A.CATEGORY_CODE
     , B.MENU_NAME
  FROM TBL_CATEGORY A
  RIGHT JOIN TBL_MENU B ON A.CATEGORY_CODE = B.CATEGORY_CODE;  
```

<figure><img src="../../.gitbook/assets/image (34).png" alt=""><figcaption></figcaption></figure>

## 6️⃣ CROSS JOIN

두 테이블의 <mark style="background-color:green;">**모든 가능한 조합**</mark>을 반환하는 JOIN

```sql
SELECT
       A.MENU_NAME
     , B.CATEGORY_NAME
  FROM TBL_MENU A
  CROSS JOIN TBL_CATEGORY B;
```

<figure><img src="../../.gitbook/assets/image (36).png" alt=""><figcaption></figcaption></figure>

## 7️⃣ SELF\_JOIN

**같은 테이블 내**에서 <mark style="background-color:yellow;">행과 행 사이의 관계</mark>를 찾기 위해 사용되는 SQL JOIN 유형\
&#xNAN;_<mark style="color:orange;">카테고리별 대분류 확인</mark>_&#xC744; 위한 SELF JOIN 조회

```sql
SELECT
       A.CATEGORY_NAME
     , B.CATEGORY_NAME
  FROM TBL_CATEGORY A
  JOIN TBL_CATEGORY B ON A.REF_CATEGORY_CODE = B.CATEGORY_CODE
  WHERE A.REF_CATEGORY_CODE IS NOT NULL;
```

<figure><img src="../../.gitbook/assets/image (37).png" alt=""><figcaption></figcaption></figure>
