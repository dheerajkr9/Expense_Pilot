# ExpensePilot Pro - Income & Expense Tracker

A modern team budget tracker that helps users manage expenses, categorize spending, and visualize data with interactive charts. Built with React and Tailwind CSS, it features a clean UI, smooth animations, and real-time insights for smarter financial decisions.

## 🌐 Live Demo

**Visit:** [https://dheerajkr9.github.io/Expense_Pilot/](https://dheerajkr9.github.io/Expense_Pilot/)

## ✨ Features

- 📊 **Real-time Dashboard**: View income, expenses, and net balance at a glance
- 💰 **Income Tracking**: Add and track multiple income sources
- 💳 **Expense Management**: Categorize and manage all your expenses
- 📈 **Analytics & Insights**: Visualize spending distribution and income sources
- 🎯 **Category Breakdown**: Detailed breakdown by category with percentages
- 🌙 **Dark Mode**: Toggle between light and dark themes
- 📱 **Fully Responsive**: Works seamlessly on desktop, tablet, and mobile
- 💾 **Local Storage**: All data is saved in your browser (100% private)
- ⚡ **Offline Support**: Works without internet connection
- 🎨 **Beautiful UI**: Modern design with smooth animations

## 🚀 Features

### Overview Tab
- Total Income, Expense, and Net Balance cards
- Income vs Expense comparison
- Spending Distribution pie chart
- Income Sources breakdown
- Recent Transactions (last 10)

### Income Tab
- Add new income entries
- Income summary by category
- Complete income history
- Delete individual income entries

### Expense Tab
- Add new expense entries
- Expense summary by category
- Complete expense history
- Delete individual expense entries

## 💻 Tech Stack

- **React 18**: For building the UI
- **Tailwind CSS**: For styling
- **Vite**: Build tool (optional, main app runs in browser)
- **LocalStorage API**: For data persistence

## 📥 Installation

### Option 1: Use the Live Version
Simply visit: https://dheerajkr9.github.io/Expense_Pilot/

### Option 2: Run Locally

1. Clone the repository:
```bash
git clone https://github.com/dheerajkr9/Expense_Pilot.git
cd Expense_Pilot
```

2. Open `index.html` in your browser:
```bash
# On macOS
open index.html

# On Windows
start index.html

# Or use a local server
python -m http.server 8000
# Then visit http://localhost:8000
```

### Option 3: With Node.js

1. Install dependencies:
```bash
npm install
```

2. Start development server:
```bash
npm run dev
```

3. Build for production:
```bash
npm run build
```

## 📊 How to Use

### Adding Income
1. Click the **"💵 Income"** tab
2. Fill in the income form:
   - Enter amount (in ₹)
   - Add description
   - Select category
   - Choose date
   - Enter source name
3. Click **"✅ Add Income"**

### Adding Expenses
1. Click the **"💳 Expense"** tab
2. Fill in the expense form:
   - Enter amount (in ₹)
   - Add description
   - Select category
   - Choose date
   - Enter payer name
3. Click **"➕ Add Expense"**

### Viewing Analytics
1. Click the **"📈 Overview"** tab to see:
   - Total income and expenses
   - Net balance and savings rate
   - Spending distribution
   - Income sources breakdown
   - Recent transactions

### Toggling Dark Mode
- Click the **"🌙"** or **"☀️"** button in the top-right corner

## 📁 Project Structure

```
Expense_Pilot/
├── index.html           # Main application file
├── app.html            # Alternative HTML version
├── package.json        # Project dependencies
├── package-lock.json   # Dependency lock file
├── tailwind.config.js  # Tailwind CSS configuration
├── vite.config.js      # Vite configuration
├── .github/
│   └── workflows/
│       └── deploy.yml  # GitHub Actions workflow
├── .nojekyll           # Jekyll disable file
└── README.md           # This file
```

## 💾 Data Storage

- All data is stored in your browser's **LocalStorage**
- No data is sent to any server
- Your financial data remains completely private
- Clear browser cache to reset all data

## 🔐 Privacy

- ✅ No backend server required
- ✅ No data collection
- ✅ No third-party tracking
- ✅ 100% client-side processing
- ✅ Works offline

## 🛠️ Customization

### Change Currency
Edit `index.html` and replace `₹` with your currency symbol (e.g., `$`, `€`, `£`)

### Add New Categories
In the `categoryEmojis` object in `index.html`, add new categories:
```javascript
const categoryEmojis = {
    food: '🍔',
    travel: '✈️',
    // Add your categories here
    cryptocurrency: '₿',
};
```

### Modify Colors
Update the gradient in `.navbar` CSS:
```css
background: linear-gradient(135deg, #YOUR_COLOR_1 0%, #YOUR_COLOR_2 100%);
```

## 📱 Browser Support

- Chrome/Edge (Latest)
- Firefox (Latest)
- Safari (Latest)
- Mobile browsers

## 🤝 Contributing

Contributions are welcome! Feel free to:
- Report bugs
- Suggest features
- Submit pull requests

## 📄 License

This project is open source and available for personal and commercial use.

## 🙏 Acknowledgments

- Built with React and Tailwind CSS
- Inspired by modern financial apps
- Created for team expense tracking

## 📞 Support

For issues or questions:
1. Check existing issues on GitHub
2. Open a new issue with details
3. Include screenshots if applicable

## 🚀 Deployment

This app is automatically deployed to GitHub Pages using GitHub Actions whenever you push to the `main` branch.

### Manual Deployment

1. Push changes to `main` branch
2. GitHub Actions automatically runs the workflow
3. Website updates within 1-2 minutes
4. Visit: https://dheerajkr9.github.io/Expense_Pilot/

---

**Built with ❤️ by ExpensePilot Team**
