# Multi-threading and Parallel Computing

## 1. Threads

### What is a Thread?

A thread is the smallest unit of execution within a process.  
While a process is a "heavyweight" structure containing its own memory and resources, a thread is "lightweight" and shares resources with other threads in the same process.

เธรดคือหน่วยย่อยของการทำงานภายในโปรเซส  
โปรเซสมีทรัพยากรของตัวเอง ส่วนเธรดใช้ทรัพยากรร่วมกับเธรดอื่นในโปรเซสเดียวกัน

---

### Motivation

In an application, there are multiple tasks like:
- Updating display
- Fetching data
- Spell checking
- User input

In a single-threaded process, only one task runs at a time.  
To run tasks concurrently without creating multiple processes, we use threads.

ในโปรแกรมหนึ่งมีหลายงาน เช่น แสดงผล รับข้อมูล ตรวจคำผิด ซึ่งการใช้หลายเธรดจะช่วยให้ทำงานพร้อมกันได้โดยไม่ต้องใช้หลายโปรเซส

---

### Multi-threaded Process

A process can have multiple threads, each with:
- Thread ID
- Thread state
- CPU registers
- Stack

All threads share:
- Data
- Files
- Global variables

แต่ละเธรดมีข้อมูลของตัวเอง เช่น stack และ register  
แต่จะใช้ข้อมูลหลัก เช่น ตัวแปร global และไฟล์ ร่วมกันกับเธรดอื่น

---

### Benefits

**Responsiveness** – UI can remain active while background tasks run  
**Resource Sharing** – Threads use shared memory, less overhead  
**Economy** – Thread creation/switching is cheaper than processes  
**Scalability** – Utilize multi-core systems effectively

ประโยชน์ของการใช้เธรดคือทำให้โปรแกรมตอบสนองเร็ว ใช้ทรัพยากรน้อย และสามารถกระจายงานได้หลาย core

---

## 2. Thread Parallelism

### Concurrency vs Parallelism

- **Concurrency**: Multiple tasks in progress (may not be simultaneous)  
- **Parallelism**: Truly simultaneous execution on multiple cores

Concurrency หมายถึงการจัดการหลายงานในเวลาเดียวกัน (อาจไม่พร้อมกันจริง ๆ)  
Parallelism หมายถึงการทำงานพร้อมกันจริง ๆ บนหลาย core

---

### Single-core vs Multi-core

- On single-core CPUs: Only one thread executes at a time  
- On multi-core CPUs: Multiple threads can execute simultaneously

ระบบที่มีหลาย core จะสามารถรันหลายเธรดได้พร้อมกันจริง ๆ ซึ่งเพิ่มประสิทธิภาพ

---

## 3. Parallel Computing

### Definition

Parallel computing is the simultaneous use of multiple compute resources to solve a computational problem.  
This includes:
- Multi-core CPUs
- Distributed systems connected via networks

การประมวลผลแบบขนานคือการใช้งานทรัพยากรคอมพิวเตอร์หลายตัวพร้อมกัน เพื่อแก้ปัญหาได้เร็วขึ้น

---

### Motivation

- Solve large, complex problems faster
- Process large datasets (Big Data)
- Improve efficiency and reduce cost using smaller processors

เหมาะกับงานที่ต้องใช้พลังการคำนวณสูง เช่น การจำลองสภาพอากาศ การค้นคว้ายา หรือการประมวลผลข้อมูลขนาดใหญ่

---

### How it Works

1. Break problem into smaller parts  
2. Divide parts into instructions  
3. Execute instructions simultaneously  
4. Use control mechanism to coordinate

แยกปัญหาออกเป็นชิ้น ๆ แล้วให้แต่ละ core หรือเครื่องคอมพิวเตอร์ประมวลผลพร้อมกัน

---

## Types of Parallelism

### Instruction-Level Parallelism (ILP)

Within a single core, multiple instructions are executed at different pipeline stages simultaneously.

ใช้การ pipeline เพื่อให้แต่ละคำสั่งอยู่ในขั้นตอนต่าง ๆ พร้อมกัน เช่น fetch, decode, execute

---

### Data-Level Parallelism (DLP)

Same operation is performed on multiple data items simultaneously.  
Example: Applying a filter to multiple pixels at once.

DLP คือการใช้คำสั่งเดียวกับข้อมูลหลายตัว เช่น การปรับแสงภาพหลายพิกเซลพร้อมกัน

---

### Task-Level Parallelism

Different tasks are executed in parallel.  
Example: Web server handling multiple user requests at once.

การแบ่งงานที่ต่างกันให้คอมพิวเตอร์หลายตัวช่วยกันทำ เช่น การให้เซิร์ฟเวอร์ตอบหลาย request พร้อมกัน

---

## Memory Architectures

### Shared Memory

All processors access the same memory.  
Types:
- **UMA (Uniform Memory Access)**: Equal access speed  
- **NUMA (Non-Uniform Memory Access)**: Access speed depends on proximity

ข้อดีคือใช้งานง่ายและเร็ว แต่ขยายระบบได้ยาก  
ต้องเขียนโปรแกรมให้มีการ synchronize หน่วยความจำร่วมกัน

---

### Distributed Memory

Each processor has its own memory.  
Processors communicate via messages.

แต่ละเครื่องมีหน่วยความจำของตนเอง ต้องส่งข้อความระหว่างกันเพื่อสื่อสาร

---

### Hybrid Systems

Combine shared and distributed memory models.  
Used in supercomputers and HPC (High Performance Computing)

เป็นระบบผสม เหมาะกับการใช้งานขนาดใหญ่ เช่น ซูเปอร์คอมพิวเตอร์

---

## Challenges in Parallel Computing

- **Task Decomposition**: แบ่งปัญหาให้เป็นงานย่อย  
- **Data Partitioning**: แบ่งข้อมูลให้แต่ละ processor ทำ  
- **Synchronization**: ให้เธรด/โปรเซสทำงานสอดคล้องกัน  
- **Load Balancing**: แจกจ่ายงานให้เหมาะสมไม่ให้บาง processor ทำงานหนักเกิน

---
