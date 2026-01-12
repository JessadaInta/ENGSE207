# Library Management System - Layered Architecture

## 📋 Project Information
- **Student Name:** เจษฎา อินตา
- **Student ID:** 67543210006-2
- **Course:** ENGSE207 Software Architecture

## 🏗️ Architecture Style
Layered Architecture (3-tier)

---

## 📂 Project Structure

midterm-individual-675432100062/
├── src/
│   ├── presentation/              # Layer 1: Presentation
│   │   ├── routes/
│   │   │   └── bookRoutes.js       # กำหนด routes
│   │   ├── controllers/
│   │   │   └── bookController.js   # Handle HTTP requests/responses
│   │   └── middlewares/
│   │       └── errorHandler.js     # Error handling middleware
│   │
│   ├── business/                  # Layer 2: Business Logic
│   │   ├── services/
│   │   │   └── bookService.js      # Business logic & rules
│   │   └── validators/
│   │       └── bookValidator.js    # Validation logic
│   │
│   └── data/                      # Layer 3: Data Access
│       ├── repositories/
│       │   └── bookRepository.js   # Database operations
│       └── database/
│           └── connection.js       # Database connection
│
├── server.js                      # Entry point
├── package.json
├── library.db                     # SQLite database
└── README.md                      # Documentation

---

## 🎯 Refactoring Summary

### ปัญหาของ Monolithic (เดิม):
- โค้ดทั้งหมดอยู่ในไฟล์เดียว ทำให้โค้ดซับซ้อนและอ่านยาก
- Business Logic, SQL และ HTTP logic ปะปนกัน
- แก้ไขหรือเพิ่มฟีเจอร์ได้ยาก เสี่ยงกระทบส่วนอื่น
- ไม่สามารถทดสอบแต่ละส่วนแยกกันได้
- การบำรุงรักษาในระยะยาวทำได้ยาก

### วิธีแก้ไขด้วย Layered Architecture:
- แยกโค้ดออกเป็น 3 Layer ตามหน้าที่ชัดเจน
- Presentation Layer รับผิดชอบเฉพาะ HTTP และ routing
- Business Logic Layer ดูแล validation และกฎทางธุรกิจ
- Data Access Layer จัดการฐานข้อมูลและ SQL เท่านั้น
- ลดการพึ่งพากันระหว่างแต่ละส่วน (Loose Coupling)

### ประโยชน์ที่ได้รับ:
- โค้ดอ่านง่าย เป็นระเบียบ และเข้าใจโครงสร้างระบบได้ชัดเจน
- แก้ไขหรือเพิ่มฟีเจอร์ใหม่ได้ง่าย
- สามารถทดสอบแต่ละ Layer แยกจากกันได้
- ลดความเสี่ยงในการเกิด bug จากการแก้ไขโค้ด
- รองรับการขยายระบบในอนาคตได้ดี

---

## 🚀 How to Run

```bash
# 1. Clone repository
git clone [your-repo-url]

# 2. Install dependencies
npm install

# 3. Run server
npm start

# 4. Test API
# Open browser: http://localhost:3000
📝 API Endpoints
📚 Book APIs
Method	Endpoint	Description
GET	/books	ดึงรายการหนังสือทั้งหมด
GET	/books?status=available	ดึงหนังสือตามสถานะ
GET	/books/:id	ดึงข้อมูลหนังสือตาม ID
POST	/books	เพิ่มหนังสือใหม่
PUT	/books/:id	แก้ไขข้อมูลหนังสือ
PATCH	/books/:id/status	เปลี่ยนสถานะหนังสือ (available / borrowed)
DELETE	/books/:id	ลบหนังสือ (ต้องไม่ถูกยืมอยู่)

✅ Conclusion
ระบบ Library Management System นี้ถูกออกแบบด้วย Layered Architecture
เพื่อให้โค้ดมีโครงสร้างชัดเจน แยกความรับผิดชอบอย่างเหมาะสม
ทำให้ระบบมีความยืดหยุ่น ดูแลรักษาง่าย และพร้อมสำหรับการพัฒนาในอนาคต