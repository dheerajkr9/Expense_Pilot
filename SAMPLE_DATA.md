# ExpensePilot - Sample Data Guide

Guide for quickly populating ExpensePilot with sample data for testing and demonstration.

## Quick Sample Data Entry

### Method 1: Manual Entry (Easiest)

Use the ExpenseForm in the UI to add these expenses:

#### Team Outing - Week 1

1. **Office Lunch**
   - Amount: 2500
   - Description: Team lunch at Italian restaurant
   - Category: Food 🍔
   - Date: 2024-01-08
   - Paid By: Alice

2. **Travel for Meeting**
   - Amount: 1200
   - Description: Uber to client meeting
   - Category: Travel ✈️
   - Date: 2024-01-08
   - Paid By: Bob

3. **Office Snacks**
   - Amount: 800
   - Description: Coffee and snacks for team
   - Category: Food 🍔
   - Date: 2024-01-09
   - Paid By: Alice

#### Accommodation & Utilities - Week 2

4. **Internet Bill**
   - Amount: 1500
   - Description: Monthly internet bill
   - Category: Utilities ⚡
   - Date: 2024-01-10
   - Paid By: Carol

5. **Team Accommodation**
   - Amount: 8000
   - Description: Hotel for team conference
   - Category: Accommodation 🏠
   - Date: 2024-01-12
   - Paid By: David

6. **Parking**
   - Amount: 500
   - Description: Parking at conference hotel
   - Category: Miscellaneous 📌
   - Date: 2024-01-12
   - Paid By: Carol

#### Travel & Food - Week 3

7. **Client Dinner**
   - Amount: 3500
   - Description: Dinner with client at premium restaurant
   - Category: Food 🍔
   - Date: 2024-01-15
   - Paid By: Bob

8. **Flight Tickets**
   - Amount: 15000
   - Description: Round trip flights for 2 to client office
   - Category: Travel ✈️
   - Date: 2024-01-16
   - Paid By: David

9. **Taxi for Airport**
   - Amount: 600
   - Description: Pickup and drop to airport
   - Category: Travel ✈️
   - Date: 2024-01-16
   - Paid By: Alice

#### Miscellaneous Expenses - Week 4

10. **Office Supplies**
    - Amount: 2000
    - Description: Stationery and office supplies
    - Category: Miscellaneous 📌
    - Date: 2024-01-18
    - Paid By: Carol

11. **Team Breakfast**
    - Amount: 1200
    - Description: Breakfast before meeting
    - Category: Food 🍔
    - Date: 2024-01-19
    - Paid By: Bob

12. **Electricity Bill**
    - Amount: 2500
    - Description: Monthly electricity
    - Category: Utilities ⚡
    - Date: 2024-01-20
    - Paid By: Alice

## Method 2: Bulk Insert via API (Advanced)

### Using cURL

Save this as `load-sample-data.sh`:

```bash
#!/bin/bash

API_URL="http://localhost:5000/api"

echo "🚀 Loading sample data..."

# Array of sample expenses
expenses=(
  '{"amount": 2500, "description": "Team lunch at Italian restaurant", "category": "food", "date": "2024-01-08", "paidBy": "Alice"}'
  '{"amount": 1200, "description": "Uber to client meeting", "category": "travel", "date": "2024-01-08", "paidBy": "Bob"}'
  '{"amount": 800, "description": "Coffee and snacks for team", "category": "food", "date": "2024-01-09", "paidBy": "Alice"}'
  '{"amount": 1500, "description": "Monthly internet bill", "category": "utilities", "date": "2024-01-10", "paidBy": "Carol"}'
  '{"amount": 8000, "description": "Hotel for team conference", "category": "accommodation", "date": "2024-01-12", "paidBy": "David"}'
  '{"amount": 500, "description": "Parking at conference hotel", "category": "miscellaneous", "date": "2024-01-12", "paidBy": "Carol"}'
  '{"amount": 3500, "description": "Dinner with client at premium restaurant", "category": "food", "date": "2024-01-15", "paidBy": "Bob"}'
  '{"amount": 15000, "description": "Round trip flights for 2 to client office", "category": "travel", "date": "2024-01-16", "paidBy": "David"}'
  '{"amount": 600, "description": "Pickup and drop to airport", "category": "travel", "date": "2024-01-16", "paidBy": "Alice"}'
  '{"amount": 2000, "description": "Stationery and office supplies", "category": "miscellaneous", "date": "2024-01-18", "paidBy": "Carol"}'
  '{"amount": 1200, "description": "Breakfast before meeting", "category": "food", "date": "2024-01-19", "paidBy": "Bob"}'
  '{"amount": 2500, "description": "Monthly electricity", "category": "utilities", "date": "2024-01-20", "paidBy": "Alice"}'
)

# Insert each expense
for expense in "${expenses[@]}"; do
  echo "Adding: $expense"
  curl -X POST "$API_URL/expenses" \
    -H "Content-Type: application/json" \
    -d "$expense"
  echo ""
done

# Set budget
echo "Setting budget to 50000..."
curl -X PUT "$API_URL/budget" \
  -H "Content-Type: application/json" \
  -d '{"amount": 50000}'

echo "✅ Sample data loaded successfully!"
```

### Run the script:

```bash
chmod +x load-sample-data.sh
./load-sample-data.sh
```

## Method 3: MongoDB Direct Insert (For Advanced Users)

If you have MongoDB running locally:

```bash
mongosh

use expensepilot

db.expenses.insertMany([
  {
    "amount": 2500,
    "description": "Team lunch at Italian restaurant",
    "category": "food",
    "date": new Date("2024-01-08"),
    "paidBy": "Alice",
    "createdAt": new Date(),
    "updatedAt": new Date()
  },
  {
    "amount": 1200,
    "description": "Uber to client meeting",
    "category": "travel",
    "date": new Date("2024-01-08"),
    "paidBy": "Bob",
    "createdAt": new Date(),
    "updatedAt": new Date()
  },
  // ... add remaining expenses
])

db.budgets.insertOne({
  "amount": 50000,
  "createdAt": new Date(),
  "updatedAt": new Date()
})
```

## Sample Data Summary

### By Category

| Category | Total | Items |
|----------|-------|-------|
| 🍔 Food | 8000 | 4 |
| ✈️ Travel | 16800 | 3 |
| 🏠 Accommodation | 8000 | 1 |
| ⚡ Utilities | 4000 | 2 |
| 📌 Miscellaneous | 2500 | 2 |
| **TOTAL** | **39,300** | **12** |

### By Team Member

| Member | Total | Items |
|--------|-------|-------|
| Alice | 7100 | 4 |
| Bob | 6900 | 3 |
| Carol | 5500 | 3 |
| David | 23000 | 2 |
| **TOTAL** | **39,300** | **12** |

## Expected App Behavior

After loading sample data:

1. **Budget Summary**
   - Total Budget: 50,000
   - Total Spent: 39,300
   - Remaining: 10,700
   - Status: ✅ On Track (78.6%)

2. **Charts**
   - Pie chart shows category breakdown
   - Bar chart shows monthly trend
   - Food dominates (20%)
   - Travel is second (43%)

3. **Team Contribution**
   - David has highest contribution (58.5%)
   - Alice second (18%)
   - Bob third (17.5%)
   - Carol fourth (14%)

4. **Expense List**
   - 12 expenses total
   - Sorted by newest first
   - All categories represented
   - Filter works for each category

## Testing Scenarios

### Scenario 1: Budget Exceeded
Add expense:
- Amount: 15000
- Description: "Over budget test"
- Category: Food
- Paid By: Test User

**Expected:** Status changes to "Over Budget" (red)

### Scenario 2: Filter Testing
Click on each category filter:
- Food: Shows 4-5 items
- Travel: Shows 3 items
- Accommodation: Shows 1 item
- Utilities: Shows 2 items
- Miscellaneous: Shows 2 items

### Scenario 3: Edit & Delete
- Edit David's flight expense to 14000
- Delete Alice's parking expense
- Verify totals update immediately

### Scenario 4: Dark Mode
- Toggle dark mode
- Verify all text is readable
- Check charts display correctly

### Scenario 5: Mobile Responsiveness
- View on mobile (use DevTools)
- Form should stack vertically
- Cards should be full width
- Charts should adapt

## Cleanup

To clear all sample data:

### Via UI
- Click delete on each expense
- Or manually reset in DevTools → Application → localStorage

### Via MongoDB
```bash
mongosh
use expensepilot
db.expenses.deleteMany({})
db.budgets.deleteMany({})
```

### Via API
```bash
# This would need a DELETE all endpoint
# Currently: delete one by one via UI
```

## Recommendations

### For Demo/Presentation
- Use sample data
- Focus on charts and visualizations
- Show filtering capabilities
- Toggle dark mode
- Demonstrate team contribution

### For Production Testing
- Start with small amounts
- Test edge cases (0 amount, very large amounts)
- Test different categories
- Test team member names with special characters

### For Performance Testing
- Load 1000+ expenses
- Monitor page performance
- Check chart rendering time
- Test MongoDB query performance

## Tips

1. **Use Realistic Data**: Team members, actual descriptions
2. **Vary Dates**: Spread across multiple days/weeks
3. **Different Amounts**: Avoid same amounts
4. **Mix Categories**: Use all 5 categories
5. **Multiple People**: At least 3-4 team members

---

**Sample data ready? Start exploring ExpensePilot! 🎉**
