---
description: SELECT문의 결과 집합에서 반환할 행의 수를 제한하는데 사용된다.
icon: '5'
---

# LIMIT

## 1️⃣ 전체 행 조회

```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
  ORDER BY MENU_PRICE DESC;
```

<figure><img src="../../.gitbook/assets/image (18).png" alt=""><figcaption></figcaption></figure>

## 2️⃣ N번 행부터 M번 행까지 조회

```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
  ORDER BY MENU_PRICE DESC
  LIMIT 1, 4; -- 0번째부터 시작한다 했을 때, 1번째부터 4번째까지 조회
```

<figure><img src="../../.gitbook/assets/image (19).png" alt=""><figcaption></figcaption></figure>

## 3️⃣ 상위 N개 줄만 조회

```sql
SELECT
       MENU_CODE
	 , MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU
  ORDER BY MENU_PRICE DESC,
           MENU_NAME ASC
  LIMIT 5;
```

<figure><img src="../../.gitbook/assets/image (20).png" alt=""><figcaption></figcaption></figure>
