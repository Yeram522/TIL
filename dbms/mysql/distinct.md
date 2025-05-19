---
description: 중복된 값을 제거하는데 사용된다. 컬럼에 있는 컬럼값들의 종류를 쉽게 파악할 수 있다.
icon: '4'
---

# DISTINCT

## 1️⃣ 단일 열 DISTINCT

{% code title="중복 제거 ❌" %}
```sql
SELECT
       CATEGORY_CODE
 FROM TBL_MENU
ORDER BY CATEGORY_CODE;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (12).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 단일 열 DISTINCT" %}
```sql
SELECT
       DISTINCT CATEGORY_CODE
  FROM TBL_MENU
  ORDER BY CATEGORY_CODE;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (13).png" alt=""><figcaption></figcaption></figure>

## 2️⃣ NULL 값 포함 DISTINCT

```sql
SELECT
       REF_CATEGORY_CODE
  FROM TBL_CATEGORY; 
```

<figure><img src="../../.gitbook/assets/image (14).png" alt=""><figcaption></figcaption></figure>

```sql
SELECT
       DISTINCT REF_CATEGORY_CODE
  FROM TBL_CATEGORY;
```

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

## 3️⃣ 다중열 DISTINC회

{% code title="✅ 다중열 조회" %}
```sql
SELECT
       DISTINCT REF_CATEGORY_CODE
  FROM TBL_CATEGORY;
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

{% code title="✅ 다중열 DISTINCT 사용" %}
```sql
SELECT DISTINCT
       CATEGORY_CODE
	,  ORDERABLE_STATUS
  FROM TBL_MENU;
```
{% endcode %}

{% hint style="success" %}
다중열의 값들이 **모두 동일**하면 **중복된 것**으로 **판별**한다.
{% endhint %}

<figure><img src="../../.gitbook/assets/image (17).png" alt=""><figcaption></figcaption></figure>
