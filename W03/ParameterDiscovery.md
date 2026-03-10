## Reconnaissance 3: Parameter Discovery ด้วย OWASP ZAP

### วัตถุประสงค์
เพื่อค้นหา parameter ที่ใช้ใน URL ของเว็บไซต์ ซึ่งสามารถนำไปใช้ในการวิเคราะห์ช่องโหว่ของระบบได้

### เครื่องมือที่ใช้
- Kali Linux
- OWASP ZAP

### ขั้นตอนการทดสอบ
1. เปิด OWASP ZAP
2. เข้าเว็บไซต์เป้าหมายผ่าน Browser  
```
http://172.31.240.1
```
3. คลิกเมนูต่าง ๆ ภายในเว็บไซต์เพื่อให้เกิด request ใหม่
4. ตรวจสอบ request ในแท็บ **History** ของ OWASP ZAP
5. วิเคราะห์ URL ที่มี parameter

### ผลลัพธ์
<img width="1916" height="826" alt="image" src="https://github.com/user-attachments/assets/18a45f0f-ebae-4479-95ff-b92128b7f0e9" />

พบ URL ที่มี parameter เช่น

```
http://172.31.240.1/index.php?page=login.php
```

Parameter ที่พบ ได้แก่

| Parameter | รายละเอียด |
|---|---|
page | ใช้สำหรับเรียกหน้าเว็บภายในระบบ |
redirectPage | ใช้สำหรับ redirect ไปยังหน้าอื่น |

### การวิเคราะห์
Parameter ที่พบสามารถนำไปใช้ในการทดสอบช่องโหว่ของระบบได้ เช่น

- File Inclusion
- Parameter Manipulation
- Injection Attack


จากการใช้ OWASP ZAP สามารถค้นพบ parameter ใน URL ของเว็บไซต์ ซึ่งเป็นข้อมูลสำคัญที่ช่วยในการวิเคราะห์โครงสร้างของเว็บแอปพลิเคชันและสามารถนำไปใช้ในขั้นตอน Exploitation ต่อไป

ตอนนี้สถานะ Recon ของนายคือ
