# Virtual Memory 

---

## 1. Review of Memory Hardware

- **Memory Hierarchy**  
  หน่วยความจำมีลำดับชั้น เช่น register, cache, main memory, secondary storage  
  แต่ละระดับมีความเร็วและขนาดต่างกัน

- **Memory Access**  
  - Register access เร็วมาก (1 cycle)
  - Main memory ใช้หลาย cycle → เกิด stall
  - Cache อยู่ระหว่าง CPU กับ main memory

- **CPU Access**  
  CPU เข้าถึงได้เฉพาะ register และ main memory  
  หน่วยความจำเห็นแค่ address + read/write request

---

## 2. Review of Virtual Memory

- **Process in Memory**  
  - ไม่จำเป็นต้องโหลดโปรแกรมทั้งหมดในหน่วยความจำ
  - มีแค่ส่วนที่ใช้เท่านั้น เช่น error handling, large data ไม่ได้ใช้ตลอด

- **Virtual Memory**  
  - บางส่วนของโปรแกรมเท่านั้นที่ต้องอยู่ใน memory
  - Logical address space > Physical address space

- **Benefits**  
  - รันหลายโปรแกรมพร้อมกัน
  - ลด I/O
  - สร้าง process ได้เร็ว
  - แชร์ address space ระหว่าง process ได้

---

## 3. Memory Management Concept

- **Goals of Memory Management**  
  - รองรับ multiprogramming, time-sharing
  - แบ่งใช้ memory, ใช้ให้คุ้มค่า, performance ดี

- **Memory Manager Tasks**  
  - จัดสรร/คืน memory
  - ติดตาม memory ทั้งที่ใช้แล้วและยังว่าง
  - ถ้า memory ไม่พอ ต้อง swap in/out
  - ป้องกันการเข้าถึงผิดพลาด

- **Address Types**  
  - **Logical Address**: ที่ CPU สร้าง (virtual address)
  - **Physical Address**: ที่ memory unit เห็น

- **Binding**  
  การแปลง logical เป็น physical address  
  มี 3 แบบ:
  1. Compile time
  2. Load time
  3. Execution time (ใช้ใน Virtual Memory)

- **MMU (Memory Management Unit)**  
  ฮาร์ดแวร์ที่แปลง logical → physical address ตอนรันจริง

- **Protection**  
  ใช้ base-register และ limit-register จำกัดพื้นที่ของแต่ละ process

---

## 4. Memory Paging

- **Contiguous Allocation**  
  แต่ละ process อยู่ในพื้นที่ต่อเนื่อง → เกิดปัญหา fragmentation

- **Fragmentation**  
  - **External**: มีช่องว่างแต่ไม่ติดกัน
  - **Internal**: มี memory ที่ไม่ได้ใช้ใน block ที่จองไว้

- **Compaction**  
  รวมช่องว่างภายนอกให้ติดกัน  
  ต้องใช้ dynamic relocation

- **Paging**  
  - แบ่ง logical memory → pages  
  - แบ่ง physical memory → frames  
  - หลีกเลี่ยง external fragmentation

- **Page vs Frame**  
  ขนาด page = ขนาด frame  
  อาจเกิด internal fragmentation ได้  
  ใช้ page table แปลง logical → physical

- **Shared Code**  
  Code ที่อ่านอย่างเดียวใช้ร่วมกันได้ เช่น editor, compiler

- **Private Code and Data**  
  แต่ละ process มีสำเนาของตัวเอง

---

## 5. More on Virtual Memory

- **Page Table Storage**  
  เก็บใน memory → ต้อง access memory 2 ครั้ง  
  ใช้ TLB (Translation Lookaside Buffer) ช่วยเร่ง

- **Backing Store**  
  ใช้สำหรับเก็บ page ที่ยังไม่โหลดเข้าหน่วยความจำ

- **Demand Paging**  
  - โหลด page เฉพาะเมื่อจำเป็น
  - ลด I/O, เร็วขึ้น, ใช้ memory น้อย
  - ต้องมีการจัดการ page fault

- **Page Fault**  
  - ถ้า reference ไปยัง page ที่ไม่มีใน memory
  - ถ้า invalid → abort  
  - ถ้า valid → โหลดจาก disk

- **Page Fault Handling Steps**  
  1. Reference ไปยังตัวแปร
  2. Hardware เจอว่าไม่มีใน memory → trap
  3. OS ตรวจว่าถูกต้อง → หา page → หาที่ว่าง → โหลด → update table → restart

- **Performance of Demand Paging**  
  - EAT = (1–p) x memory access + p x (fault overhead + swap out + swap in)
  - ถ้า p สูง → ระบบช้า

- **Locality**  
  - กลุ่มของ page ที่ถูกใช้งานใกล้กัน
  - Temporal, Spatial, Sequential Locality

- **Thrashing**  
  - ถ้า locality ใหญ่กว่า memory → page fault rate สูงมาก

---

## Summary

- Virtual memory ช่วยให้ไม่ต้องโหลดทุกอย่างเข้าหน่วยความจำ
- ใช้ MMU สำหรับ binding และ protection
- Paging แก้ปัญหา fragmentation ได้
- ใช้ Demand Paging เพื่อลดการใช้ memory และ I/O
- การจัดการ locality และลด thrashing สำคัญต่อ performance
