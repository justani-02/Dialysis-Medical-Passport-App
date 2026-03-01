# 🛠️ Getting Started: Medical Passport Setup

This guide will walk you through setting up the local development environment for both the **FastAPI Backend** and the **React/TypeScript Frontend**.

---

## 📋 Prerequisites

Before you begin, ensure you have the following installed:
* **Python 3.9+**
* **Node.js (v18 or higher)** & **npm**
* **Git**
* A **Supabase** account (Free tier is sufficient)

---

## 🔑 Environment Variables

Both the frontend and backend require a `.env` file to handle secrets and API connections.

### Backend (`/backend/.env`)
```env
SUPABASE_URL=your_supabase_project_url
SUPABASE_KEY=your_supabase_anon_key
SECRET_HMAC_KEY=your_super_secret_signing_key_32_chars
```

### Frontend (`/frontend/.env`)

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key

```

---

## 🐍 1. Backend Setup (FastAPI)

The backend handles the **HMAC-SHA256** signing logic and FHIR data validation.

1. **Navigate to the directory:**
```bash
cd backend

```


2. **Create and activate a virtual environment:**
```bash
python -m venv venv
# macOS/Linux:
source venv/bin/activate
# Windows:
.\venv\Scripts\activate

```


3. **Install dependencies:**
```bash
pip install -r requirements.txt

```


4. **Run the development server:**
```bash
uvicorn main:app --reload

```


*The API will be live at `http://localhost:8000`. You can view the interactive Swagger docs at `/docs`.*

---

## ⚛️ 2. Frontend Setup (React + Vite)

The frontend provides the patient dashboard and the clinician's QR scanning interface.

1. **Navigate to the directory:**
```bash
cd frontend

```


2. **Install dependencies:**
```bash
npm install

```


3. **Start the development server:**
```bash
npm run dev

```


*The app will be live at `http://localhost:5173`.*

---

## 🧪 Testing the HMAC Logic

To verify that the "Bulletproof" security is working:

1. Use the backend `/sign` endpoint to generate a signed FHIR JSON package.
2. Manually change the `blood-flow-rate` value in the JSON.
3. Send the modified JSON to the `/verify` endpoint.
4. The system should return a `403 Forbidden` or `Integrity Failure` response.

---

