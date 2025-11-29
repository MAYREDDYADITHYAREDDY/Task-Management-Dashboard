# Quick Setup Guide

## 📥 Download Project

**Download the complete project from Google Drive:**

🔗 **[Download Project Files](https://drive.google.com/file/d/1D9Vg85T50awazdFUpbqvuOuR0lpPNplp/view?usp=drive_link)**

---

## 🚀 Setup Instructions

### Step 1: Extract the Project
1. Download the ZIP file from the link above
2. Extract to your desired location (e.g., `C:\Projects\Adithya_AI`)
3. Open the folder in your code editor

### Step 2: Install Dependencies

**Backend:**
```bash
cd backend
npm install
```

**Frontend (in a new terminal):**
```bash
cd frontend
npm install
```

### Step 3: Start the Application

**Terminal 1 - Start Backend:**
```bash
cd backend
npm run dev
```
✅ Backend will run on http://localhost:5000

**Terminal 2 - Start Frontend:**
```bash
cd frontend
npm start
```
✅ Frontend will run on http://localhost:3000

### Step 4: Access the Application

| Service | URL |
|---------|-----|
| **Frontend** | http://localhost:3000 |
| **Backend API** | http://localhost:5000 |
| **API Docs** | http://localhost:5000/api-docs |

---

## 🎯 First Steps

1. **Register a new account** at http://localhost:3000
   - Username: Your choice (alphanumeric, 3+ chars)
   - Email: Valid email format
   - Password: Min 6 chars with uppercase, lowercase, and number (e.g., `Test1234`)

2. **Login** with your credentials

3. **Create tasks** from the dashboard

4. **Test the API** at http://localhost:5000/api-docs (Swagger UI)

---

## ✅ Requirements

- Node.js v16 or higher
- npm or yarn

That's it! No database setup needed - SQLite is auto-configured.

---

## 🐛 Troubleshooting

**Port already in use?**
```bash
# Kill process on port 5000
netstat -ano | findstr :5000
taskkill /PID <PID> /F
```

**Dependencies failed to install?**
```bash
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

**Need help?** Check the full README.md for detailed documentation.
