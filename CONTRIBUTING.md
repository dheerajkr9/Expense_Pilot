# Contributing to ExpensePilot

Thank you for your interest in contributing to ExpensePilot! This guide will help you understand our workflow and how to contribute effectively.

## Table of Contents

- [Code of Conduct](#code-of-conduct)
- [Getting Started](#getting-started)
- [Development Workflow](#development-workflow)
- [Coding Standards](#coding-standards)
- [Commit Guidelines](#commit-guidelines)
- [Pull Request Process](#pull-request-process)
- [Reporting Issues](#reporting-issues)

## Code of Conduct

Be respectful, inclusive, and constructive. We want a positive community for everyone.

## Getting Started

### 1. Fork & Clone

```bash
# Fork on GitHub
# Clone your fork
git clone https://github.com/YOUR_USERNAME/expensepilot.git
cd expensepilot

# Add upstream
git remote add upstream https://github.com/ORIGINAL/expensepilot.git
```

### 2. Create Branch

```bash
# Update main
git fetch upstream
git checkout main
git merge upstream/main

# Create feature branch
git checkout -b feature/your-feature-name
```

### 3. Install & Run

```bash
# Backend
cd backend
npm install
npm start

# Frontend (new terminal)
cd frontend
npm install
npm run dev
```

## Development Workflow

### Frontend Development

**File Structure:**
```
frontend/src/
├── components/          # React components
├── services/           # API calls
├── hooks/              # Custom hooks
├── assets/             # Images, icons
├── App.jsx
└── main.jsx
```

**Creating a New Component:**
```javascript
// src/components/MyComponent.jsx
import { motion } from 'framer-motion'

export default function MyComponent() {
  return (
    <motion.div
      initial={{ opacity: 0 }}
      animate={{ opacity: 1 }}
      className="p-6 card"
    >
      {/* Your component */}
    </motion.div>
  )
}
```

**Styling:**
- Use Tailwind CSS classes
- Avoid inline styles
- Use `dark:` prefix for dark mode
- Reference custom classes in `index.css`

### Backend Development

**File Structure:**
```
backend/
├── models/             # MongoDB schemas
├── controllers/        # Business logic
├── routes/             # API endpoints
└── server.js
```

**Creating a New Route:**
```javascript
// routes/example.js
import express from 'express'
import { getExample } from '../controllers/exampleController.js'

const router = express.Router()
router.get('/', getExample)

export default router
```

**Validation:**
```javascript
// In controller
if (!amount || amount <= 0) {
  return res.status(400).json({ error: 'Invalid amount' })
}
```

## Coding Standards

### JavaScript/React

- Use **ES6+ syntax** (arrow functions, const/let, template literals)
- Use **functional components** with hooks
- **Meaningful variable names** (not `x`, `tmp`, `foo`)
- **Comments for complex logic** only
- **No console.log** in production code (use proper logging)

### Style Guide

```javascript
// ✅ Good
const handleAddExpense = async (expense) => {
  try {
    const result = await addExpense(expense)
    setExpenses([...expenses, result])
  } catch (error) {
    console.error('Failed to add expense:', error)
  }
}

// ❌ Bad
async function handle(e){
const r=await a(e);s([...e,r]);}
```

### CSS/Tailwind

```html
<!-- ✅ Good -->
<div className="p-4 rounded-lg bg-white dark:bg-slate-800 hover:shadow-lg">

<!-- ❌ Bad -->
<div className="p-4" style={{backgroundColor: 'white'}}>
```

### Naming Conventions

- **Components**: PascalCase (`MyComponent.jsx`)
- **Functions**: camelCase (`handleClick`, `getExpenses`)
- **Constants**: UPPER_SNAKE_CASE (`MAX_BUDGET`, `DEFAULT_CATEGORY`)
- **Files**: kebab-case or PascalCase (components use PascalCase)

## Commit Guidelines

### Commit Message Format

```
<type>(<scope>): <subject>

<body>

<footer>
```

**Types:**
- `feat`: New feature
- `fix`: Bug fix
- `docs`: Documentation
- `style`: Formatting
- `refactor`: Code restructuring
- `test`: Adding tests
- `chore`: Build/tooling changes

**Examples:**
```bash
git commit -m "feat(expenses): add category filter"
git commit -m "fix(charts): fix pie chart rendering"
git commit -m "docs: update setup instructions"
git commit -m "refactor(api): simplify expense fetching"
```

### Commit Practices

- Commit frequently with meaningful messages
- One feature per commit
- Test before committing
- Don't commit commented-out code
- Use `git rebase` to clean up commits before PR

## Pull Request Process

### 1. Before Creating PR

```bash
# Update your branch
git fetch upstream
git rebase upstream/main

# Run linter
npm run lint

# Test your changes
# - Manually test UI changes
# - Test API endpoints
# - Check on mobile
```

### 2. Create PR

**Title Format:**
```
[feature/fix/docs] Brief description
```

**PR Template:**
```markdown
## Description
What does this PR do?

## Type
- [ ] Feature
- [ ] Bug Fix
- [ ] Documentation

## Related Issues
Fixes #123

## Changes
- Change 1
- Change 2

## Testing
How to test this?

## Screenshots
If UI change, add screenshots

## Checklist
- [ ] Tested locally
- [ ] No breaking changes
- [ ] Documentation updated
- [ ] Code follows style guide
```

### 3. Code Review

- Respond to comments constructively
- Request changes if needed
- Approve once satisfied
- Merge when approved

## Reporting Issues

### Issue Template

**Title:** Clear, concise description

**Description:**
```markdown
## Bug / Feature Request
[Describe the issue]

## Steps to Reproduce (if bug)
1. Step 1
2. Step 2
3. Step 3

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Environment
- OS: Windows/Mac/Linux
- Browser: Chrome/Firefox/Safari
- Node version: 16/18
- MongoDB: Local/Atlas

## Screenshots
[If applicable]

## Additional Context
[Any other information]
```

## Testing Guidelines

### Frontend Testing

```javascript
// Test user interactions
- Add expense
- Edit expense
- Delete expense
- Filter by category
- Toggle dark mode
- Check responsive layout
```

### Backend Testing

```bash
# Test API endpoints
curl -X GET http://localhost:5000/api/expenses
curl -X POST http://localhost:5000/api/expenses \
  -H "Content-Type: application/json" \
  -d '{"amount": 100, ...}'
```

### Manual Testing Checklist

- [ ] Feature works as expected
- [ ] No console errors
- [ ] Responsive on mobile
- [ ] Works offline (browser storage)
- [ ] Dark mode looks good
- [ ] No broken animations
- [ ] Form validation works

## Performance Guidelines

### Frontend
- Keep bundle size under 200KB
- Optimize images
- Lazy load heavy components
- Memoize expensive computations

### Backend
- Use database indexes
- Limit query results
- Cache when possible
- Handle errors gracefully

## Security Considerations

- Never commit `.env` files or secrets
- Validate all user inputs
- Sanitize database queries
- Use HTTPS in production
- Keep dependencies updated

## Documentation

When adding features:
1. Update code comments
2. Update relevant `.md` files
3. Update FEATURES.md
4. Add examples in SAMPLE_DATA.md

## Getting Help

- **Questions?** Open a discussion
- **Found a bug?** Create an issue
- **Want to suggest feature?** Create a feature request
- **Need help?** Comment on related issues

## Community

- Be kind and respectful
- Assume good intentions
- Help other contributors
- Share knowledge

## License

By contributing, you agree your code will be under the MIT License.

## Acknowledgments

Thank you for contributing to making ExpensePilot better! 🎉

---

**Happy coding! Feel free to reach out if you have questions.**
