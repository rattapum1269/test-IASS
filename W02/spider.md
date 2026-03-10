# Reconnaissance 2: Spider / Crawling ด้วย OWASP ZAP

## วัตถุประสงค์
เพื่อรวบรวมข้อมูลเกี่ยวกับโครงสร้างของเว็บไซต์เป้าหมาย เช่น URL หน้าเว็บต่าง ๆ และ parameter ที่มีอยู่ โดยใช้เทคนิค Web Crawling ผ่านเครื่องมือ OWASP ZAP

เว็บไซต์เป้าหมาย

```
http://172.31.240.1
```

---

## เครื่องมือที่ใช้

- Kali Linux
- OWASP ZAP

OWASP ZAP (Zed Attack Proxy) เป็นเครื่องมือสำหรับทดสอบความปลอดภัยของ Web Application ที่สามารถทำ Spider หรือ Web Crawling เพื่อค้นหา URL และโครงสร้างของเว็บไซต์ได้

---

## ขั้นตอนการทดสอบ

### 1. เปิดโปรแกรม OWASP ZAP

เปิดโปรแกรมจาก Kali Linux

Applications → Web Application Analysis → OWASP ZAP

---

### 2. ใส่ URL เป้าหมาย

ในหน้าต่าง **Automated Scan** ให้ใส่ URL ของเว็บไซต์

```
http://172.31.240.1
```

จากนั้นกดปุ่ม **Attack**

---

### 3. เริ่มการทำ Spider

OWASP ZAP จะเริ่มทำการ Spider หรือ Crawling เว็บไซต์ โดยจะพยายามเข้าถึงหน้าต่าง ๆ ของเว็บไซต์เพื่อค้นหา URL และโครงสร้างของระบบ

---

### 4. ตรวจสอบผลลัพธ์

เมื่อการสแกนเสร็จสิ้น ZAP จะแสดงจำนวน URL ที่พบ เช่น

- URLs Found: 484
- Nodes Added: 88

ตัวอย่าง URL ที่พบจากการ Crawling เช่น

```
/index.php
/login.php
/register.php
/index.php?page=login.php
/index.php?page=register.php
/phpinfo.php
```

---

## การวิเคราะห์ผลลัพธ์

จากการใช้ OWASP ZAP Spider พบว่าเว็บไซต์มีหลายหน้าที่สามารถเข้าถึงได้ เช่น หน้า Login, Register และหน้าที่มี parameter ใน URL

ตัวอย่าง URL ที่มี parameter

```
index.php?page=login.php

```
Parameter `page=` สามารถนำไปใช้ในการทดสอบช่องโหว่ เช่น

- File Inclusion
- Parameter Manipulation
- Injection Attack

---
<img width="1912" height="671" alt="image" src="https://github.com/user-attachments/assets/2968cecd-76f1-4565-aed3-c60363c99e6c" />

## สรุปผล

การใช้ OWASP ZAP Spider ช่วยให้สามารถรวบรวม URL และโครงสร้างของเว็บไซต์ได้อย่างรวดเร็ว ทำให้ทราบถึงหน้าต่าง ๆ ของระบบ รวมถึง parameter ที่สำคัญ ซึ่งสามารถนำไปใช้วิเคราะห์ช่องโหว่ของเว็บไซต์ในขั้นตอน Exploitation ต่อไป

ถ้านายอยากให้ รายงานดูโปรขึ้นอีก (แบบที่อาจารย์เห็นแล้วรู้ว่าเป็นงาน Cybersecurity จริง) เดี๋ยวผมช่วยทำเพิ่ม
