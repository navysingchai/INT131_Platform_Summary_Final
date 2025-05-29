# Input/Output Subsystem - Detailed Summary (INT131 Class 9)

**Instructor**: Olarn Rojanapornpun  
**Date**: Thursday, 15 May 2025  
**Reference**: A. Silberschatz, P.B. Galvin, and G. Gagne, *Operating System Concepts*, 10th ed.

---

## 1. I/O Hardware Basics

- **I/O Hardware**  
  Virtual memory ใช้ disk เป็น backing store  
  ประสิทธิภาพของระบบขึ้นอยู่กับ I/O access time และ throughput  
  อุปกรณ์ I/O มีหลายประเภท เช่น storage, transmission, human-interface

- **Device Port**  
  จุดเชื่อมต่อของอุปกรณ์เข้ากับคอมพิวเตอร์

- **PC Bus Structure**  
  - **System/Memory bus** เชื่อม CPU ↔ RAM  
  - **I/O bus** เช่น PCIe เชื่อม CPU ↔ peripherals  
  - Expansion bus สำหรับอุปกรณ์ที่ช้ากว่า  
  - SAS (Serial Attached SCSI) ใช้กับ server ประสิทธิภาพสูง

- **Controller**  
  - ควบคุม port, bus, device  
  - อาจเป็นชิปในเมนบอร์ดหรือบอร์ดแยก (host adapter)  
  - มี processor, microcode, memory ภายใน

- **I/O Registers**  
  อุปกรณ์มี register สำหรับรับคำสั่ง/ข้อมูล เช่น:  
  - data-in, data-out, status, control register

- **Programmed I/O (Polling)**  
  ใช้ CPU เช็ค status และเขียนข้อมูลทีละ byte  
  เสีย CPU time เยอะ ไม่เหมาะกับข้อมูลปริมาณมาก

- **Memory-Mapped I/O**  
  Mapping register ของอุปกรณ์ไว้ใน address space ของ processor  
  ใช้สำหรับ address space ขนาดใหญ่ เช่น graphics card

- **Interrupt-Driven I/O**  
  อุปกรณ์ส่งสัญญาณ interrupt เมื่อพร้อมใช้งาน  
  CPU ตรวจสอบและเรียก handler มาทำงาน

- **Direct Memory Access (DMA)**  
  - ใช้ processor พิเศษทำ I/O แทน CPU  
  - ข้อมูลไหลตรงจาก I/O → memory โดยไม่ผ่าน CPU

---

## 2. Characteristics of I/O Devices

- **Character Devices**  
  ส่งข้อมูลเป็น byte ละตัว เช่น keyboard, mouse, printer  
  ทำงานแบบ interrupt-driven ได้ดี

- **Block Devices**  
  ส่งข้อมูลเป็นกลุ่ม เช่น disk, tape  
  ใช้คำสั่ง read, write, seek  
  รองรับ memory-mapped file access และ demand paging

- **Synchronous vs Asynchronous**  
  - **Synchronous**: ตอบสนองได้ตามเวลาที่กำหนด เช่น SDRAM  
  - **Asynchronous**: ตอบสนองไม่แน่นอน เช่น keyboard, network

- **Sharable vs Dedicated**  
  - **Sharable**: ใช้ได้หลาย process พร้อมกัน เช่น memory  
  - **Dedicated**: ใช้ได้ครั้งละ process เดียว เช่น printer

---

## 3. I/O Subsystem

- **Goals**  
  - จัดการ I/O อย่างมีประสิทธิภาพ  
  - ควบคุม resource allocation/deallocation  
  - ป้องกันการเข้าถึงที่ไม่ปลอดภัย

---

## 4. Application I/O Interface

- **Challenges**  
  - อุปกรณ์ I/O หลากหลาย ทำให้ OS พัฒนายาก  
  - ต้องมีระบบที่รองรับการเพิ่มอุปกรณ์ใหม่โดยไม่ต้องแก้ OS  
  - ต้องมี interface เดียวที่ง่ายต่อ application

- **Solutions**  
  - ใช้ system call เพื่อ encapsulate พฤติกรรมอุปกรณ์  
  - Device driver ช่วย abstract ความแตกต่างของ controller  
  - หากใช้ protocol ที่รองรับอยู่แล้ว เช่น SATA ไม่ต้องเขียนใหม่  
  - แต่ละ OS มีระบบ driver framework ของตัวเอง

---

## 5. I/O Subsystem Services

- **I/O Services** ที่ Kernel ให้:
  - **Scheduling**: จัดลำดับคำขอเพื่อเพิ่ม performance และลดรอ
  - **Buffering**: เก็บข้อมูลชั่วคราวระหว่างอุปกรณ์/CPU  
    → จัดการ speed mismatch หรือขนาดการส่งข้อมูลไม่เท่ากัน
  - **Caching**: เก็บสำเนาข้อมูลไว้ในหน่วยความจำเร็ว เช่น CPU cache, disk cache
  - **Spooling**: เก็บคำขอ output ไว้ก่อน เช่น งานพิมพ์
  - **Device Reservation**: ล็อคการใช้อุปกรณ์เฉพาะ process เดียว  
    → ป้องกัน deadlock ต้อง deallocate ให้ดี
  - **Error Handling**: ตรวจจับและจัดการ error เช่น retry, log
  - **I/O Protection**: จำกัดไม่ให้ process เข้าถึง I/O ตรง ๆ  
    → ต้องผ่าน system call และ instruction ต้องเป็น privileged เท่านั้น

---

## Summary

- อุปกรณ์ I/O หลากหลาย แบ่งเป็น character/block, sync/async, sharable/dedicated  
- มีการจัดการผ่านระบบ interrupt, DMA  
- OS มี subsystem สำหรับจัดการ I/O  
- มี Interface ที่ standardized สำหรับ application  
- Kernel มี I/O services สำคัญ เช่น scheduling, buffering, caching และ protection

