# Students Doubt Solving website app
# Academia Ace

A modern React + TypeScript + Vite application powered by Supabase.

---

# Installation & Setup Guide

Follow these steps to run the project locally from scratch.

---

## 1️⃣ Prerequisites

Make sure you have:

* **Node.js (LTS version recommended – v18 or above)**
* **npm** (comes with Node)
* A **Supabase account**

To check Node installation:

```bash
node -v
npm -v
```

If Node is not installed, download it from:
[https://nodejs.org](https://nodejs.org)

---

## 2️⃣ Clone the Repository

```bash
git clone <your-repository-url>
cd academia-ace
```

---

## 3️⃣ Install Dependencies

Delete old dependencies if needed:

```bash
rm -rf node_modules package-lock.json
```

Install fresh dependencies:

```bash
npm install
```

---

## 4️⃣ Setup Environment Variables

Create a `.env` file in the root directory (if not already present).

Add the following:

```env
VITE_SUPABASE_URL=your_supabase_project_url
VITE_SUPABASE_ANON_KEY=your_supabase_anon_key
```

---

## 5️⃣ Create Supabase Project

1. Go to [https://supabase.com](https://supabase.com)
2. Create a new project
3. Go to **Settings → API**
4. Copy:

   * Project URL
   * anon public key
5. Paste them inside the `.env` file

---

## 6️⃣ Run Development Server

```bash
npm run dev
```

The app will start at:

```
http://localhost:5173
```

---

## 7️⃣ Build for Production (Optional)

```bash
npm run build
```

To preview production build:

```bash
npm run preview
```

---

# Project Stack

* React + TypeScript
* Vite
* Tailwind CSS
* Supabase (Authentication & Database)

---

