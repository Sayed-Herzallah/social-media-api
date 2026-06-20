# 🌐 Social Media AI Engine - Real-Time Backend

<div align="center">
  <img src="https://capsule-render.vercel.app/api?type=waving&color=0:0d1117,100:1e88e5&height=180&section=header&text=Social%20Media%20AI%20Engine&fontSize=40&fontColor=ffffff&fontFamily=Outfit" width="100%" />
</div>

A production-grade, AI-integrated, and real-time Social Media API backend built on a modular MVC architecture. This backend powers standard social activities (posts, nested comments, users relationship, administrative controls) and supercharges them with a **Hybrid AI Layer** (supporting Google Gemini, OpenAI, and local Ollama execution) alongside real-time communication via WebSockets.

---

## 🚀 Key Features

* **🔌 Real-Time Communications**: Full-duplex WebSockets using `Socket.io` powering instant notifications, real-time comment streams, post updates, and chat messages.
* **🧠 Hybrid AI Orchestration**: Multi-LLM adapter supporting Google Gemini (`@google/generative-ai`), OpenAI GPT models, and local offline execution via `Ollama`. Powers auto-post generation, text completions, sentiment analysis, and automated content moderation.
* **🖼️ Rich Media Processing**: Multi-part upload pipelines using `Multer` combined with direct streaming and storage optimization on `Cloudinary`.
* **🔒 Enterprise-Grade Security**: Cryptographic salting and password hashing using `Bcrypt`, JWT-based state-less authentication, and database-level field encryption via `Crypto-JS`.
* **🛡️ Bulletproof Data Sanitization**: Strict schema-level validation at the routing layer using `Joi` preventing SQL/NoSQL injections and malformed payloads.
* **📂 Modular MVC Architecture**: Clean code structure separation containing dedicated modules for `Admin`, `Ai`, `Auth`, `Comments`, `Posts`, and `Users`.

---

## 🧬 Architecture & Logic Flow

Below is the visual overview of how request routing, middleware validation, WebSocket events, and AI service calls are processed inside this engine:

```mermaid
graph TD
    Client[Client App / Postman] -->|HTTP REST Request| Express[Express Server Engine]
    Client -->|WebSocket Connection| SocketIO[Socket.io WebSockets Layer]
    
    Express -->|Route Handlers| AuthMW[Auth & Role Validation]
    AuthMW -->|Sanitization| JoiMW[Joi Schema Validation]
    JoiMW -->|Valid Payload| Controller[Feature Controller]
    
    Controller -->|Real-Time Broadcast| SocketIO
    Controller -->|Store Data| MongoDB[(MongoDB / Mongoose ODM)]
    Controller -->|Upload Assets| Cloudinary[Cloudinary CDN]
    
    Controller -->|Prompt Engineering| AIService[AI Adapter Service]
    AIService -->|API Web Calls| OpenAI[OpenAI API]
    AIService -->|API Web Calls| Gemini[Google Gemini SDK]
    AIService -->|Local Offline RPC| Ollama[Local Ollama Instance]
```

---

## 🛠️ Technology Stack & Badges

### Core Architecture
[![Node.js](https://img.shields.io/badge/Node.js-v20.x-green?logo=nodedotjs&style=flat-square)](https://nodejs.org/)
[![Express.js](https://img.shields.io/badge/Express.js-v5.x_Beta-lightgrey?logo=express&style=flat-square)](https://expressjs.com/)
[![MongoDB](https://img.shields.io/badge/MongoDB-v7.x-green?logo=mongodb&style=flat-square)](https://www.mongodb.com/)
[![Mongoose](https://img.shields.io/badge/Mongoose-v9.x-red?logo=mongoose&style=flat-square)](https://mongoosejs.com/)
[![Socket.io](https://img.shields.io/badge/Socket.io-v4.x-blue?logo=socketdotio&style=flat-square)](https://socket.io/)

### Artificial Intelligence & Security
[![Google Gemini](https://img.shields.io/badge/Gemini_AI-SDK-blue?logo=google&style=flat-square)](https://ai.google.dev/)
[![OpenAI](https://img.shields.io/badge/OpenAI_GPT-6.x-brightgreen?logo=openai&style=flat-square)](https://openai.com/)
[![Ollama](https://img.shields.io/badge/Ollama-Offline_LLM-darkgrey?style=flat-square)](https://ollama.com/)
[![CryptoJS](https://img.shields.io/badge/Crypto_JS-AES_Encryption-orange?style=flat-square)](https://cryptojs.gitbook.io/)
[![Cloudinary](https://img.shields.io/badge/Cloudinary-Media_CDN-lightblue?logo=cloudinary&style=flat-square)](https://cloudinary.com/)

---

## 📂 Folder Structure

```text
Social-Mdeia Application/
├── index.js               # Application Entrypoint & HTTP Bootstrap
├── app.controller.js      # App setup (CORS, Express Middlewares, Globals, Database Connect)
├── vercel.json            # Serverless deployment configuration
├── Src/
│   ├── DataBase/          # Connection wrapper, Model schemas & indexes
│   │   ├── connection.js
│   │   └── Models/
│   ├── MiddleWare/        # Global request filters
│   │   ├── auth.middleware.js
│   │   └── validation.middleware.js
│   ├── Utils/             # Shared helpers, email templates & cryptographic wrappers
│   │   ├── sendEmail.js
│   │   └── crypto.js
│   └── Modules/           # Modular Domain Features (Routes, Controllers, Schema Rules)
│       ├── Admin/         # Analytics, user bans, audit logs
│       ├── Ai/            # LLM connectors (Gemini, OpenAI, Ollama controllers)
│       ├── Auth/          # Registration, verified logins, JWT signing
│       ├── Comments/      # Nested discussion controllers
│       ├── Posts/         # Rich feed management & cloud uploads
│       └── Users/         # Social graphs (Follows, bios, search indexes)
```

---

## 🚀 Getting Started

### Prerequisites
- Node.js (v20.x or above)
- MongoDB running locally or a MongoDB Atlas URI
- API Keys for Cloudinary, OpenAI, and Google Gemini (Optional if using local Ollama)

### Installation
1. Clone the codebase:
   ```bash
   git clone https://github.com/Sayed-Herzallah/Social-Mdeia-Application.git
   cd Social-Mdeia-Application
   ```
2. Install standard dependencies:
   ```bash
   npm install
   ```
3. Set up your environment file. Create a `.env` in the root:
   ```env
   PORT=3000
   MONGO_URI=mongodb://127.0.0.1:27017/social_media
   JWT_SECRET=your_jwt_signature_key
   CRYPTO_SECRET=your_aes_database_secret_key
   
   CLOUDINARY_CLOUD_NAME=your_cloudinary_name
   CLOUDINARY_API_KEY=your_cloudinary_key
   CLOUDINARY_API_SECRET=your_cloudinary_secret
   
   GEMINI_API_KEY=your_gemini_token
   OPENAI_API_KEY=your_openai_token
   OLLAMA_HOST=http://127.0.0.1:11434
   ```
4. Run in development mode:
   ```bash
   npm start
   ```

---

## 📜 Verified Certificates & Achievements
To review verified technical accomplishments, backend training, and professional project portfolios, click below:

[![Portfolio Achievements](https://img.shields.io/badge/Verified_Certifications-Click_to_View-gold?style=for-the-badge&logo=credentials)](https://herzallah.me#certifications)

---

## 👨‍💻 Developed By
**Sayed Herzallah**  
*Backend-Focused Full-Stack Developer*  
- [LinkedIn Profile](https://www.linkedin.com/in/sayed-herzallah)  
- [Portfolio Website](https://herzallah.me)  
- [GitHub Profile](https://github.com/Sayed-Herzallah)  
