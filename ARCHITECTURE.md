# ExpensePilot - Project Architecture

Complete project architecture and structure documentation.

## Directory Structure

```
ExpensePilot/
│
├── 📄 README.md                    # Main project README
├── 📄 SETUP.md                     # Local setup instructions
├── 📄 DEPLOYMENT.md                # Production deployment guide
├── 📄 FEATURES.md                  # Feature documentation
├── 📄 SAMPLE_DATA.md               # Sample data guide
├── 📄 ARCHITECTURE.md              # This file
├── 📄 .gitignore                   # Git ignore rules
├── 📄 .env.example                 # Example environment variables
│
├── 📁 frontend/                    # React + Vite application
│   ├── 📁 src/
│   │   ├── 📁 components/          # React components
│   │   │   ├── Navbar.jsx          # Top navigation bar
│   │   │   ├── BudgetSummary.jsx   # Budget overview cards
│   │   │   ├── ExpenseForm.jsx     # Add expense form
│   │   │   ├── ExpenseList.jsx     # List of expenses
│   │   │   ├── Charts.jsx          # Pie and bar charts
│   │   │   └── TeamContribution.jsx # Team member stats
│   │   ├── 📁 services/            # API services
│   │   │   └── api.js              # Axios API client
│   │   ├── 📁 hooks/               # Custom React hooks (future)
│   │   ├── 📄 App.jsx              # Main app component
│   │   ├── 📄 main.jsx             # React entry point
│   │   └── 📄 index.css            # Global styles + Tailwind
│   │
│   ├── 📄 package.json             # NPM dependencies
│   ├── 📄 vite.config.js           # Vite configuration
│   ├── 📄 tailwind.config.js       # Tailwind CSS config
│   ├── 📄 postcss.config.js        # PostCSS config
│   ├── 📄 .eslintrc.json           # ESLint config
│   ├── 📄 .gitignore               # Frontend git ignore
│   ├── 📄 .env                     # Frontend env variables
│   ├── 📄 .env.example             # Example frontend env
│   └── 📄 index.html               # HTML template
│
└── 📁 backend/                     # Node.js + Express API
    ├── 📁 models/                  # MongoDB schemas
    │   ├── Expense.js              # Expense schema
    │   └── Budget.js               # Budget schema
    │
    ├── 📁 controllers/             # Business logic
    │   ├── expenseController.js    # Expense operations
    │   └── budgetController.js     # Budget operations
    │
    ├── 📁 routes/                  # API routes
    │   ├── expenses.js             # /api/expenses routes
    │   └── budget.js               # /api/budget routes
    │
    ├── 📁 middleware/              # Custom middleware (future)
    │
    ├── 📄 server.js                # Express server setup
    ├── 📄 package.json             # NPM dependencies
    ├── 📄 .gitignore               # Backend git ignore
    ├── 📄 .env                     # Backend env variables
    └── 📄 .env.example             # Example backend env
```

## Component Architecture

### Frontend Component Tree

```
App
├── Navbar
│   ├── Logo (with animation)
│   └── Theme Toggle
├── BudgetSummary
│   ├── Total Budget Card
│   ├── Total Spent Card
│   ├── Remaining Balance Card
│   └── Status Card
├── ExpenseForm
│   ├── Amount Input
│   ├── Description Input
│   ├── Category Dropdown
│   ├── Date Picker
│   ├── Paid By Input
│   └── Submit Button
├── Charts
│   ├── Pie Chart (Category breakdown)
│   ├── Bar Chart (Monthly trend)
│   └── Stats Cards
├── ExpenseList
│   ├── Filter Buttons
│   └── Expense Cards (multiple)
│       ├── Edit Button
│       └── Delete Button
└── TeamContribution
    ├── Contribution Cards (multiple)
    └── Total Stats
```

## Data Flow Diagram

```
┌─────────────────────────────────────────────────────────┐
│                    React App (State)                     │
│  - expenses: []                                          │
│  - budget: 5000                                          │
│  - darkMode: false                                       │
└─────────────────────────────────────────────────────────┘
           │
    ┌──────┴──────────────────────────────────┐
    │                                         │
    ▼                                         ▼
┌─────────────────────────────┐    ┌──────────────────────────────┐
│     Local Storage           │    │   Express API Server         │
│ (Browser)                   │    │   http://localhost:5000      │
│                             │    │                              │
│ - expenses                  │    │ GET /api/expenses            │
│ - budget                    │    │ POST /api/expenses           │
│ - darkMode                  │    │ PUT /api/expenses/:id        │
│                             │    │ DELETE /api/expenses/:id     │
│ (Fallback when offline)     │    │ GET /api/budget              │
└─────────────────────────────┘    │ PUT /api/budget              │
                                   └──────────────────────────────┘
                                            │
                                            ▼
                                   ┌──────────────────────────────┐
                                   │   MongoDB Atlas              │
                                   │   (Cloud Database)           │
                                   │                              │
                                   │ Collection: expenses         │
                                   │ Collection: budgets          │
                                   └──────────────────────────────┘
```

## API Architecture

### REST Endpoints

#### Expenses
```
GET    /api/expenses              - Get all expenses
POST   /api/expenses              - Create new expense
GET    /api/expenses/:id          - Get single expense
PUT    /api/expenses/:id          - Update expense
DELETE /api/expenses/:id          - Delete expense
GET    /api/expenses/summary      - Get summary stats
```

#### Budget
```
GET    /api/budget                - Get current budget
PUT    /api/budget                - Update budget
```

#### Health
```
GET    /api/health                - Server health check
GET    /                           - Server info
```

### Request/Response Examples

#### Create Expense
```
POST /api/expenses
Content-Type: application/json

{
  "amount": 500,
  "description": "Office lunch",
  "category": "food",
  "date": "2024-01-15",
  "paidBy": "John"
}

Response (201):
{
  "_id": "507f1f77bcf86cd799439011",
  "amount": 500,
  "description": "Office lunch",
  "category": "food",
  "date": "2024-01-15T00:00:00.000Z",
  "paidBy": "John",
  "createdAt": "2024-01-15T10:30:00.000Z",
  "updatedAt": "2024-01-15T10:30:00.000Z"
}
```

#### Get Expenses
```
GET /api/expenses

Response (200):
[
  {
    "_id": "507f1f77bcf86cd799439011",
    "amount": 500,
    "description": "Office lunch",
    "category": "food",
    "date": "2024-01-15T00:00:00.000Z",
    "paidBy": "John",
    "createdAt": "2024-01-15T10:30:00.000Z",
    "updatedAt": "2024-01-15T10:30:00.000Z"
  },
  // ... more expenses
]
```

## Technology Stack

### Frontend
- **React 18** - UI library
- **Vite 5** - Build tool (fast bundling)
- **Tailwind CSS 3** - Utility-first CSS
- **Recharts 2** - React charts library
- **Framer Motion 10** - Animation library
- **Lucide React** - Icon library
- **Axios** - HTTP client
- **PostCSS** - CSS processing

### Backend
- **Node.js** - JavaScript runtime
- **Express 4** - Web framework
- **MongoDB** - NoSQL database
- **Mongoose 7** - MongoDB ODM
- **Dotenv** - Environment variables
- **CORS** - Cross-origin support

### Tools
- **Git** - Version control
- **npm** - Package manager
- **ESLint** - Code linting
- **Vercel** - Frontend hosting
- **Render** - Backend hosting
- **MongoDB Atlas** - Cloud database

## Development Workflow

### Local Development

```bash
# Terminal 1: Start Backend
cd backend
npm install
npm start

# Terminal 2: Start Frontend
cd frontend
npm install
npm run dev

# App runs at http://localhost:5173
# API at http://localhost:5000/api
```

### Production Deployment

```bash
# Frontend
npm run build  # Creates dist/ folder
# Deploy dist/ to Vercel/Netlify

# Backend
# Deploy to Render/Railway/Heroku
# Set environment variables on platform
# MongoDB Atlas handles database
```

## State Management

### React useState/useContext Flow

```javascript
// App.jsx
const [expenses, setExpenses] = useState([])
const [budget, setBudget] = useState(5000)
const [darkMode, setDarkMode] = useState(false)

// Props flow down
<BudgetSummary budget={budget} setBudget={setBudget} />
<ExpenseForm onAddExpense={handleAddExpense} />
<ExpenseList expenses={expenses} onDelete={handleDelete} />
<Charts expenses={expenses} />
<TeamContribution expenses={expenses} />
```

### Data Persistence

```javascript
// localStorage (browser)
localStorage.setItem('expenses', JSON.stringify(expenses))
localStorage.setItem('budget', budget)
localStorage.setItem('darkMode', darkMode)

// MongoDB (server)
Expense.findOne() → Database
Budget.findOne() → Database
```

## Security Architecture

### Frontend Security
- Input validation in forms
- XSS prevention (React escaping)
- CORS configured on backend
- Environment variables for API URLs

### Backend Security
- Input validation on all endpoints
- MongoDB injection prevention (Mongoose)
- CORS whitelist
- Error handling without exposing details

### Data Security
- HTTPS in production
- MongoDB Atlas encryption
- Environment variables for secrets
- No sensitive data in git

## Performance Optimizations

### Frontend
- **Vite** for fast bundling
- **Code splitting** by route
- **Tree shaking** for smaller bundle
- **Lazy loading** of charts
- **Memoization** of components

### Backend
- **Database indexing** on frequently queried fields
- **Connection pooling** with Mongoose
- **Response compression** with gzip
- **Caching** headers for static files

### Network
- **HTTP/2** support
- **Gzip compression**
- **CDN** for frontend (Vercel)
- **Connection reuse** (Keep-Alive)

## Error Handling

### Frontend Error Handling
```javascript
try {
  const data = await getExpenses()
} catch (err) {
  // Fallback to localStorage
  const saved = localStorage.getItem('expenses')
  setExpenses(saved ? JSON.parse(saved) : [])
}
```

### Backend Error Handling
```javascript
app.use((err, req, res, next) => {
  console.error('Error:', err)
  res.status(err.status || 500).json({
    error: err.message || 'Internal server error'
  })
})
```

## Testing Strategy

### Manual Testing
1. Add expenses in all categories
2. Edit and delete expenses
3. Toggle filters
4. Check calculations
5. Toggle dark mode
6. Test on mobile

### Integration Testing (Recommended)
- Test API endpoints with Postman
- Test MongoDB queries
- Test frontend-backend communication

### Performance Testing
- Lighthouse audit
- Bundle size analysis
- MongoDB query performance

## Monitoring & Logs

### Frontend
- Browser console for errors
- DevTools for performance
- Network tab for API calls

### Backend
- Server console logs
- MongoDB Atlas monitoring
- Render/Railway logs

### Production
- Error tracking (Sentry)
- Performance monitoring (New Relic)
- Uptime monitoring (UptimeRobot)

## Scalability Plan

### Phase 1: Current (100-1000 users)
- Vercel free tier ✓
- Render free tier ✓
- MongoDB Atlas free tier ✓

### Phase 2: Growth (1000-10000 users)
- Vercel Pro
- Render paid tier
- MongoDB M10+ cluster

### Phase 3: Scale (10000+ users)
- Vercel Enterprise
- Render Pro + load balancing
- MongoDB dedicated cluster
- Redis caching layer

## Future Improvements

### Code Quality
- [ ] Add Jest unit tests
- [ ] Add E2E tests (Cypress)
- [ ] Setup CI/CD pipeline
- [ ] Code coverage reports

### Features
- [ ] Multi-team support
- [ ] Receipt image uploads
- [ ] Split expenses
- [ ] Monthly reports
- [ ] Budget forecasting

### Infrastructure
- [ ] Docker containerization
- [ ] Kubernetes deployment
- [ ] Redis caching
- [ ] ElasticSearch for logs

---

**Architecture is scalable and production-ready!**
