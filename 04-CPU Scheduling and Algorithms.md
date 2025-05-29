# CPU Scheduling and Algorithms

## 1. Context Switching

When the CPU switches from one process to another, the system must save the state of the current process and load the saved state of the next.  
This state is stored in the Process Control Block (PCB).

เมื่อ CPU เปลี่ยนจาก process หนึ่งไปยังอีก process หนึ่ง ระบบต้องบันทึกสถานะของ process เดิม และโหลดสถานะของ process ใหม่  
สถานะนี้ถูกจัดเก็บไว้ใน PCB (Process Control Block)

Context switch ใช้เวลาและเป็น overhead ซึ่งหมายถึงช่วงเวลาที่ CPU ไม่ได้ทำงานจริง  
ระยะเวลาในการสลับขึ้นอยู่กับการสนับสนุนจากฮาร์ดแวร์

---

## 2. Process States

A process may be in one of several states:
- New
- Ready
- Running
- Waiting/Blocked
- Terminated

process หนึ่งสามารถอยู่ในสถานะใหม่ พร้อมใช้งาน กำลังทำงาน รอ หรือสิ้นสุด  
ไม่สามารถอยู่หลายสถานะพร้อมกันได้ใน processor แบบ single-core

---

## 3. CPU Scheduling

Scheduling is needed when more than one process is in the ready state.  
The scheduler selects one process to allocate the CPU.

การจัดตารางการทำงานของ CPU จะเลือก process ที่พร้อมใช้งาน เพื่อใช้ CPU  
การเปลี่ยน context ต้องรวดเร็วเพราะเกิดบ่อยทุกไม่กี่ millisecond

---

## 4. Scheduling Criteria

- CPU utilization: maximize CPU usage
- Throughput: number of completed processes per unit time
- Waiting time: time a process waits in ready queue
- Response time: time from request to first response
- Fairness: equal opportunity for processes

เกณฑ์ในการเลือกอัลกอริธึมมีทั้งประสิทธิภาพ ความเร็ว ความยุติธรรม และเวลารอคอยของแต่ละ process

---

## 5. Scheduling Algorithms

### First-Come, First-Served (FCFS)
- Processes executed in order of arrival
- Non-preemptive
- Simple but can cause long waiting times

ตัวอย่าง:
```
P1 (24) → P2 (3) → P3 (3)
Average waiting time = (0 + 24 + 27)/3 = 17
```

### Shortest-Job-First (SJF)
- Process with shortest burst time is selected
- Non-preemptive
- Can significantly reduce waiting time

ตัวอย่าง:
```
P4 (3) → P1 (6) → P2 (8) → P3 (7)
Average waiting time = (3 + 16 + 9 + 0) / 4 = 7
```

### Round Robin (RR)
- Each process gets a small unit of CPU time (quantum)
- Preemptive
- Fair for all, avoids starvation

ตัวอย่าง:
```
P1, P2, P3, P4 with q = 20
Average waiting time = 73
```

### Priority Scheduling
- Each process assigned a priority
- Process with highest priority executes first
- Can be preemptive or non-preemptive

ตัวอย่าง:
```
P2 (priority 1) → P5 (2) → P1 (3) → P3 (4) → P4 (5)
Average waiting time = 8.2
```

---

## 6. Summary

| Algorithm | Key Feature | Weakness |
|-----------|-------------|----------|
| FCFS      | Simple      | Long wait for large tasks |
| SJF       | Optimal avg waiting time | Needs burst time prediction |
| RR        | Fair        | High context switch overhead |
| Priority  | Prioritized execution | Starvation possible |

อัลกอริธึมแต่ละแบบมีจุดเด่นและจุดด้อยต่างกัน ขึ้นอยู่กับสถานการณ์และความต้องการของระบบ

---

> Source: Operating System Concepts, 10th Edition, Silberschatz, Galvin, Gagne (2018)
