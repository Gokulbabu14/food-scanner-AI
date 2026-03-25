# TechSprint Food Scanner

An AI-powered food scanner application that analyzes food images and provides nutritional information using Google Gemini AI.

## 🚀 Quick Start

**For detailed setup instructions, see [SETUP_GUIDE.md](./SETUP_GUIDE.md)**

### Quick Commands:

**Backend:**
```bash
cd backend
python -m venv .venv
.venv\Scripts\Activate.ps1  # Windows PowerShell
pip install -r requirements.txt
python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
```

**Frontend:**
```bash
cd frontend
pnpm install
pnpm dev
```

**Verify Backend Setup:**
```bash
cd backend
python verify_setup.py
```

## Project Structure

```
GDG/
├── backend/          # FastAPI backend
│   ├── app/
│   │   ├── main.py   # FastAPI application with CORS
│   │   ├── utils.py  # Food image analysis logic
│   │   └── schemas.py # Pydantic models
│   ├── .env          # Environment variables (GEMINI_API_KEY)
│   └── requirements.txt
└── frontend/         # Next.js frontend
    ├── app/          # Next.js app directory
    ├── components/   # React components
    ├── lib/
    │   └── api.ts    # API configuration and client functions
    ├── .env.local    # Frontend environment variables (API URL)
    └── package.json
```

## ✨ Features

- 🔐 **Secure Authentication** - JWT-based auth with bcrypt password hashing
- 📸 **AI Food Analysis** - Upload food images and get instant nutritional info
- 💾 **Data Storage** - Save food analyses in mock database
- 📊 **User Dashboard** - Track your nutrition journey
- 🎨 **Modern UI** - Built with Next.js and Tailwind CSS

## Prerequisites

- **Python 3.8+** (for backend)
- **Node.js 18+** and **pnpm** (for frontend)
- **Google Gemini API Key** (for AI analysis)

## Setup Instructions

### Backend Setup

1. **Navigate to the backend directory:**
   ```bash
   cd backend
   ```

2. **Create a virtual environment (recommended):**
   ```bash
   python -m venv .venv
   ```

3. **Activate the virtual environment:**
   - **Windows (PowerShell):**
     ```powershell
     .venv\Scripts\Activate.ps1
     ```
   - **Windows (CMD):**
     ```cmd
     .venv\Scripts\activate.bat
     ```
   - **macOS/Linux:**
     ```bash
     source .venv/bin/activate
     ```

4. **Install dependencies:**
   ```bash
   pip install -r requirements.txt
   ```

5. **Configure environment variables:**
   - The `.env` file already exists with a GEMINI_API_KEY
   - If you need to update it, edit `backend/.env`:
     ```
     GEMINI_API_KEY=your_api_key_here
     ```

6. **Run the backend server:**
   ```bash
   python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000
   ```
   
   Or simply:
   ```bash
   python -m app.main
   ```

   The backend will be available at: **http://127.0.0.1:8000**

   You can test it by visiting: http://127.0.0.1:8000/ (should show `{"status": "TechSprint Backend is running"}`)

### Frontend Setup

1. **Navigate to the frontend directory:**
   ```bash
   cd frontend
   ```

2. **Install dependencies:**
   ```bash
   pnpm install
   ```
   
   If you don't have pnpm installed:
   ```bash
   npm install -g pnpm
   ```
   
   Or use npm instead:
   ```bash
   npm install
   ```

3. **Configure API connection (optional):**
   - A `.env.local` file is already created with the default backend URL
   - To change the backend URL, edit `frontend/.env.local`:
     ```
     NEXT_PUBLIC_API_URL=http://127.0.0.1:8000
     ```
   - If the file doesn't exist, copy `.env.local.example` to `.env.local`

4. **Run the development server:**
   ```bash
   pnpm dev
   ```
   
   Or with npm:
   ```bash
   npm run dev
   ```

   The frontend will be available at: **http://localhost:3000**

## Running the Application

1. **Start the backend first:**
   - Open a terminal in the `backend` directory
   - Activate virtual environment (if using one)
   - Run: `python -m uvicorn app.main:app --reload --host 127.0.0.1 --port 8000`

2. **Start the frontend:**
   - Open another terminal in the `frontend` directory
   - Run: `pnpm dev` (or `npm run dev`)

3. **Open your browser:**
   - Navigate to: http://localhost:3000
   - The frontend will automatically connect to the backend at http://127.0.0.1:8000
   - You'll see a connection status indicator if the backend is not reachable

## Connection Status

The frontend includes automatic backend connection checking:
- ✅ **Connected**: Backend is running and accessible
- ⚠️ **Warning**: If backend is not connected, a warning message will appear at the top of the scanner
- The connection is checked automatically when the page loads

### Verifying the Connection

1. **Backend health check:**
   - Visit: http://127.0.0.1:8000/
   - Should return: `{"status": "TechSprint Backend is running"}`

2. **Frontend connection:**
   - The frontend automatically checks backend health on page load
   - If disconnected, you'll see a warning banner with connection details

## API Endpoints

### Authentication Endpoints

- `POST /register` - Register a new user
  - **Request:** `{ "email": "user@example.com", "password": "password", "name": "Name" }`
  - **Response:** `{ "access_token": "...", "token_type": "bearer", "user": {...} }`

- `POST /login` - Login and get access token
  - **Request:** `{ "email": "user@example.com", "password": "password" }`
  - **Response:** `{ "access_token": "...", "token_type": "bearer", "user": {...} }`

- `GET /me` - Get current user (requires Bearer token)
- `PUT /me` - Update current user (requires Bearer token)

### Food Analysis Endpoints

- `GET /` - Health check endpoint
- `POST /scan-food` - Upload a food image and get nutritional analysis
  - **Request:** Multipart form data with `file` field (image file)
  - **Response:** JSON with `itemName`, `calories`, `protein`, `carbs`, `fats`, `intakeDecision`, `suggestion`

- `POST /save-analysis` - Save food analysis to database
- `GET /analyses` - Get all saved analyses
- `GET /analyses/{id}` - Get specific analysis
- `DELETE /analyses/{id}` - Delete analysis

## Features

- 📸 Upload food images via drag-and-drop or file picker
- 🤖 AI-powered nutritional analysis using Google Gemini
- 📊 Detailed macro breakdown (calories, protein, carbs, fats)
- 💡 Health recommendations (Allow/Limited/Avoid)
- 🎨 Modern, responsive UI built with Next.js and Tailwind CSS

## Troubleshooting

### Backend Issues

- **"GEMINI_API_KEY not found"**: Make sure `.env` file exists in the `backend` directory with a valid API key
- **Port 8000 already in use**: Change the port in the uvicorn command: `--port 8001`
- **Module not found errors**: Make sure you've activated the virtual environment and installed requirements

### Frontend Issues

- **Cannot connect to backend**: Ensure the backend is running on `http://127.0.0.1:8000`
- **Port 3000 already in use**: Next.js will automatically use the next available port (3001, 3002, etc.)
- **pnpm not found**: Install pnpm globally or use npm instead

### Connection Issues

- **Backend not connecting**: 
  - Ensure backend is running on `http://127.0.0.1:8000`
  - Check that the port matches in `frontend/.env.local` (NEXT_PUBLIC_API_URL)
  - The frontend will show a warning if the backend is unreachable

### Authentication Issues

- **"Invalid authentication credentials"**: 
  - Make sure JWT_SECRET_KEY is set in `backend/.env`
  - Generate a new key: `python backend/generate_jwt_secret.py`
  - Try logging out and logging in again
  
- **"User not found"**: 
  - Register a new account first
  - Check that backend user_db is working

### CORS Issues

- The backend is configured to allow connections from `localhost:3000` and `127.0.0.1:3000`
- CORS is properly configured for development
- In production, update `backend/app/main.py` to restrict CORS to your specific frontend domain

## Production Build

### Backend
```bash
# No special build needed, just ensure dependencies are installed
pip install -r requirements.txt
```

### Frontend
```bash
cd frontend
pnpm build
pnpm start
```

## Dependencies

### Backend
- `fastapi` - Web framework
- `uvicorn` - ASGI server
- `google-generativeai` - Google Gemini AI SDK
- `python-multipart` - File upload support
- `python-dotenv` - Environment variable management
- `pydantic` - Data validation

### Frontend
- `next` - React framework
- `react` & `react-dom` - UI library
- `tailwindcss` - Styling
- `lucide-react` - Icons
- Various Radix UI components for accessible UI primitives
#   f o o d - s c a n n e r - A I  
 #   f o o d - s c a n n e r - A I  
 