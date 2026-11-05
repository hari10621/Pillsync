# PillSync — Intelligent Medicine Management \& Reminder System

PillSync is an end-to-end healthcare assistance platform designed to ensure medication adherence, streamline refill management, and empower patients, caregivers, and medical administrators through intelligent scheduling, prescription OCR processing, and conversational AI insights.

\---

## 📌 Table of Contents

* [Project Overview](#-project-overview)
* [Key Features](#-key-features)

  * [Patient Experience](#patient-experience)
  * [Caregiver Portal](#caregiver-portal)
  * [Administrative Control](#administrative-control)
  * [OCR \& AI Intelligence](#ocr--ai-intelligence)
* [System Architecture](#-system-architecture)
* [Tech Stack](#-tech-stack)
* [Directory Structure](#-directory-structure)
* [API Endpoints Overview](#-api-endpoints-overview)
* [Getting Started](#-getting-started)

  * [Prerequisites](#prerequisites)
  * [Backend Setup (Django)](#backend-setup-django)
  * [Frontend Setup (React + Vite)](#frontend-setup-react--vite)
* [Environment Configuration](#-environment-configuration)
* [License](#-license)

\---

## 🩺 Project Overview

Managing multiple medication regimens is complex and often leads to missed doses, improper timing, and delayed refills. **PillSync** addresses these challenges by offering:

1. **Precision Scheduling**: Flexible dosage scheduling adapted to daily, interval, or custom medical regimens.
2. **Prescription Digitization (OCR)**: Converting scanned or photographed prescriptions into structured medication entries with dosage and frequency extraction.
3. **Refill Forecasting**: Stock depletion calculations that forecast runout dates and provide proactive alerts before critical levels are reached.
4. **Caregiver Oversight**: Family members and caregivers can monitor patient compliance, receive missed dose notifications, and review adherence reports.
5. **Contextual AI Assistant**: An in-app health assistant powered by Groq LLM that provides instant answers based on a patient's active prescriptions, logs, and medical schedule.

\---

## ✨ Key Features

### Patient Experience

* **Interactive Dashboard**: Real-time view of daily dose timelines, pending vs. completed medications, and inventory levels.
* **Dose Tracking \& Logging**: Mark doses as taken, missed, or snoozed, with automatic adherence score tracking.
* **Prescription Upload (OCR)**: Upload prescription images to automatically parse medicine names, dosages, and daily frequencies.
* **Smart Refill Alerts**: Proactive notifications when supplies dip below critical thresholds (3 days or 7 days of supply).
* **Customizable Preferences**: Light/dark mode switching, custom reminder lead times (e.g., 15 minutes before dose), and sound preferences.

### Caregiver Portal

* **Patient Monitoring**: Supervise multiple assigned patients under a unified portal.
* **Adherence \& Compliance Tracking**: Inspect compliance percentages and historical dose trends.
* **Alert Feeds**: Receive alerts when patients miss scheduled doses or encounter stock shortages.

### Administrative Control

* **Master Medicine Catalog**: Centralized database to maintain standard medicine names, brands, dosages, and descriptions.
* **User Management**: Control patient and caregiver registrations, account statuses, and verification workflows.
* **System Logs \& Audit Trail**: Comprehensive tracking of authentication activities, administrative actions, and API events.
* **System-Wide Analytics**: Aggregate statistics on user growth, population-wide adherence, and inventory consumption.

### OCR \& AI Intelligence

* **Tesseract OCR Pipeline**: Custom image enhancement (grayscale conversion, auto-contrast, contrast boost, sharpening, binary thresholding) coupled with regex-based data extraction for dosage units (`mg`, `mcg`, `ml`), quantities, and frequencies (`t.i.d`, `b.i.d`, etc.).
* **Groq-Powered AI Assistant**: A draggable, role-aware floating assistant capable of parsing user queries in the context of their actual health profile, schedules, and adherence history.

\---

## 🏗 System Architecture

```text
\[ Browser / Client ] 
        │
        │ HTTP / REST (JWT Auth)
        ▼
\[ Vite + React Frontend ] (Port: 5173)
   ├── Role-Based Protected Routes (Patient / Caregiver / Admin)
   ├── Tailwind CSS + Lucide Icons + Recharts
   └── Draggable AI Assistant Drawer \& Notification System
        │
        │ Axios HTTP Requests
        ▼
\[ Django REST Framework Backend ] (Port: 8000)
   ├── Apps: users, medications, reminders, adherence, refill\_engine, notifications, ocr, analytics
   ├── Tesseract OCR Pipeline (Image Processing \& Pattern Matching)
   ├── Groq API Client (AI Contextual Insights)
   └── SQLite Database (db.sqlite3)
```

\---

## 💻 Tech Stack

### Frontend

* **Framework**: [React 18](https://react.dev/)
* **Build Tool**: [Vite](https://vitejs.dev/)
* **Routing**: [React Router DOM v6](https://reactrouter.com/)
* **Styling**: [Tailwind CSS](https://tailwindcss.com/) \& CSS Modules / Custom Properties
* **Data Visualization**: [Recharts](https://recharts.org/)
* **Icons**: [Lucide React](https://lucide.dev/)
* **HTTP Client**: [Axios](https://axios-http.com/) (configured with automatic JWT bearer interceptors)

### Backend

* **Framework**: [Django 5.0.6](https://www.djangoproject.com/)
* **API Engine**: [Django REST Framework (DRF) 3.15.1](https://www.django-rest-framework.org/)
* **Authentication**: [SimpleJWT](https://django-rest-framework-simplejwt.readthedocs.io/) (JSON Web Tokens)
* **API Documentation**: [drf-spectacular](https://drf-spectacular.readthedocs.io/) (OpenAPI 3.0 / Swagger UI \& ReDoc)
* **CORS Handling**: `django-cors-headers`
* **Environment Management**: `python-decouple`
* **Database**: SQLite (default, easily swappable with PostgreSQL/MySQL)

### OCR \& AI

* **OCR Engine**: [Tesseract OCR](https://github.com/tesseract-ocr/tesseract) via `pytesseract`
* **Image Preprocessing**: [Pillow (PIL)](https://python-pillow.org/)
* **LLM Integration**: [Groq Cloud SDK](https://console.groq.com/)

\---

```

\---

### Backend Setup (Django)

1. **Open a terminal and navigate to the backend directory**:

```bash
   cd backend
   ```

2. **Create and activate a virtual environment**:

   * *Windows (PowerShell)*:

```powershell
     python -m venv venv
     .\\venv\\Scripts\\Activate.ps1
     ```

   * *macOS / Linux*:

```bash
     python3 -m venv venv
     source venv/bin/activate
     ```

3. **Install dependencies**:

```bash
   pip install -r requirements.txt
   ```

4. **Configure environment variables**:
Create a `.env` file inside the `backend/` directory (see [Environment Configuration](#-environment-configuration)).
5. **Apply database migrations**:

```bash
   python manage.py migrate
   ```

6. **Create an administrator account (optional)**:

```bash
   python manage.py createsuperuser
   ```

7. **Run the development server**:

```bash
   python manage.py runserver 8000
   ```

   *The Django API will be accessible at `http://localhost:8000/`.*

\---

### Frontend Setup (React + Vite)

1. **Open a new terminal and navigate to the frontend directory**:

```bash
   cd frontend
   ```

2. **Install frontend dependencies**:

```bash
   npm install
   ```

3. **Start the development server**:

```bash
   npm run dev
   ```

   *The application UI will run at `http://localhost:5173/`.*

\---

## ⚙️ Environment Configuration

Create a `.env` file in the `backend/` directory with the following variables:

```env
# Django Settings
SECRET\_KEY=your-secure-secret-key-here
DEBUG=True
ALLOWED\_HOSTS=\*

# Groq Cloud API (For AI Assistant features)
GROQ\_API\_KEY=your\_groq\_api\_key\_here
```

> \*\*Note\*\*: If Tesseract OCR is installed in a non-default location on your machine, ensure the path set in `backend/apps/ocr/views.py` matches your system's executable path.

\---

.

