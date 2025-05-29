# Multitasking Mechanism

## 1. Background

In von Neumann architecture, instructions and data are stored in the same memory.  
The CPU processes binary machine instructions sequentially and uses a few internal registers.  
Memory access is slow, so cache and prefetch units help improve performance.

ในสถาปัตยกรรม von Neumann คำสั่งและข้อมูลอยู่ในหน่วยความจำเดียวกัน  
CPU ดำเนินคำสั่งแบบลำดับ และต้องใช้ register และหน่วยความจำร่วมกัน  
หน่วยความจำช้ากว่า CPU มาก จึงต้องใช้ cache และ prefetch ช่วยเร่งความเร็ว

---

## 2. Evolution of Multitasking

### 1st Generation
- No OS, only assembler/loader
- Parameters manually set
- ไม่มีระบบปฏิบัติการ ต้องตั้งค่าด้วยตนเอง

### 2nd Generation
- Batch jobs: multiple jobs submitted, executed one at a time
- ระบบทำงานแบบ batch โดยไม่ต้องมีผู้ใช้โต้ตอบ

### 3rd Generation
- Multiprogramming: several jobs loaded, executed alternately
- Terminal introduced for user I/O
- จัดสรรงานให้ CPU ทำเสมอโดยไม่ปล่อยให้ว่าง

### 4th Generation
- Timesharing: illusion of a separate machine for each user
- Multitasking: efficient resource use in single-user environment
- ใช้แนวคิด virtual machine ต่อผู้ใช้แต่ละคน และแชร์ resource

---

## 3. Concepts

### Process
- A program in execution
- Needs CPU, memory, I/O, storage
- Runs sequentially; no parallel execution for a single-threaded process

โปรแกรมที่กำลังทำงานคือ process ซึ่งต้องใช้ทรัพยากรหลายอย่าง และทำงานทีละคำสั่งเท่านั้น

### Concurrency
- Several processes may be in memory at once
- Parallelism possible with multiple cores
- Concurrent execution creates illusion of parallelism

การประมวลผลพร้อมกันสามารถเกิดขึ้นได้หากมีหลาย core

---

## 4. Context Switching

When the CPU switches from one process to another:
- The current process state is saved (in PCB)
- The new process state is loaded

Context switch เป็นกระบวนการที่บันทึกสถานะของ process เก่า และโหลดสถานะของ process ใหม่  
เวลาที่ใช้ในการสลับ process ถือเป็น overhead เพราะไม่เกิดการทำงานจริง

### Process Control Block (PCB) Contains:
- Program Counter, CPU registers
- CPU scheduling info (priority, queue pointers)
- Memory usage info
- I/O status (allocated devices, open files)

PCB คือโครงสร้างที่เก็บข้อมูลของ process เช่น ตำแหน่งคำสั่งที่ทำอยู่, การจัดสรรหน่วยความจำ, สถานะ I/O

---

## 5. Summary

| Concept           | Description |
|------------------|-------------|
| Batch System     | Run jobs sequentially |
| Multiprogramming | Run multiple jobs concurrently to optimize CPU |
| Timesharing      | Create illusion of personal machine for each user |
| Multitasking     | Share resources among programs efficiently |

ระบบ Batch ทำงานทีละงาน  
Multiprogramming และ Timesharing ทำให้ระบบใช้ทรัพยากรได้คุ้มค่า  
Multitasking คือการบริหารจัดการ resource ที่มีประสิทธิภาพสำหรับโปรแกรมหลายตัว

---
