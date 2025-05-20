---
description: >-
  SET 연산자는 두 개 이상의 SELECT문의 결과 집합을 결합하는데 사용한다.    SET 연산자를 통해 결합하는 결과 집합의 컬럼이
  동일해야 한다.
icon: '9'
---

# SET\_OPERATION

## 1️⃣ UNION

두 개 이상의 SELECT 문의 결과를 결합하여 중복된 레코드를 제거한 후 반환하는 연산자

<pre class="language-sql"><code class="lang-sql"><strong>SELECT
</strong>       MENU_CODE
	 , MENU_NAME
     , MENU_PRICE
     , CATEGORY_CODE
     , ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE CATEGORY_CODE = 10
 UNION
SELECT
       MENU_CODE
	 , MENU_NAME
     , MENU_PRICE
     , CATEGORY_CODE
     , ORDERABLE_STATUS
  FROM TBL_MENU
 WHERE MENU_PRICE &#x3C; 9000;
</code></pre>
