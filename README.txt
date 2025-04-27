Project NoSQL กลุ่มที่ 5
ไม่มีหรอกครับ โจทย์ที่ยากไป มีแต่ใจที่ไม่แข็งพอ
นายคุณานนต์	หฤทัยธรรม		รหัสนิสิต     66102010134
นายศิลายุชย์	โชติธรรมาภรณ์	รหัสนิสิต     66102010134
นายธัญวรัตม์	ก.วิบูลย์ศักดิ์ศรี	รหัสนิสิต     66102010567


ระบบจัดการบันทึกหนังสือส่วนตัว(Personal book manager)
เป็นเว็บแอปพลิเคชันที่ช่วยให้ผู้ใช้สามารถจัดการคอลเลกชันหนังสือส่วนตัวของตนเองได้
ผู้ใช้สามารถสมัครสมาชิก, เข้าสู่ระบบ และทำการดำเนินการ CRUD (สร้าง, อ่าน, แก้ไข, ลบ) กับข้อมูลหนังสือของตนได้
แอปพลิเคชันนี้สร้างขึ้นด้วย Node.js, Express.js และ Cassandra และใช้ EJS สำหรับการสร้างหน้าตาเว็บไซต์

เทคโนโลยีที่ใช้
- Node.js, Express.js
- Cassandra
- EJS
- CSS
- Docker

วิธีการติดตั้งและใช้งาน
- ติดตั้ง Docker Desktop และ Node.js
- ติดตั้ง image ของ Cassandra ลงบน docker
- ดาวน์โหลดไฟล์โปรเจคใน google drive
- เปิดไฟล์ใน VScode และ รันคำสั่ง npm install ใน terminal
- สร้าง container ของ cassandra และ กำหนดพอร์ท ใน docker
- ทำการรัน container นั้น ใน docker desktop
- สร้าง keyspace ชื่อ book_catalog ด้วยคำสั่ง CREATE KEYSPACE book_catalog WITH replication = {'class': 'SimpleStrategy','replication_factor': 1};
- ใช้คำสั่ง npm start ใน terminal ของ VScode
-  เข้าไปที่ browser และไปยัง http://localhost:3000'
- เข้าใช้งานเว็ปไซต์

การทำงานของไฟล์หลักๆ
1. src/app.js
-ตั้งค่า Express, Session, Body-parser
-เชื่อมต่อ Cassandra
-กำหนดเส้นทาง (bookRoutes, authRoutes)

2. src/controllers/userController.js
-จัดการฟอร์มลงทะเบียน/ล็อกอิน
-สมัคร, ล็อกอิน, ล็อกเอาท์ผู้ใช้
-ใช้ฟังก์ชันจาก UserModel จัดการข้อมูลใน Cassandra

3. src/controllers/bookController.js
-จัดการเพิ่ม,ดู,แก้ไข,ลบหนังสือ
-ใช้ฟังก์ชันจาก BookModel จัดการข้อมูลใน Cassandra

4. src/models/userModel.js
-ฟังก์ชันสร้างตาราง,สมัคร,ดึงข้อมูลผู้ใช้,ตรวจรหัสผ่าน

5. src/models/bookModel.js
-ฟังก์ชันสร้างตาราง,เพิ่ม,ดู,แก้ไข,ลบหนังสือ

6. src/routes/authRoutes.js
-เส้นทางสำหรับสมัคร, ล็อกอิน, ล็อกเอาท์
-เรียก UserController

7. src/routes/bookRoutes.js
-เส้นทางสำหรับดู, เพิ่ม, แก้ไข, ลบหนังสือ
-เรียก BookController

8. src/middleware/auth.js
-ตรวจสอบและเปลี่ยนเส้นทางไป /auth/login ถ้าไม่ได้ล็อกอิน

9. views/
-โฟลเดอร์เก็บไฟล์ EJS
-มีหน้าลงทะเบียน,ล็อกอิน,เพิ่ม/แก้ไข/แสดงหนังสือ
-ใช้ layouts/main.ejs เป็นเทมเพลตรวม

10. docker-compose.yml
-ตั้งค่า Cassandra บน Docker
-เปิดพอร์ต 9042 ให้แอปเชื่อมต่อ

11. Dockerfile
-สร้าง Docker image สำหรับ Node.js
-ติดตั้ง dependencies และรัน app.js

12. package.json
-ข้อมูลโปรเจกต์ เช่น dependencies,ชื่อ