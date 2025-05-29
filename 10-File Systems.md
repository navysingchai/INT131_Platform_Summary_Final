# File Systems - Detailed Summary (INT131 Class 10)
---

## 1. File Attributes

- **What is a File?**  
  ไฟล์คือข้อมูลที่มีชื่อและมีความสัมพันธ์กัน ซึ่งถูกบันทึกใน secondary storage  
  สำหรับผู้ใช้ ไฟล์คือหน่วยข้อมูลที่เล็กที่สุดในระบบจัดเก็บแบบตรรกะ

- **File Contents**  
  ไฟล์ประกอบด้วย bit, byte, line, หรือ record แล้วแต่ผู้สร้างกำหนดความหมาย

- **File Attributes**  
  - **Name**: ชื่อของไฟล์ (อ่านได้โดยมนุษย์)  
  - **Identifier**: หมายเลขเฉพาะในระบบ  
  - **Type**: ประเภทของไฟล์ เช่น `.txt`, `.jpg`  
  - **Time/Date/User ID**: ใช้ตรวจสอบการใช้งานและความปลอดภัย  
  - **Location**: ตำแหน่งไฟล์บนอุปกรณ์  
  - **Size**: ขนาดไฟล์จริง

- **Blocks and Clusters**  
  - การอ่าน/เขียนข้อมูลบนดิสก์ใช้หน่วยที่เรียกว่า **block**  
  - หลาย block รวมกันเรียกว่า **cluster** (เช่น NTFS ใช้ 4KB ต่อ cluster)

- **Size on Disk**  
  ขนาดไฟล์จริงอาจเล็กกว่าพื้นที่ที่ใช้จริงบนดิสก์ เพราะใช้พื้นที่เป็น block หรือ cluster

- **Advanced Attributes & Permissions**  
  - **Protection**: สิทธิ์ในการอ่าน เขียน หรือรัน

---

## 2. Directories

- **Directory Structure**  
  เป็นโครงสร้างที่เก็บข้อมูลเกี่ยวกับไฟล์ทั้งหมด เช่น ชื่อ ตำแหน่ง ขนาด  
  ทั้ง directory และไฟล์ถูกเก็บอยู่ในดิสก์

- **File-System Organization**  
  ระบบไฟล์จะจัดโครงสร้างของ directory และไฟล์เป็นลำดับขั้นเพื่อความง่ายในการค้นหาและจัดการ

---

## 3. File Operations

- **File Operations**  
  - **Create**: สร้างไฟล์ใหม่  
  - **Delete**: ลบไฟล์  
  - **Read**: อ่านข้อมูลที่ตำแหน่ง read pointer  
  - **Write**: เขียนข้อมูลที่ตำแหน่ง write pointer  
  - **Seek**: เปลี่ยนตำแหน่ง pointer ในไฟล์ (reposition)

- **Create File Steps**  
  1. หาเนื้อที่ว่าง  
  2. สร้าง entry ใน directory

- **Delete File Steps**  
  1. หาไฟล์ใน directory  
  2. คืนพื้นที่  
  3. ลบ entry

- **Read/Write**  
  ต้องรู้ตำแหน่งใน storage และตำแหน่งใน memory ที่ใช้

- **Seek**  
  เปลี่ยนตำแหน่ง pointer โดยไม่จำเป็นต้องอ่าน/เขียนจริง

---

## 4. Directory Operations

- **Operations**  
  - ค้นหาไฟล์ (Search)  
  - แสดงรายการไฟล์ (List)  
  - สร้าง/ลบ/คัดลอก/ย้าย/เปลี่ยนชื่อไฟล์  
  - Traverse ทั้งระบบ (find, cp, du)

- **Move vs Copy**  
  การย้าย (move) ไฟล์ในที่เดียวกันจะเร็วกว่า copy เพราะแค่เปลี่ยน pointer

---

## 5. Directory Properties

- **Acyclic-Graph Directory**  
  - ไฟล์หรือ directory สามารถแชร์กันได้  
  - ใช้ **symbolic link** (ลิงก์ไปยัง path) หรือ **hard link** (ลิงก์ไปยัง inode)

- **General Graph Directory**  
  - อาจเกิด loop ได้ (เช่น link กลับไปหา parent)  
  - ต้องมีวิธีป้องกัน เช่น count reference หรือ garbage collection

- **Mounting**  
  - ต้องทำการ mount ก่อนใช้ file system  
  - Windows จะ mount อัตโนมัติตอนบูต  
  - รูปแบบ path เช่น `C:\Users\file.txt`

---

## Summary

- ไฟล์คือหน่วยข้อมูลพร้อม attributes เช่น name, type, location  
- Directory คือโครงสร้างที่จัดการไฟล์ในระบบ  
- File operation มีตั้งแต่ create, read, write, seek  
- Directory operation มี traverse, rename, move  
- Property พิเศษ เช่น symbolic link, mount point เพิ่มความยืดหยุ่นในการจัดเก็บ
