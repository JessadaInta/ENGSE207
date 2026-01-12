# Library Management System

![Library Management System Architecture](architecture-diagram.png)

## C1: System Context Diagram

- **Actors:** System User (บรรณารักษ์, เจ้าหน้าที่, ผู้ดูแลระบบ)
- **System:** Library Management System
  - จัดการข้อมูลหนังสือ (CRUD)
  - ยืม–คืนหนังสือ
  - กรองหนังสือตามสถานะ (available / borrowed)
- **External Systems:** SQLite Database (`library.db`)

---

## C2: Container Diagram - Layered Architecture

### Presentation Layer 📋
**หน้าที่:**
- รับ HTTP Request  
- Parse parameters  
- เรียก Service  
- ส่ง HTTP Response  

**ไฟล์:**
- `bookRoutes.js` – API endpoints  
- `bookController.js` – HTTP handling  
- `errorHandler.js` – Error handling  

**ห้ามทำ:**
- ❌ เขียน SQL Query  
- ❌ เขียน Business Logic  

### Business Logic Layer 🧠
**หน้าที่:**
- Validation  
- Business Rules  
- Calculations  
- เรียก Repository  

**ไฟล์:**
- `bookService.js` – Business logic  
- `bookValidator.js` – Validation  

**Business Rules:**
- Title, author, isbn required  
- ISBN format ต้องถูกต้อง  
- หนังสือมีสถานะ `available` หรือ `borrowed`  
- หนังสือที่ถูกยืมแล้ว ไม่สามารถลบซ้ำได้  

**ห้ามทำ:**
- ❌ เขียน SQL Query  
- ❌ จัดการ HTTP  

### Data Access Layer 💾
**หน้าที่:**
- CRUD Operations  
- Execute SQL  
- Return data  

**ไฟล์:**
- `bookRepository.js` – CRUD  
- `connection.js` – DB connection  

**Methods:**
- `findAll(status)`  
- `findById(id)`  
- `create(bookData)`  
- `update(id, bookData)`  
- `updateStatus(id, status)`  
- `delete(id)`  

**ห้ามทำ:**
- ❌ Business Logic  
- ❌ Validation  

---

## Data Flow: Create Book

**Client → Controller → Service → Repository → Database**  
↓ parse ↓ validate ↓ SQL ↓ insert  
← response ← ← ← ← ← ← ← ← ← ←

**Steps:**
1. Client ส่ง POST request พร้อมข้อมูลหนังสือ  
2. Controller parse request → เรียก Service  
3. Service validate ข้อมูลและ ISBN → เรียก Repository  
4. Repository execute SQL INSERT  
5. Database insert record  
6. Response กลับไปยัง Client  

---

## Summary

**Architecture Benefits:**
- ✅ Separation of Concerns – แยก layer ชัดเจน  
- ✅ Maintainability – แก้ไขง่าย  
- ✅ Testability – Test แยก layer ได้  
- ✅ Scalability – ขยายง่าย  

**Key Principles:**
- Each layer has clear responsibilities  
- Dependencies flow downward  
- No layer skipping  
- Business rules stay in Business Layer
