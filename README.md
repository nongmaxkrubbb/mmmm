# 🏫 Nongmim Child Development Center Management System

## 📋 ภาพรวมโปรเจกต์ (Project Overview)
ระบบบริหารจัดการศูนย์พัฒนาเด็กเล็กแบบ Full-stack ที่เชื่อมต่อระหว่างเว็บไซต์ประชาสัมพันธ์และระบบหลังบ้านสำหรับผู้ดูแลระบบ (Admin) โดยมีการนำ **AI (Google Gemini)** มาช่วยในการทำงานอัตโนมัติ เช่น การเขียนข่าวและการตอบคำถาม

## 🛠️ เทคโนโลยีที่ใช้ (Tech Stack)
*   **Frontend**: React.js (Vite), Tailwind CSS
    *   *Hosting*: **Firebase Hosting**
*   **Backend**: Node.js, Express.js
    *   *Hosting*: **Render (Cloud Application Hosting)**
*   **Database**: **Firebase Cloud Firestore** (NoSQL Database)
*   **AI Integration**: Google Gemini API (สำหรับสรุปข่าวและ Chatbot)
*   **Automation**: Node-cron + External Cron Trigger

## 🏗️ แผนภาพการทำงานของระบบ (System Architecture)

```mermaid
graph TD
    %% Users
    User["👶 ผู้ใช้งานทั่วไป / ผู้ปกครอง"]
    Admin["👩‍🏫 ผู้ดูแลระบบ (Admin)"]

    %% Frontend
    subgraph Frontend ["🌐 Frontend (React + Vite)"]
        Web["เว็บไซต์ประชาสัมพันธ์"]
        AdminPanel["ระบบจัดการหลังบ้าน"]
    end

    %% Backend
    subgraph BackendSystem ["⚙️ Backend (Node.js on Render)"]
        API["API Server (Express)"]
        Scheduler["Auto News Scheduler"]
    end

    %% External & Data
    subgraph CloudServices ["☁️ Cloud Services"]
        DB[("Firebase Firestore\nDatabase")]
        Gemini["🧠 Google Gemini AI"]
    end

    subgraph External ["โลกภายนอก"]
        RSS["📰 Google News RSS"]
        CronJob["⏰ External Cron (09:00 น.)"]
    end

    %% Connections
    User -->|เข้าชมเว็บไซต์| Web
    Admin -->|Login / จัดการข้อมูล| AdminPanel
    
    Web -->|Request API| API
    AdminPanel -->|Request API| API
    
    API -->|Read/Write Data| DB
    API -->|Generate Content / Chat| Gemini
    
    %% Automation Flow
    CronJob -->|Trigger via API| API
    Scheduler -->|1. Fetch News| RSS
    Scheduler -->|2. Summarize & Rewrite| Gemini
    Scheduler -->|3. Save Auto Post| DB
```

## 🚀 วิธีการเริ่มโปรเจกต์ (How to Start)

### 1. เตรียม Environment Variables
ตรวจสอบไฟล์ `.env` ในทั้งสองโฟลเดอร์:
*   **Backend (`/Backend/.env`)**: ต้องมีค่า `GEMINI_API_KEY`, `FIREBASE_SERVICE_ACCOUNT` (หรือไฟล์ key json), `JWT_SECRET`
*   **Frontend (`/frontend/.env`)**: ต้องมีค่า `VITE_API_URL` (เช่น `http://localhost:5000/api`)

### 2. รันระบบหลังบ้าน (Backend)
```bash
cd Backend
npm install
npm run dev
# Server จะเริ่มทำงานที่ Port 5000
```

### 3. รันระบบหน้าบ้าน (Frontend)
เปิด Terminal ใหม่:
```bash
cd frontend
npm install
npm run dev
# Web จะเริ่มทำงานที่ http://localhost:5173
```
