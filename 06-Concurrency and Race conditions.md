# Concurrency and Race Conditions

## 1. Background

Modern software commonly uses multiprocessing and multithreading.  
- **Processes** may share memory or communicate via files/messages.  
- **Threads** share memory directly.

ซอฟต์แวร์ยุคใหม่ใช้หลาย process และ thread เพื่อให้ทำงานได้พร้อมกัน  
เธรดสามารถแชร์หน่วยความจำกันได้โดยตรง ทำให้ประสานงานกันได้เร็วขึ้น

---

## 2. LAB – Processes

### fork() and exec()

- `fork()` creates a new child process  
- `exec()` replaces process memory with a new program  
- `wait()` is used by the parent to wait for the child to finish

`fork()` ใช้ในการสร้าง process ใหม่ ส่วน `exec()` ใช้รันโปรแกรมใหม่ใน process เดิม  
`wait()` ช่วยให้ parent รอ child ทำงานเสร็จ

### Example Programs
- `helloWithPID`: แสดงข้อความจากทั้ง parent และ child
- `helloWithPIDWait`: รอ child เสร็จก่อน parent จะพิมพ์ข้อความ
- `printAB`: สั่งให้แต่ละ process พิมพ์ `a` หรือ `b`
- `helloThailand`: child เปลี่ยนค่าตัวแปรใน memory ของตัวเอง

---

## 3. LAB – Threads

### pthread_create() and pthread_join()

ใช้ในการสร้าง thread ใหม่และรอให้ thread นั้นจบการทำงาน  
ตัวอย่าง: `helloThailandThread` เปลี่ยนค่าตัวแปรจาก thread

---

## 4. Race Conditions

### Definition

A **race condition** occurs when multiple processes/threads access and modify shared resources concurrently and the outcome depends on the order of execution.

Race condition คือสถานการณ์ที่ผลลัพธ์ของโปรแกรมขึ้นอยู่กับลำดับการทำงานของ thread/process ซึ่งอาจไม่แน่นอน

---

### Example: Producer-Consumer

Producer สร้างข้อมูล Consumer อ่านข้อมูล  
ถ้าไม่จัดการดี อาจเกิดการชนกัน เช่น buffer เต็ม หรือไม่มีข้อมูลให้ consumer อ่าน

---

### Shared Counter Problem

**Single-threaded version**: Count เพิ่มตามคาด  
**Multi-threaded (concurrent)**: Count น้อยกว่าที่ควรเพราะ thread แย่งกันเขียน  
**Pseudo-parallelism**: Thread ทำงานสลับกันใน CPU เดียว

---

### Why does it happen?

Consider this instruction: `counter++`

เบื้องหลังอาจแปลเป็นหลายคำสั่ง เช่น
1. อ่าน counter ไปไว้ใน register  
2. บวก 1  
3. เขียนกลับไปที่ counter

ถ้า thread ถูกสลับระหว่างขั้นตอนเหล่านี้ ข้อมูลอาจหาย

---

### Banking Example

T1: ฝากเงิน 500  
T2: ถอนเงิน 1000  
หากทำพร้อมกันโดยไม่ sync อาจเกิดการถอนเงินเกินยอดได้

---

## 5. Solutions to Race Conditions

### Critical Section

- A part of code where shared resources are modified  
- Only one thread/process can enter at a time

Critical Section คือช่วงของโค้ดที่ห้ามหลาย thread เข้าไปทำงานพร้อมกัน

### Atomic Instruction / Transaction

- Perform operations as indivisible units  
- Ensure data consistency

การทำให้คำสั่งทำงานแบบ "อะตอม" หมายถึงทำทั้งหมดหรือไม่ทำเลย เพื่อป้องกันผลลัพธ์ผิดพลาด

---

### Example: Atomic Banking

Deposit:
1. อ่านยอดเงิน
2. เพิ่มเงิน
3. เขียนกลับ

Withdraw:
1. อ่านยอดเงิน
2. เช็คว่าถอนได้ไหม
3. หักเงิน
4. เขียนกลับ

การทำงานแบบนี้ต้องแน่ใจว่าไม่มี process อื่นเข้าไปอ่านหรือเขียนค่าระหว่างกลาง

---
