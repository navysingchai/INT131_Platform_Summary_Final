# Fetch-Decode-Execute Cycle

## 1. Overview

The **Fetch-Decode-Execute Cycle** is the process by which a computer retrieves, interprets, and executes instructions. This is fundamental to how a CPU operates.

**วงจรการดึง–ถอดรหัส–ดำเนินการ** คือกระบวนการที่คอมพิวเตอร์ดึงคำสั่งจากหน่วยความจำ ถอดรหัส และดำเนินการตามคำสั่งนั้น เป็นหัวใจสำคัญของการทำงานของ CPU

---

## 2. The Cycle Steps

### Step 1: Fetch

The control unit fetches the next instruction from memory or cache located at the Program Counter (PC) and stores it in the Instruction Register (IR).

หน่วยควบคุมจะดึงคำสั่งถัดไปจากหน่วยความจำหรือแคชที่ระบุโดย Program Counter (PC) แล้วเก็บไว้ใน Instruction Register (IR)

### Step 2: Decode

The instruction is decoded into a language that the ALU can understand.

คำสั่งจะถูกแปลให้อยู่ในรูปแบบที่ ALU (หน่วยคำนวณและตรรกะ) เข้าใจได้

### Step 3: Get (Operands)

Any data operands required to execute the instruction are fetched from memory and placed into registers within the CPU.

ถ้าคำสั่งต้องใช้ข้อมูลเพิ่มเติม ข้อมูลจะถูกดึงจากหน่วยความจำมาใส่ไว้ในรีจิสเตอร์ภายใน CPU

### Step 4: Execute

The ALU executes the instruction and places results in registers or memory.

ALU จะดำเนินการตามคำสั่ง และจัดเก็บผลลัพธ์ไว้ในรีจิสเตอร์หรือหน่วยความจำ

---

## 3. Summary

Each instruction is processed in a cycle of fetch, decode, get, and execute.

คำสั่งแต่ละคำสั่งจะผ่านกระบวนการเป็นรอบ ได้แก่ ดึงคำสั่ง, ถอดรหัส, รับข้อมูล, และดำเนินการ

---
