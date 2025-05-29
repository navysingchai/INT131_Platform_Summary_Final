# System Calls and Memory Hierarchy

## 1. System Calls

### What are System Calls?

System calls provide a **programming interface** to the services provided by the operating system.  
They are essential for **protection**, as they prevent user programs from directly accessing sensitive hardware or kernel functions.

System call คือวิธีที่โปรแกรมติดต่อกับบริการของระบบปฏิบัติการ โดยไม่ให้โปรแกรมเข้าไปยุ่งกับฮาร์ดแวร์โดยตรงเพื่อความปลอดภัย

---

### Types of OS Services Accessed via System Calls
- Program execution  
- I/O operations  
- File manipulation  
- Communications between processes  
- Error detection  
- Resource allocation  
- Protection and security

ตัวอย่างสิ่งที่ process ขอจากระบบปฏิบัติการ เช่น การเปิดไฟล์ รันโปรแกรม หรือจัดการหน่วยความจำ

---

### API – System Call – OS Relationship

Most programs use a **high-level API** to indirectly invoke system calls.  
Common APIs include:
- WinAPI (Windows)
- POSIX API (Unix/Linux/Mac)
- Java API (JVM)

API คือชุดคำสั่งระดับสูงที่แปลงไปเป็น system call เพื่อให้โปรแกรมสามารถใช้บริการของ OS ได้ง่ายขึ้น

---

### Dual-Mode Operation

To protect system resources, CPUs operate in **two modes**:
- **User Mode**: Restricted access
- **Kernel Mode**: Full access (privileged)

เมื่อมีการเรียก system call โหมดจะเปลี่ยนเป็น kernel mode  
เมื่อทำงานเสร็จจะสลับกลับเป็น user mode

---

## 2. Interrupts

### Polling vs Interrupts

**Polling**: CPU checks device status repeatedly (busy-waiting).  
- Efficient for fast devices  
- Wasteful for slow ones

**Interrupts**: Devices signal the CPU when they are ready.  
- CPU handles other tasks in the meantime  
- Uses interrupt request (IRQ) line

Polling คือการที่ CPU ถามอุปกรณ์ซ้ำ ๆ ว่าพร้อมหรือยัง  
Interrupt ช่วยให้ CPU ทำงานอื่นได้จนกว่าจะถูกเรียก

---

### Exceptions and Traps

Exceptions คือข้อผิดพลาดจากซอฟต์แวร์ เช่น divide-by-zero  
Traps คือ software interrupt ที่ใช้ในการเรียก system call

หากเกิด exception ระบบอาจต้องยุติ process หรือปิดโปรแกรม

---

### Timer

Timer interrupt is used to:
- Prevent infinite loops
- Allow OS to regain control

ตัวจับเวลาช่วยให้ OS ไม่โดน process ใด process หนึ่งแย่งใช้ CPU ตลอดไป

---

## 3. Basic Memory Concepts

### Memory Characteristics

Key characteristics of memory:
- **Type**: RAM, ROM  
- **Location**: Internal/External to CPU  
- **Access method**: Sequential, Direct, Random, Associative  
- **Performance**: Access time, Transfer rate

หน่วยความจำมีหลายแบบ และใช้วิธีการเข้าถึงที่แตกต่างกัน

---

### RAM (Random Access Memory)

- Volatile (ข้อมูลหายเมื่อปิดเครื่อง)
- Read/Write capable
- Temporary storage

แบ่งเป็น:
- **DRAM**: ใช้ประจุไฟฟ้า ต้อง refresh ตลอดเวลา ใช้เป็น main memory
- **SRAM**: ใช้สวิตช์เก็บข้อมูล เร็วกว่า ไม่ต้อง refresh ใช้ใน cache

---

### ROM (Read Only Memory)

- Non-volatile  
- Stores firmware/BIOS  
- Types: ROM, PROM, EPROM, EEPROM, Flash

ข้อมูลใน ROM ไม่หายแม้ปิดเครื่อง ใช้เก็บโปรแกรมพื้นฐานที่จำเป็น

---

### Access Methods

- **Sequential**: อ่านตามลำดับ เช่นเทป  
- **Direct**: เข้าถึงโดยใช้ตำแหน่ง เช่นดิสก์  
- **Random**: เข้าถึงจุดใดก็ได้ เช่น RAM  
- **Associative**: ค้นหาด้วยการเปรียบเทียบ เช่น cache

---

### Memory Hierarchy

หน่วยความจำถูกจัดเป็นลำดับจากเร็วที่สุดไปช้าที่สุด เช่น:
1. Register  
2. Cache  
3. Main Memory (RAM)  
4. Secondary Storage (Disk)  
5. Tertiary Storage (Tape, Archive)

ยิ่งใกล้ CPU ยิ่งเร็ว แต่มีขนาดน้อยและราคาแพง

---

## 4. Cache

### Locality of Reference

There are three types of locality:
- **Temporal**: ข้อมูลที่เพิ่งใช้มักถูกใช้ซ้ำ
- **Spatial**: ข้อมูลใกล้กันมักถูกเรียกใช้ต่อกัน
- **Sequential**: คำสั่งมักถูกรันแบบเรียงลำดับ

---

### Cache Architecture

- **Direct mapping**: แต่ละ block จาก main memory ถูกแมพไปตำแหน่งใน cache  
- **Cache hit**: พบข้อมูลใน cache  
- **Cache miss**: ไม่พบ ต้องไปหาใน memory

ประสิทธิภาพของ cache ขึ้นกับ:
- **Hit rate**: ความถี่ที่เจอข้อมูล
- **Miss penalty**: เวลาที่เสียไปเมื่อไม่พบข้อมูล

---
