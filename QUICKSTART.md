# ExpensePilot - Quick Start ⚡

Get ExpensePilot running in 5 minutes!

## 30-Second Setup

```bash
# Terminal 1: Backend
cd backend
npm install
npm start

# Terminal 2: Frontend (open new terminal)
cd frontend
npm install
npm run dev
```

**Done!** Visit `http://localhost:5173` 🎉

## Common Issues & Quick Fixes

### Port Already in Use
```bash
# Kill process on port 5000
lsof -i :5000 | grep LISTEN | awk '{print $2}' | xargs kill -9

# Or just restart your terminal
```

### MongoDB Connection Error
**Solution:** It's ok! The app works without MongoDB (uses browser storage)
- Add MongoDB later when you need cloud sync

### Vite Port Issue
```bash
# Kill port 5173
lsof -i :5173 | grep LISTEN | awk '{print $2}' | xargs kill -9

# Vite will auto-switch if busy
```

## What You Get

✅ **Fully Working Team Budget Tracker**
- Add, edit, delete expenses
- Real-time budget calculations
- Beautiful charts and analytics
- Dark mode support
- Team contribution tracking
- Works offline (with fallback storage)

## First Steps

1. Open `http://localhost:5173`
2. Set budget (default 5000)
3. Add expense using the form
4. See it appear in the list
5. Check charts and summaries
6. Try dark mode (moon icon)

## Adding MongoDB (Optional)

Want to sync data across devices? Add MongoDB:

1. Sign up at [MongoDB Atlas](https://www.mongodb.com/cloud/atlas)
2. Create free cluster
3. Create database user
4. Get connection string
5. Add to `backend/.env`:
   ```
   MONGODB_URI=mongodb+srv://user:pass@cluster.mongodb.net/expensepilot
   ```
6. Restart backend

## Deployment Ready

When you want to go live:

```bash
# Frontend to Vercel (1 click)
# Backend to Render (1 click)
# Database ready at MongoDB Atlas

# See DEPLOYMENT.md for details
```

## Documentation

- **[SETUP.md](./SETUP.md)** - Detailed setup
- **[FEATURES.md](./FEATURES.md)** - Feature list
- **[DEPLOYMENT.md](./DEPLOYMENT.md)** - Production deployment
- **[SAMPLE_DATA.md](./SAMPLE_DATA.md)** - Add test data
- **[ARCHITECTURE.md](./ARCHITECTURE.md)** - Tech architecture

## Tech Stack at a Glance

```
Frontend: React + Vite + Tailwind + Recharts
Backend:  Express + MongoDB + Mongoose
Hosting:  Vercel + Render + MongoDB Atlas
```

## Keyboard Shortcuts

- `Tab` - Navigate form fields
- `Enter` - Submit form
- `Delete` - Remove expense (after clicking)

## Commands Cheat Sheet

```bash
# Backend
npm start          # Start server
npm run dev        # Start with auto-reload (need nodemon)

# Frontend
npm run dev        # Start dev server
npm run build      # Build for production
npm run preview    # Preview production build

# Both
npm install        # Install dependencies
npm run lint       # Check code quality
```

## Default Behavior

- **Budget**: 5000 (editable)
- **Storage**: Browser's localStorage
- **API**: http://localhost:5000/api
- **Port**: 5173 (frontend), 5000 (backend)
- **Database**: Optional (works without it!)

## Troubleshooting One-Liner

```bash
# Nuclear option - clean install
rm -rf node_modules package-lock.json
npm install
npm start
```

## Next: Add Sample Data

See expenses in action:

1. Go to [SAMPLE_DATA.md](./SAMPLE_DATA.md)
2. Add 12 test expenses
3. Explore charts and analytics
4. Try filtering by category
5. Check team contributions

## Need Help?

1. Check [SETUP.md](./SETUP.md) - Most common issues covered
2. Verify Node.js installed: `node --version`
3. Verify npm installed: `npm --version`
4. Check ports are free: `lsof -i :5000` / `lsof -i :5173`
5. Clear cache: `rm -rf node_modules && npm install`

## Pro Tips

💡 **Tip 1:** Use localhost IP for mobile testing
```bash
# Find your IP: ipconfig (Windows) or ifconfig (Mac/Linux)
# Visit: http://YOUR_IP:5173
```

💡 **Tip 2:** Keep terminal windows visible to see logs

💡 **Tip 3:** Browser DevTools → Application → localStorage to see data

💡 **Tip 4:** Stop servers with `Ctrl+C` in terminal

## What's Next?

1. **For Testing**: Load sample data (SAMPLE_DATA.md)
2. **For Development**: Read ARCHITECTURE.md
3. **For Deployment**: Follow DEPLOYMENT.md
4. **For Features**: Check FEATURES.md

## Project Stats

- **Frontend Files**: ~2000 lines
- **Backend Files**: ~400 lines
- **Components**: 7 major components
- **Routes**: 8 API endpoints
- **Animations**: Framer Motion throughout
- **Database**: MongoDB optional but recommended

## Success Checklist ✓

- [ ] Backend running on :5000
- [ ] Frontend running on :5173
- [ ] Can add expense in UI
- [ ] Expense appears in list
- [ ] Budget displays correctly
- [ ] Charts render
- [ ] Dark mode works
- [ ] Can edit/delete expenses

**All green? You're ready to use ExpensePilot! 🚀**

---

**Questions?** Check the docs above or review the code - it's well-commented!

**Want to deploy?** See [DEPLOYMENT.md](./DEPLOYMENT.md)

**Happy budgeting! 💰**
