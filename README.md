# Social Media API: Cursor-Based Feed Generation & Social Graph Engine

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,100:0284c7&height=160&section=header&text=Social%20Graph%20Engine&fontSize=42&fontColor=ffffff&fontFamily=Outfit" width="100%" />
</div>

<div align="center">
  <img src="https://img.shields.io/badge/Node.js-v18-green?logo=nodedotjs&style=for-the-badge" alt="Node.js" /> <img src="https://img.shields.io/badge/MongoDB-v6-green?logo=mongodb&style=for-the-badge" alt="MongoDB" /> <img src="https://img.shields.io/badge/Socket.io-v4-black?logo=socketdotio&style=for-the-badge" alt="Socket.io" /> <img src="https://img.shields.io/badge/License-MIT-green?style=for-the-badge" alt="License" />
</div>

خادم **منصة التواصل الاجتماعي** هو محرك برمجي مصمم لبناء وإدارة المنشورات، التعليقات، الإعجابات، والعلاقات المعقدة بين المستخدمين (Social Graph) مع توليد جدول زمني (Feed) فوري وتصفح سريع لا متناهي.

This repository holds the Express backend REST API, database schemas, and feed generation logic for the **Social Media System**. Special focus is placed on query optimizations to support sub-10ms response times.

---

## 🧬 Timeline Generation & Graph Flow

The query engine aggregates timeline feeds dynamically while avoiding duplicate content:

```mermaid
graph TD
    Client[Client Mobile/Web App] -->|Query Feed with Cursor timestamp| API[REST Gateway]
    API -->|Fetch followers| Graph[Mongoose Social Graph Query]
    Graph -->|Return friends list ids| Agg[MongoDB Aggregation Pipeline]
    Agg -->|Filter & Sort posts by timestamp < Cursor| DB[(MongoDB Database)]
    DB -->|Map mutual-likes metadata| API
    API -->|Return JSON Array + next_cursor| Client
```

---

## 🧬 Core Services & Layouts

1.  **Feed Generator (`src/controllers/feed.js`)**: Employs cursor-based pagination utilizing timestamp indexes to guarantee fluid scrolling.
2.  **Social Graph Model (`src/models/friendship.js`)**: Tracks user connections, mutual follows, and blocks.
3.  **Real-Time Message Handler (`src/sockets/`)**: Manages chat rooms and online statuses for active friends.

---

## 🛠️ Technology Stack & Assets

*   **Runtime Backend**: Node.js & Express.js server router.
*   **Database Engine**: MongoDB for fast document structures and aggregation pipelines.
*   **Pagination Engine**: Cursor-based pagination logic (offset-free scrolling).

---

## 📂 Repository Module Layout

```text
social-media-api/
├── src/
│   ├── controllers/     # Business logic (Feed, Auth, Comments)
│   ├── models/          # MongoDB schemas (User, Post, Friendship)
│   ├── routes/          # API route bindings
│   └── app.js           # Express initializer
├── package.json         # Node metadata
└── README.md            # System documentation
```

---

## ⚡ Local Setup & Run
```bash
git clone https://github.com/Sayed-Herzallah/social-media-api.git
cd social-media-api
npm install
# Set MONGO_URI in environment variables
npm start
```

---

## 📄 License
Licensed under the **MIT License**.
