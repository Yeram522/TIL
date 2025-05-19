---
description: >-
  SUBQUERY 다른 쿼리 내에서 실행되는 쿼리이다.  SUBQUERY의 결과를 활용해서 복잡한 MAINQUERY를 작성해 한번에 여러
  작업을 수행할 수 있다.
icon: '8'
---

# SUBQUERY

## 1️⃣ 예제 1

### 서브쿼리

{% code title="💡 민트미역국 카테고리 번호 조회" %}
```sql
SELECT
       CATEGORY_CODE
  FROM TBL_MENU
 WHERE MENU_NAME = '민트미역국';
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (46).png" alt=""><figcaption><p>실행 결과</p></figcaption></figure>

### 메인 쿼리

{% code title="💡 다중열 결과 조회" %}
```sql
SELECT
       MENU_CODE
	,  MENU_NAME
    ,  MENU_PRICE
    ,  CATEGORY_CODE
    ,  ORDERABLE_STATUS
 FROM  TBL_MENU;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (47).png" alt=""><figcaption></figcaption></figure>

### 서브쿼리를 활용한 메인쿼리

{% code title="💡 민트미역국과 같은 카테고리 메뉴 조회" %}
```sql
SELECT
       MENU_CODE
	,  MENU_NAME
    ,  MENU_PRICE
    ,  CATEGORY_CODE
    ,  ORDERABLE_STATUS
 FROM  TBL_MENU
 WHERE CATEGORY_CODE = (SELECT
			       CATEGORY_CODE
			  FROM TBL_MENU
			 WHERE MENU_NAME = '민트미역국');
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (48).png" alt=""><figcaption></figcaption></figure>

## 2️⃣ 예제 2

{% code title="서브 쿼리" %}
```sql
SELECT
       COUNT(*) AS 'count'
  FROM TBL_MENU
  GROUP BY CATEGORY_CODE;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (49).png" alt=""><figcaption></figcaption></figure>

{% code title="" %}
```sql
SELECT
       MAX(count)
  FROM (SELECT
               COUNT(*) AS 'count'
          FROM TBL_MENU
      GROUP BY CATEGORY_CODE) AS countmenu;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (50).png" alt=""><figcaption></figcaption></figure>

## 3️⃣ 예제 3

{% code title="서브쿼리" %}
```sql
SELECT
       AVG(MENU_PRICE)
  FROM TBL_MENU;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (51).png" alt=""><figcaption></figcaption></figure>

{% code title="전체 메뉴 평균가격보다 높은 가격의 메뉴 전체 조회" %}
```sql
SELECT
       MENU_CODE
	,  MENU_NAME
    ,  MENU_PRICE
    ,  CATEGORY_CODE
    ,  ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE MENU_PRICE > (SELECT
			    AVG(MENU_PRICE)
		      FROM TBL_MENU);
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (52).png" alt=""><figcaption></figcaption></figure>
