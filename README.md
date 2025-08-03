Tessarion-Tsc Platform

🚀 AI-Driven Investment & Financial Education Platform
Built by the Tessarion-Tsc Channel Team under @Tess-Cyber1


---

📌 Overview

Tessarion-Tsc is a full-stack platform that combines:

🧠 AI-powered portfolio management

📊 Real-time investment dashboards

🎓 Interactive financial education and certification

🔒 Secure authentication with role-based access

⚙️ Admin tools for content and user management



---

🛠 Tech Stack

Frontend: React / Next.js / Tailwind CSS

Backend: Python (FastAPI)

Database: PostgreSQL

Auth: Firebase Auth or NextAuth.js

AI Models: Python (scikit-learn, TensorFlow)



---

📁 Structure

/frontend – User interface and dashboards

/backend – API and investment logic

/education – Course engine and certification

/auth – Login and access control

/dashboard – Admin & investment dashboards



---

✅ Getting Started

Clone the repo:

git clone https://github.com/Tess-Cyber1/Tessarion-Tsc-Platform.git
cd Tessarion-Tsc-Platform

Install dependencies:

cd frontend && npm install
cd ../backend && pip install -r requirements.txt


---

📄 License

This project is licensed under the MIT License – see the LICENSE file for details.


---

🙌 Team

Maintained by the Tessarion-Tsc Channel Team
Contact: tess.cyber@protonmail.com


---

📦 backend/requirements.txt

fastapi
uvicorn
pydantic
sqlalchemy
psycopg2-binary
scikit-learn
tensorflow
python-dotenv


---

🚀 backend/main.py

from fastapi import FastAPI
from fastapi.middleware.cors import CORSMiddleware

app = FastAPI()

app.add_middleware(
    CORSMiddleware,
    allow_origins=["*"],
    allow_credentials=True,
    allow_methods=["*"],
    allow_headers=["*"],
)

@app.get("/")
def read_root():
    return {"message": "Welcome to the Tessarion-Tsc API"}

@app.get("/health")
def health_check():
    return {"status": "ok"}


---

🎯 frontend/pages/index.tsx

import Head from 'next/head'

export default function Home() {
  return (
    <div className="min-h-screen bg-gray-100 flex flex-col items-center justify-center">
      <Head>
        <title>Tessarion-Tsc Platform</title>
      </Head>

      <main className="text-center">
        <h1 className="text-4xl font-bold text-blue-600">Welcome to Tessarion-Tsc</h1>
        <p className="mt-4 text-lg text-gray-700">
          AI-Driven Investment & Financial Education for Everyone.
        </p>
        <p className="mt-2 text-sm text-gray-500">
          Built by the Tessarion-Tsc Channel Team
        </p>
      </main>
    </div>
  )
}


---

🧪 .env.example

# Backend
DATABASE_URL=postgresql://user:password@localhost:5432/tessarion_db
SECRET_KEY=your-secret-key

# AI Configs
MODEL_PATH=models/portfolio_model.pkl

# Frontend
NEXT_PUBLIC_API_BASE_URL=http://localhost:8000

# Auth (Firebase or NextAuth)
FIREBASE_API_KEY=your-api-key
FIREBASE_AUTH_DOMAIN=your-project.firebaseapp.com
FIREBASE_PROJECT_ID=your-project-id


---

⚙️ .github/workflows/deploy.yml

name: CI/CD Workflow

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]

jobs:
  build:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:13
        env:
          POSTGRES_USER: postgres
          POSTGRES_PASSWORD: postgres
          POSTGRES_DB: tessarion_db
        ports:
          - 5432:5432
        options: >-
          --health-cmd pg_isready
          --health-interval 10s
          --health-timeout 5s
          --health-retries 5

    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up Python
        uses: actions/setup-python@v4
        with:
          python-version: '3.10'

      - name: Install backend dependencies
        run: |
          cd backend
          pip install -r requirements.txt

      - name: Run FastAPI health check
        run: |
          uvicorn main:app --host 0.0.0.0 --port 8000 &
          sleep 5
          curl http://localhost:8000/health

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '18'

      - name: Install frontend dependencies
        run: |
          cd frontend
          npm install
          npm run build

