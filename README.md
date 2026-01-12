## 📊 5. แผนภาพระบบ (System Architecture)

```mermaid
graph TD
    Client[User / Browser] -->|HTTPS| Frontend[Firebase Hosting]
    Frontend -->|REST API| Backend[Render (Node.js)]
    
    Backend -->|Read/Write| DB[(Firestore Database)]
    Backend -->|Generate| AI[Google Gemini AI]
    
    Cron[External Cron Job] -->|Trigger 09:00 AM| Backend
    Backend -- Fetch RSS --> News[Thai Education News]
```
