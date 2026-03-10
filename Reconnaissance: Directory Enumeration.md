# Reconnaissance: Directory Enumeration ด้วย Gobuster

## วัตถุประสงค์
เพื่อค้นหา Directory และไฟล์ที่ซ่อนอยู่ของเว็บไซต์เป้าหมาย ซึ่งช่วยให้เข้าใจโครงสร้างของระบบและเตรียมข้อมูลสำหรับการวิเคราะห์ช่องโหว่ในขั้นตอนต่อไป

เว็บไซต์เป้าหมาย
```c
http://172.31.240.1
```

---

## เครื่องมือที่ใช้
- Kali Linux  
- Gobuster  
- Wordlist (dirb common.txt)  
- Web Browser  

Gobuster เป็นเครื่องมือสำหรับค้นหา Directory หรือไฟล์ที่ซ่อนอยู่บนเว็บไซต์ โดยใช้ Wordlist ในการเดา path ของระบบ

---

## ขั้นตอนการทดสอบ

### 1. เปิด Kali Linux
เข้าสู่ระบบ Kali Linux และเปิด Terminal เพื่อเตรียมใช้งานเครื่องมือสำหรับการทำ Reconnaissance

---

### 2. ตรวจสอบการเข้าถึงเว็บไซต์เป้าหมาย
เปิด Web Browser และเข้าเว็บไซต์ 
```c
http://172.31.240.1
```

หากหน้าเว็บไซต์แสดงผลปกติ แสดงว่าเครื่อง Kali สามารถเชื่อมต่อกับเซิร์ฟเวอร์เป้าหมายได้

---

### 3. ใช้ Gobuster เพื่อค้นหา Directory
เปิด Terminal และใช้คำสั่ง

```bash
gobuster dir -u http://172.31.240.1 -w /usr/share/wordlists/dirb/common.txt
```
## ความหมายของคำสั่ง

| คำสั่ง | ความหมาย |
|------|------|
| gobuster | เครื่องมือค้นหา directory |
| dir | โหมดค้นหา directory |
| -u | URL เว็บไซต์เป้าหมาย |
| -w | wordlist สำหรับเดา path |

---

## 4. รอให้ระบบทำการสแกน

Gobuster จะทำการทดสอบ path ต่าง ๆ จาก wordlist และแสดง directory หรือไฟล์ที่พบในเว็บไซต์

### ตัวอย่างผลลัพธ์
```c
.htaccess (403)
.htpasswd (403)
ajax (301)
classes (301)
data (301)
documentation (301)
images (301)
includes (301)
javascript (301)
labs (301)
passwords (301)
phpinfo.php (200)
robots.txt (200)
styles (301)
webservices (301)
```

## 5. ทดลองเข้าถึง Directory ที่พบ

นำ path ที่ค้นพบไปเปิดใน Web Browser เช่น
```c
http://172.31.240.1/phpinfo.php
http://172.31.240.1/passwords/
```
ผลลัพธ์บางหน้าจะปรากฏข้อความ 403 Forbidden


ซึ่งหมายความว่า directory มีอยู่จริง แต่เซิร์ฟเวอร์ไม่อนุญาตให้เข้าถึง

---

## การวิเคราะห์ผลลัพธ์

จากการสแกนพบ directory และไฟล์สำคัญหลายรายการ เช่น

| Path | รายละเอียด |
|----|----|
| /ajax | โฟลเดอร์สำหรับ AJAX |
| /data | โฟลเดอร์ข้อมูล |
| /labs | โฟลเดอร์สำหรับทดสอบ vulnerability |
| /passwords | โฟลเดอร์ที่อาจเก็บข้อมูลรหัสผ่าน |
| /phpinfo.php | ไฟล์แสดงข้อมูลระบบ |
| /robots.txt | ไฟล์กำหนดการเข้าถึงของ crawler |

นอกจากนี้ยังพบข้อมูลของ Web Server จากหน้า 403
```c
Apache/2.4.66 (Debian)
```

จึงสามารถระบุข้อมูลระบบได้ดังนี้

| รายการ | รายละเอียด |
|------|------|
| Web Server | Apache 2.4.66 |
| Operating System | Debian Linux |
| Port | 80 |

---

## สรุปผล

จากการทำ Directory Enumeration ด้วย Gobuster สามารถค้นพบ directory และไฟล์หลายรายการของเว็บไซต์เป้าหมาย เช่น

- `/ajax`
- `/data`
- `/labs`
- `/passwords`
- `/phpinfo.php`

รวมถึงสามารถระบุชนิดของ Web Server และระบบปฏิบัติการของเซิร์ฟเวอร์ได้ ข้อมูลเหล่านี้มีประโยชน์ในการวิเคราะห์ช่องโหว่ของระบบ และสามารถนำไปใช้ในขั้นตอน **Exploitation** ต่อไป
