# Reconnaissance 4: Technology Detection ด้วย OWASP ZAP

## วัตถุประสงค์
เพื่อระบุเทคโนโลยีที่เว็บไซต์ใช้ เช่น Web Server, Programming Language และ Library ต่าง ๆ ซึ่งสามารถนำไปใช้ในการวิเคราะห์ช่องโหว่ของระบบได้

เว็บไซต์เป้าหมาย


http://172.31.240.1


---

## เครื่องมือที่ใช้

- Kali Linux
- OWASP ZAP

---

## ขั้นตอนการทดสอบ

1. เปิดโปรแกรม OWASP ZAP ใน Kali Linux
2. เข้าเว็บไซต์เป้าหมายผ่าน Web Browser


http://172.31.240.1


3. หลังจากเข้าเว็บไซต์แล้ว ให้ตรวจสอบข้อมูลในแท็บ **Technology**
4. เลือกเว็บไซต์ `http://172.31.240.1` จาก Sites Tree
5. วิเคราะห์เทคโนโลยีที่ระบบใช้

---

## ผลลัพธ์

จากการตรวจสอบด้วย OWASP ZAP พบว่าเว็บไซต์ใช้เทคโนโลยีดังนี้

| Technology | Category |
|---|---|
| Apache HTTP Server 2.4.66 | Web Server |
| Debian | Operating System |
| PHP | Programming Language |
| jQuery | JavaScript Library |
| Google Font API | Font Scripts |
| HSTS | Security |

---

## การวิเคราะห์

จากข้อมูลที่ตรวจพบ ทำให้ทราบว่าเว็บไซต์ทำงานบน Web Server ประเภท Apache และใช้ภาษา PHP ในการพัฒนา รวมถึงใช้ JavaScript Library เช่น jQuery ในฝั่ง Client-side ข้อมูลเหล่านี้ช่วยให้สามารถวิเคราะห์โครงสร้างของระบบ และระบุช่องโหว่ที่อาจเกิดขึ้นกับเทคโนโลยีดังกล่าวได้

---
<img width="1902" height="825" alt="image" src="https://github.com/user-attachments/assets/6ae5fc63-9def-4890-80cd-fa9e501e3ae3" />

## สรุปผล

การใช้ OWASP ZAP ในการตรวจสอบเทคโนโลยีของเว็บไซต์ช่วยให้สามารถระบุประเภทของ Web Server, Programming Lang
