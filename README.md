# ExpensePilot 💰

A modern, elegant team-based budget tracking web application with expense categories, visual insights, and real-time budget management.

## Features ✨

- **Add & Manage Expenses** - Track spending with categories and descriptions
- **Budget Summary** - View total budget, spent, and remaining balance
- **Visual Breakdown** - Pie and bar charts for category-wise spending
- **Team Support** - Track who added each expense and contribution per person
- **Dark/Light Mode** - Toggle between themes
- **Smooth Animations** - Modern UI with Framer Motion animations
- **Local Storage** - Fallback storage without backend
- **Responsive Design** - Works perfectly on mobile and desktop

## Categories 📂

- Food 🍔
- Travel ✈️
- Accommodation 🏠
- Utilities ⚡
- Miscellaneous 📌

## Tech Stack 🛠️

**Frontend:**
- React 18
- Vite (fast build tool)
- Tailwind CSS (styling)
- Recharts (visualizations)
- Framer Motion (animations)

**Backend:**
- Node.js + Express
- MongoDB
- Mongoose (ODM)
- Dotenv (environment variables)

## Project Structure 📁

```
ExpensePilot/
├── frontend/
│   ├── src/
│   │   ├── components/
│   │   ├── pages/
│   │   ├── services/
│   │   ├── hooks/
│   │   ├── assets/
│   │   ├── App.jsx
│   │   └── main.jsx
│   ├── package.json
│   └── vite.config.js
├── backend/
│   ├── models/
│   ├── routes/
│   ├── controllers/
│   ├── middleware/
│   ├── server.js
│   └── package.json
├── README.md
├── .gitignore
└── .env.example
```

## Getting Started 🚀

### Prerequisites
- Node.js (v16+)
- npm or yarn
- MongoDB running locally or Atlas connection string

### Frontend Setup

```bash
cd frontend
npm install
npm run dev
```

The app will run on `http://localhost:5173`

### Backend Setup

```bash
cd backend
npm install
# Create .env file with MongoDB URI
npm start
```

The server will run on `http://localhost:5000`

### Environment Variables

Create a `.env` file in the backend folder:

```
MONGODB_URI=mongodb://localhost:27017/expensepilot
PORT=5000
NODE_ENV=development
```

Or use MongoDB Atlas:

```
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/expensepilot
PORT=5000
NODE_ENV=development
```

## How to Use 📖

1. **Add Budget**: Set your total budget in the summary section
2. **Add Expense**: Fill the expense form with amount, description, category, date, and who paid
3. **View Charts**: See visual breakdown of spending by category
4. **Edit/Delete**: Manage expenses from the list
5. **Track Team**: See who spent what in the contribution section

## Features in Detail 🎯

### Dashboard
- Clean card-based layout
- Animated counter displays
- Real-time budget calculations
- Status indicators (on track, warning, over budget)

### Charts
- **Pie Chart**: Category-wise spending distribution
- **Bar Chart**: Monthly spending trends
- Smooth animated transitions

### Expense Management
- Add, edit, delete expenses
- Filter by category
- Search functionality
- Date range filtering

### Theme Support
- Light mode (default)
- Dark mode toggle
- Smooth theme transitions

## API Endpoints 📡

### Expenses
- `GET /api/expenses` - Get all expenses
- `POST /api/expenses` - Add new expense
- `PUT /api/expenses/:id` - Update expense
- `DELETE /api/expenses/:id` - Delete expense

### Budget
- `GET /api/budget` - Get current budget
- `PUT /api/budget` - Update budget

## Deployment 🌐

### Vercel (Frontend)
1. Push code to GitHub
2. Connect repository to Vercel
3. Set environment variables
4. Deploy

### Render (Backend)
1. Push code to GitHub
2. Create new Web Service on Render
3. Set environment variables
4. Deploy

## Browser Support 🌐

- Chrome (latest)
- Firefox (latest)
- Safari (latest)
- Edge (latest)

## License 📄

MIT License - feel free to use for personal or commercial projects

## Support & Feedback 💬

Found a bug? Have a suggestion? Feel free to open an issue or contribute!

---

**Made with ❤️ for better budget management**
