# ExpensePilot Setup Guide

Complete setup instructions for running ExpensePilot locally.

## Prerequisites

Before you begin, make sure you have the following installed:

- **Node.js** (v16 or higher) - [Download](https://nodejs.org/)
- **npm** (comes with Node.js)
- **MongoDB** (optional - app works without it)
  - Local: [Download MongoDB Community](https://www.mongodb.com/try/download/community)
  - Cloud: [MongoDB Atlas](https://www.mongodb.com/cloud/atlas) (free tier available)

## Quick Start (Recommended)

### 1. Clone/Navigate to Project

```bash
cd ExpensePilot
```

### 2. Backend Setup

```bash
# Navigate to backend folder
cd backend

# Install dependencies
npm install

# Create .env file
# Copy .env.example to .env
cp .env.example .env

# For MongoDB Atlas (Cloud):
# Edit .env and replace MONGODB_URI with your connection string:
# MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/expensepilot

# Start backend server
npm start
```

**Expected output:**
```
🚀 Server running on http://localhost:5000
✅ Connected to MongoDB
```

### 3. Frontend Setup (in new terminal)

```bash
# Navigate to frontend folder (from project root)
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

**Expected output:**
```
VITE v5.0.0  ready in 456 ms

➜  Local:   http://localhost:5173/
```

### 4. Open in Browser

Visit: **http://localhost:5173**

## Detailed Setup Options

### Option A: With Local MongoDB

#### Windows

1. Download and install [MongoDB Community Server](https://www.mongodb.com/try/download/community)
2. During installation, select "Install MongoDB as a Service"
3. MongoDB will automatically start on port 27017

#### macOS

```bash
# Install with Homebrew
brew tap mongodb/brew
brew install mongodb-community

# Start MongoDB
brew services start mongodb-community
```

#### Linux (Ubuntu/Debian)

```bash
# Install MongoDB
sudo apt-get install mongodb

# Start MongoDB
sudo systemctl start mongodb
```

### Option B: With MongoDB Atlas (Cloud) - Recommended for Production

1. Go to [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create a free account
3. Create a new cluster
4. Create database user (username and password)
5. Get connection string from "Connect" button
6. Update `.env` file in backend:

```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/expensepilot?retryWrites=true&w=majority
PORT=5000
NODE_ENV=development
```

## Troubleshooting

### Issue: Backend won't start

**Error:** `Error: connect ECONNREFUSED 127.0.0.1:27017`

**Solution:** MongoDB is not running
```bash
# macOS/Linux
sudo systemctl start mongodb

# Windows: Check Services or restart MongoDB service
```

**Error:** `MONGODB_URI is not defined`

**Solution:** Create `.env` file in backend folder:
```bash
cd backend
echo "MONGODB_URI=mongodb://localhost:27017/expensepilot" > .env
echo "PORT=5000" >> .env
echo "NODE_ENV=development" >> .env
```

### Issue: Frontend won't load

**Error:** `VITE_API_URL is not defined`

**Solution:** Create `.env` file in frontend folder:
```bash
cd frontend
echo "VITE_API_URL=http://localhost:5000/api" > .env
```

### Issue: Port already in use

**Backend (Port 5000):**
```bash
# Find process using port 5000
lsof -i :5000

# Kill process (macOS/Linux)
kill -9 <PID>

# Windows: Open Task Manager → find node.js → End task
```

**Frontend (Port 5173):**
```bash
# Vite will automatically use next available port
```

## Running Without Backend (Local Storage Mode)

The app works with just the frontend! It will use browser's localStorage:

```bash
cd frontend
npm install
npm run dev
```

**Note:** Data will be saved in browser only, lost on clear cache.

## Project Structure

```
ExpensePilot/
├── frontend/                 # React + Vite
│   ├── src/
│   │   ├── components/      # React components
│   │   ├── services/        # API services
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   ├── vite.config.js
│   ├── tailwind.config.js
│   └── .env
├── backend/                  # Node.js + Express
│   ├── models/              # MongoDB schemas
│   ├── controllers/         # Business logic
│   ├── routes/              # API routes
│   ├── server.js
│   ├── package.json
│   └── .env
├── README.md
└── .gitignore
```

## API Endpoints

### Expenses

- `GET /api/expenses` - Get all expenses
- `POST /api/expenses` - Create expense
- `PUT /api/expenses/:id` - Update expense
- `DELETE /api/expenses/:id` - Delete expense
- `GET /api/expenses/summary` - Get summary stats

### Budget

- `GET /api/budget` - Get budget
- `PUT /api/budget` - Update budget

### Health

- `GET /api/health` - Check server status
- `GET /` - Server info

## Environment Variables

### Backend (.env)

```
MONGODB_URI=mongodb://localhost:27017/expensepilot
PORT=5000
NODE_ENV=development
```

### Frontend (.env)

```
VITE_API_URL=http://localhost:5000/api
```

## Building for Production

### Frontend

```bash
cd frontend
npm run build
```

Output in `frontend/dist/` - deploy this folder to Vercel, Netlify, or any static host.

### Backend

Backend is ready for deployment as-is. Deploy to:
- Render.com
- Railway.app
- Heroku
- AWS Elastic Beanstalk
- DigitalOcean App Platform

## Development Tips

### Hot Reload

Both frontend and backend support file watching:
- **Frontend:** Changes reload automatically (Vite)
- **Backend:** `npm start` watches for changes (with `--watch` flag)

### Database Inspection

For local MongoDB:
```bash
# Install MongoDB Compass (GUI)
# Or use MongoDB Shell
mongosh

# Show databases
show dbs

# Use database
use expensepilot

# Show collections
show collections

# View expenses
db.expenses.find()
```

### API Testing

Use Postman or cURL:

```bash
# Get all expenses
curl http://localhost:5000/api/expenses

# Add expense
curl -X POST http://localhost:5000/api/expenses \
  -H "Content-Type: application/json" \
  -d '{
    "amount": 500,
    "description": "Lunch",
    "category": "food",
    "date": "2024-01-15",
    "paidBy": "John"
  }'

# Get budget
curl http://localhost:5000/api/budget

# Update budget
curl -X PUT http://localhost:5000/api/budget \
  -H "Content-Type: application/json" \
  -d '{"amount": 10000}'
```

## Useful Commands

### Backend

```bash
# Start in production mode
NODE_ENV=production npm start

# Run with nodemon (auto-restart on changes)
npx nodemon server.js
```

### Frontend

```bash
# Build for production
npm run build

# Preview production build
npm run preview

# Check code quality
npm run lint
```

## Getting Help

1. Check the logs in terminal
2. Verify .env files are configured correctly
3. Ensure MongoDB is running
4. Check if ports 5000 and 5173 are available
5. Try clearing browser cache (Ctrl+Shift+Delete)

## Next Steps

After setup:

1. Add your first expense
2. Try editing and deleting
3. Check the charts
4. Toggle dark mode
5. Explore team contributions

Happy budgeting! 🎉
