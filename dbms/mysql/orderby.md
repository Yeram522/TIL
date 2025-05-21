---
icon: '2'
---

# Orderby

ORDER BY절은 SELECT문과 함께 사용하며 결과 집합을 특정 열이나  열들의 값에 따라 정렬하는 데 사용한다.

### attribute를 Select

```sql
SELECT
      MENU_CODE
     ,MENU_NAME
     ,MENU_PRICE
  FROM TBL_MENU
```

<figure><img src="../../.gitbook/assets/image (53).png" alt=""><figcaption></figcaption></figure>

### ascending order

`MENU_PRICE` 를 오름차순으로 정렬

```sql
ORDER BY MENU_PRICE ASC;
```

<figure><img src="../../.gitbook/assets/image (1) (1) (1).png" alt=""><figcaption></figcaption></figure>

### descending order

`MENU_PRICE` 를 내림차순으로 정렬

```sql
ORDER BY MENU_PRICE DESC;
```

<figure><img src="../../.gitbook/assets/image (2) (1) (1).png" alt=""><figcaption></figcaption></figure>

### ascending and descending order

오름차순과 내림차순을 각각 다른 어트리뷰트에 적용할 수 있다.

```sql
ORDER BY MENU_PRICE DESC,
         MENU_NAME ASC;
```

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption></figcaption></figure>

### attribute끼리 연산한 결과를 컬럼으로 받을 수 있다.

```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , MENU_PRICE * MENU_CODE
  FROM TBL_MENU
 ORDER BY MENU_PRICE * MENU_CODE DESC;
```

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

### FIELD()를 이용한 정렬 우선순위 정하기

```sql
SELECT
       MENU_NAME
     , ORDERABLE_STATUS
  FROM TBL_MENU
ORDER BY FIELD(ORDERABLE_STATUS,'N','Y');
```

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

### 오름차순 시 NULL 을 처음으로 정렬

```sql
SELECT
       CATEGORY_CODE
     , CATEGORY_NAME
     , REF_CATEGORY_CODE
  FROM TBL_CATEGORY
ORDER BY REF_CATEGORY_CODE;
```

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

### 오름차순 시 NULL을 마지막으로 정렬

```sql
SELECT
       CATEGORY_CODE
     , CATEGORY_NAME
     , REF_CATEGORY_CODE
  FROM TBL_CATEGORY
ORDER BY REF_CATEGORY_CODE IS NULL;
```

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>

### 내림차순 시 NULL을 마지막으로 정렬

```sql
SELECT
      CATEGORY_CODE
	, CATEGORY_NAME
    , REF_CATEGORY_CODE
 FROM TBL_CATEGORY
ORDER BY REF_CATEGORY_CODE IS NULL DESC, REF_CATEGORY_CODE DESC;
```

`REF_CATEGORY_CODE IS NULL` 는 해당 컬럼이 NULL 이면 TRUE(1), 아니면 FALSE(0)을 반환한다.\
`DESC` 는 내림차순이므로 TRUE(1)가 FALSE(0)보다 먼저 온다.\
💡 NULL을 가진 행들이 먼저 나오고, NULL이 아닌 값이 다음에 나온다.

`REF_CATEGORY_CODE_DESC` 는 각 그룹 내에서 해당 속성값을 기준으로 내림차순 정렬하므로, NULL이 아닌 값들 중에서 큰 값부터 작은 순으로 정렬된다.

따라서, 이 쿼리는 아래와 같이 NULL값을 가진 행들이 가장 먼저 표시 되고 `REF_CATEGORY_CODE` 값의 내림차순으로 정렬되어 표시된다.



### 내림차순 시 NULL을 처음으로 정렬

```sql
SELECT
       CATEGORY_CODE
     , CATEGORY_NAME
     , REF_CATEGORY_CODE
  FROM TBL_CATEGORY
 ORDER BY REF_CATEGORY_CODE IS NULL DESC, REF_CATEGORY_CODE DESC;
```

<figure><img src="../../.gitbook/assets/image (2).png" alt=""><figcaption></figcaption></figure>
