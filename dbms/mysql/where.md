---
description: WHERE절은 특정 조건에 맞는 레코드만을 선택하는데 사용되며 다양한 방법으로 조건을 설정할 수 있다.
icon: '3'
---

# WHERE

## 1️⃣ 비교 연산자 예제와 함께 WHERE절 사용

```sql
SELECT
       MENU_NAME
     , MENU_PRICE
     , ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE ORDERABLE_STATUS = 'Y';
```

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
       MENU_NAME
     , MENU_PRICE
     , ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE MENU_PRICE = 13000;
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>

### 같지 않음 연산자와 함께 WHERE절 사용

```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE ORDERABLE_STATUS != 'Y';
```

<figure><img src="../../.gitbook/assets/image (3).png" alt=""><figcaption></figcaption></figure>

### 대소 비교 연산자와 함께 WHERE절 사용

```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
 WHERE MENU_PRICE > 20000;
```

<figure><img src="../../.gitbook/assets/image (4).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
 WHERE MENU_PRICE <= 20000;
```

<figure><img src="../../.gitbook/assets/image (5).png" alt=""><figcaption></figcaption></figure>

## 2️⃣ WHERE + AND&#x20;

```sql
 SELECT
       MENU_NAME
	,  MENU_PRICE
    ,  CATEGORY_CODE
    ,  ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE ORDERABLE_STATUS = 'Y'
   AND CATEGORY_CODE = 10;
```

<figure><img src="../../.gitbook/assets/image (6).png" alt=""><figcaption></figcaption></figure>

## 3️⃣ WHERE + OR

```sql
SELECT
     MENU_NAME
   , MENU_PRICE
   , CATEGORY_CODE
   , ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE ORDERABLE_STATUS = 'Y'
    OR CATEGORY_CODE = 10;
```

<figure><img src="../../.gitbook/assets/image (7).png" alt=""><figcaption></figcaption></figure>

## 4️⃣  WHERE + BETWEEN

```sql
SELECT 
       MENU_NAME
     , MENU_PRICE
     , CATEGORY_CODE
  FROM TBL_MENU
 WHERE MENU_PRICE BETWEEN 10000 AND 25000
 ORDER BY MENU_PRICE;
```

<figure><img src="../../.gitbook/assets/image (8).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 부정 표현 `NOT`" %}
```sql
SELECT 
       MENU_NAME
     , MENU_PRICE
     , CATEGORY_CODE
  FROM TBL_MENU
 WHERE MENU_PRICE NOT BETWEEN 10000 AND 25000
 ORDER BY MENU_PRICE;
```
{% endcode %}

## 5️⃣ WHERE + LIKE&#x20;

```sql
SELECT
       MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
 WHERE MENU_NAME LIKE '%마늘%'
 ORDER BY MENU_NAME현
```

<figure><img src="../../.gitbook/assets/image (9).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 부정 표현" %}
```sql
SELECT
       MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
 WHERE MENU_NAME NOT LIKE '%마늘%'
 ORDER BY MENU_NAME;
```
{% endcode %}

## 6️⃣ WHERE + IN

```sql
SELECT
       MENU_NAME
     , CATEGORY_CODE
  FROM TBL_MENU
 WHERE CATEGORY_CODE IN (4,5,6)
 ORDER BY CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (10).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 부정 표현 `NOT IN`" %}
```sql
SELECT
       MENU_NAME
     , CATEGORY_CODE
  FROM TBL_MENU
 WHERE CATEGORY_CODE NOT IN (4,5,6)
 ORDER BY CATEGORY_CODE; 
```
{% endcode %}



## 7️⃣ WHERE + IS NULL

```sql
SELECT
       CATEGORY_CODE
     , CATEGORY_NAME
     , REF_CATEGORY_CODE
  FROM TBL_CATEGORY
 WHERE REF_CATEGORY_CODE IS NULL; 
```

<figure><img src="../../.gitbook/assets/image (11).png" alt=""><figcaption></figcaption></figure>

{% code title="✅부정 표현 `NOT NULL`" %}
```sql
SELECT
       CATEGORY_CODE
     , CATEGORY_NAME
     , REF_CATEGORY_CODE
  FROM TBL_CATEGORY
 WHERE REF_CATEGORY_CODE IS NOT NULL;  
```
{% endcode %}
