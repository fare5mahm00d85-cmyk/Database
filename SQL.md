-- ==========================
-- DATABASE
-- ==========================
# 1. SELECT

**الوظيفة:**  
يعرض البيانات من جدول.

**الصيغة:**

```
SELECT * FROM users;
```

**الشرح:**

- `SELECT` = اختار.
- `*` = كل الأعمدة.
- `FROM` = من الجدول.

**مثال:**

```
SELECT name,email
FROM users;
```

يعرض عمودي `name` و`email` فقط.

---

# 2. FROM

**الوظيفة:**  
يحدد الجدول الذي سيتم أخذ البيانات منه.

**مثال:**

```
SELECT *
FROM users;
```

بدون `FROM` لا يعرف SQL من أي جدول يجلب البيانات.

---

# 3. WHERE

**الوظيفة:**  
يحدد شرطًا لعرض بيانات معينة.

**مثال:**

```
SELECT *
FROM users
WHERE id=1;
```

يعرض المستخدم الذي رقمه 1 فقط.

---

### أمثلة

```
WHERE age>20
```

أكبر من 20.

```
WHERE age<20
```

أقل من 20.

```
WHERE age>=20
```

أكبر من أو يساوي 20.

```
WHERE age<=20
```

أقل من أو يساوي 20.

```
WHERE age<>20
```

لا يساوي 20.

---

# 4. ORDER BY

**الوظيفة:**  
يرتب النتائج.

تصاعدي:

```
SELECT *
FROM users
ORDER BY age ASC;
```

تنازلي:

```
SELECT *
FROM users
ORDER BY age DESC;
```

---

# 5. UNION

**الوظيفة:**  
يجمع نتائج استعلامين.

```
SELECT name
FROM users

UNION

SELECT product_name
FROM products;
```

### في SQL Injection

يستخدم لاستخراج البيانات.

مثال:

```
' UNION SELECT NULL,NULL--
```

---

# 6. LIMIT

**الوظيفة:**  
يعرض عددًا محددًا من الصفوف.

```
SELECT *
FROM users
LIMIT 5;
```

يعرض أول خمسة مستخدمين.

---

# 7. GROUP BY

**الوظيفة:**  
يجمع البيانات حسب قيمة معينة.

```
SELECT age,
COUNT(*)

FROM users

GROUP BY age;
```

يعرض عدد المستخدمين لكل عمر.

---

# 8. HAVING

**الوظيفة:**  
يشبه WHERE لكنه يعمل بعد GROUP BY.

```
SELECT age,
COUNT(*)

FROM users

GROUP BY age

HAVING COUNT(*)>2;
```

يعرض الأعمار التي يوجد لها أكثر من مستخدمين.

---

# 9. JOIN

**الوظيفة:**  
يربط جدولين معًا.

مثال:

جدول المستخدمين

|id|name|
|---|---|
|1|Fares|

جدول الطلبات

|user_id|product|
|---|---|
|1|Laptop|

```
SELECT *

FROM users

INNER JOIN orders

ON users.id=orders.user_id;
```

النتيجة

|name|product|
|---|---|
|Fares|Laptop|

---

# 10. INSERT

**الوظيفة:**  
إضافة بيانات.

```
INSERT INTO users(name,email)

VALUES('Fares','fares@gmail.com');
```

---

# 11. UPDATE

**الوظيفة:**  
تعديل بيانات.

```
UPDATE users

SET age=22

WHERE id=1;
```

---

# 12. DELETE

**الوظيفة:**  
حذف بيانات.

```
DELETE FROM users

WHERE id=1;
```

---

# 13. CREATE TABLE

**الوظيفة:**  
إنشاء جدول.

```
CREATE TABLE users(

id INT,

name VARCHAR(50),

email VARCHAR(100)

);
```

---

# 14. ALTER TABLE

**الوظيفة:**  
تعديل الجدول.

إضافة عمود:

```
ALTER TABLE users

ADD phone VARCHAR(20);
```

حذف عمود:

```
ALTER TABLE users

DROP COLUMN phone;
```

---

# 15. DROP TABLE

**الوظيفة:**  
يحذف الجدول بالكامل.

```
DROP TABLE users;
```

---

# 16. SHOW DATABASES

**الوظيفة:**  
يعرض قواعد البيانات.

```
SHOW DATABASES;
```

---

# 17. SHOW TABLES

**الوظيفة:**  
يعرض الجداول داخل قاعدة البيانات الحالية.

```
SHOW TABLES;
```

---

# 18. DESCRIBE

**الوظيفة:**  
يعرض معلومات الجدول.

```
DESCRIBE users;
```

النتيجة

|Field|Type|
|---|---|
|id|INT|
|name|VARCHAR(50)|

---

# 19. NULL

**الوظيفة:**  
تعني عدم وجود قيمة.

```
SELECT *

FROM users

WHERE email IS NULL;
```

يعرض المستخدمين الذين ليس لديهم بريد إلكتروني.

---

# 20. LIKE

**الوظيفة:**  
البحث باستخدام نمط.

يبدأ بـ F

```
SELECT *

FROM users

WHERE name LIKE 'F%';
```

ينتهي بـ s

```
SELECT *

FROM users

WHERE name LIKE '%s';
```

يحتوي على ar

```
SELECT *

FROM users

WHERE name LIKE '%ar%';
```

## DISTINCT

إزالة النتائج المكررة.

```
SELECT DISTINCT username
FROM users;
```

---

## IN

```
SELECT *
FROM users
WHERE id IN (1,2,3);
```

---

## BETWEEN

```
SELECT *
FROM users
WHERE age BETWEEN 20 AND 30;
```

---

## IS NULL

```
SELECT *
FROM users
WHERE email IS NULL;
```

---

## IS NOT NULL

```
SELECT *
FROM users
WHERE email IS NOT NULL;
```

---

## AND

```
WHERE username='admin'
AND password='123'
```

---

## OR

```
WHERE username='admin'
OR 1=1
```

**وده من أشهر الأمثلة لفهم منطق SQL Injection.**

---

## NOT

```
WHERE NOT id=1
```

---

# المرحلة 3 (الأهم في SQL Injection)

هنا تبدأ تتعلم الدوال (Functions) اللي هتشوفها في اللابات.

## version()

تعرض إصدار قاعدة البيانات.

```
SELECT version();
```

---

## database()

تعرض اسم قاعدة البيانات الحالية.

```
SELECT database();
```

---

## user()

تعرض المستخدم الحالي.

```
SELECT user();
```

---

## current_user()

تعرض المستخدم الحالي أيضًا (قد يختلف حسب الصلاحيات).

```
SELECT current_user();
```

---

## @@version

طريقة أخرى لمعرفة إصدار قاعدة البيانات.

```
SELECT @@version;
```

---

## CONCAT()

دمج نصين أو أكثر.

```
SELECT CONCAT(name,email)
FROM users;
```

---

## LENGTH()

طول النص.

```
SELECT LENGTH(username)
FROM users;
```

---

## SUBSTRING()

استخراج جزء من النص.

```
SELECT SUBSTRING(username,1,3)
FROM users;
```

---

## ASCII()

تحويل الحرف إلى رقمه.

```
SELECT ASCII('A');
```

---

## IF()

شرط.

```
SELECT IF(1=1,'YES','NO');
```

---

## SLEEP()

ينتظر عددًا من الثواني.

```
SELECT SLEEP(5);
```

**مهم جدًا في Time-based Blind SQL Injection.**

---

## CAST()

تحويل نوع البيانات.

```
SELECT CAST(id AS CHAR)
FROM users;
```

---

## COALESCE()

ترجع أول قيمة ليست `NULL`.

```
SELECT COALESCE(email,'No Email')
FROM users;
```


# المرحلة الرابعة: استكشاف قاعدة البيانات (Database Enumeration)

الفكرة الأساسية:

لما تكتشف وجود SQL Injection، غالبًا لا تعرف:

- اسم قاعدة البيانات.
- أسماء الجداول.
- أسماء الأعمدة.
- مكان البيانات المهمة.

لذلك تتعلم أولًا **كيف تُنظَّم قواعد البيانات** ثم كيف تُستخرج هذه المعلومات في بيئة اختبار مثل PortSwigger.

---

# أولًا: ما هي `information_schema`؟

هي قاعدة بيانات خاصة موجودة في MySQL وMariaDB.

لا تحتوي على بيانات المستخدمين، لكنها تحتوي على **معلومات عن قواعد البيانات نفسها** (Metadata).

يعني تخيل:

```
Database
│
├── users
├── products
├── orders
```

`information_schema` هي التي تصف هذا الهيكل.

---

# أهم الجداول داخلها

## 1. `information_schema.tables`

يحتوي على معلومات عن جميع الجداول.

من أهم الأعمدة:

- `table_schema` → اسم قاعدة البيانات.
- `table_name` → اسم الجدول.

---

## 2. `information_schema.columns`

يحتوي على معلومات عن أعمدة كل جدول.

من أهم الأعمدة:

- `table_name`
- `column_name`
- `data_type`

---

# لماذا هذا مهم؟

افترض أنك دخلت معملًا في PortSwigger.

أنت تعرف فقط أن هناك SQL Injection.

لكن لا تعرف:

```
users
products
admin
customers
```

ولا تعرف:

```
username
password
email
```

فلا يمكنك طلب بيانات من جدول لا تعرف اسمه.

لهذا تتعلم أولًا **استكشاف البنية**.

---

# ترتيب التفكير

في أي معمل UNION-based غالبًا يكون التفكير كالتالي:

1. هل يوجد SQL Injection؟
2. كم عدد الأعمدة؟
3. أي الأعمدة تقبل عرض النص؟
4. ما اسم قاعدة البيانات؟
5. ما أسماء الجداول؟
6. ما أسماء الأعمدة؟
7. ما البيانات المطلوبة؟

لو حفظت هذا الترتيب، هتفهم أغلب لابات SQL Injection.

---

# الدوال المهمة

## `database()`

تعرض اسم قاعدة البيانات الحالية.

```
SELECT database();
```

---

## `version()`

تعرض إصدار قاعدة البيانات.

```
SELECT version();
```

---

## `user()`

تعرض المستخدم الحالي لقاعدة البيانات.

```
SELECT user();
```

---

## `current_user()`

تعرض المستخدم الحالي أيضًا (قد يختلف حسب الصلاحيات).

```
SELECT current_user();
```

---

# دوال النصوص المهمة

## `CONCAT()`

دمج أكثر من نص.

```
SELECT CONCAT(first_name, last_name)
FROM users;
```

مثال:

```
Ali Mohamed
```

---

## `LENGTH()`

يعرض طول النص.

```
SELECT LENGTH(name)
FROM users;
```

---

## `SUBSTRING()`

يستخرج جزءًا من النص.

```
SELECT SUBSTRING(name,1,3)
FROM users;
```

إذا كان الاسم:

```
Mohamed
```

النتيجة:

```
Moh
```

---

## `ASCII()`

يعرض القيمة الرقمية لحرف.

```
SELECT ASCII('A');
```

النتيجة:

```
65
```

ويظهر كثيرًا في Blind SQL Injection.

---

# الدوال المنطقية

## `IF()`

```
SELECT IF(1=1,'YES','NO');
```

النتيجة:

```
YES
```

---

## `CASE`

بديل لـ IF في بعض قواعد البيانات.

```
SELECT
CASE
WHEN age > 18 THEN 'Adult'
ELSE 'Child'
END
FROM users;
```

---

# Time-based

## `SLEEP()`

```
SELECT SLEEP(5);
```

يجعل قاعدة البيانات تنتظر خمس ثوانٍ.

ويُستخدم في فهم هجمات **Time-based Blind SQL Injection**.

---

# التحويل

## `CAST()`

تحويل نوع البيانات.

```
SELECT CAST(id AS CHAR)
FROM users;
```

---

# التعامل مع NULL

## `COALESCE()`

يرجع أول قيمة ليست NULL.

```
SELECT COALESCE(email,'No Email')
FROM users;
```

إذا كان البريد فارغًا:

```
No Email
```