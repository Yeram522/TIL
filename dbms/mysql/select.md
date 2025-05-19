---
icon: '1'
---

# SELECT

SELECT절은 MYSQL의 가장 기본적인 명령어로&#x20;특정 테이블에서 원하는 데이터를 조회해서 가져오는데 사용 된다.



{% code title="✅ 속성으로 열 선택" %}
```sql
SELECT 
       MENU_NAME
  FROM TBL_MENU;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (3) (1).png" alt=""><figcaption><p>SELECT 한 속성의 행 반환</p></figcaption></figure>

{% code title=" ✅속성으로 여러 열 선택" %}
```sql
SELECT
       MENU_CODE
     , MENU_NAME
     , MENU_PRICE
  FROM TBL_MENU;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (4) (1).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 전체 테이블 가져오기" %}
```sql
SELECT * FROM TBL_MENU;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (5) (1).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 사칙 연산 가능" %}
```sql
SELECT 6 + 3;
SELECT 6 * 3;
SELECT 6 % 3;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (6) (1).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 내장 함수 사용 가능" %}
```sql
SELECT NOW();
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (7) (1).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 컬럼 별칭 사용" %}
```sql
SELECT CONCAT('홍', '', '길동') AS name;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (8) (1).png" alt=""><figcaption></figcaption></figure>
