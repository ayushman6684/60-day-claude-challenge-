# Day 42 — Personal Financial Command Center
## Demo Video
Watch the walkthrough here: https://drive.google.com/file/d/1RI-QXu1fcGyLvcqLpEr7SOb76XeJ-UAv/view?usp=sharing
## What I built
A single-page HTML financial dashboard ("Personal Financial Command Center") 
tailored for a student profile — tracking pocket money, expenses, subscriptions, 
savings goals, and basic investing concepts (SIP simulator), all in one 
self-contained file using vanilla HTML, CSS, and JavaScript (no frameworks).

## Key features
- Overview dashboard with income/expense summary, cash flow chart, and category breakdown
- AI-style insights and a rule-based Financial Health Score (savings rate, budget 
  discipline, subscription load, emergency buffer)
- Income & Expense trackers with category-wise budgeting (Needs / Wants / Future-you split)
- Subscription tracker to catch recurring costs
- Savings goals with an animated "coin jar" progress visual
- SIP (Systematic Investment Plan) growth simulator with adjustable sliders
- What-If simulator to model the impact of spending cuts or extra income
- Printable monthly report, dark/light mode, and local storage persistence — 
  no backend, no external calls

## Key learnings
1. **Timezone bugs are sneaky.** Using `Date.toISOString()` to get a date/month 
   string silently converts to UTC — for any timezone ahead of UTC (like India, 
   UTC+5:30), this can shift the reported date/month backward by one, breaking 
   month-based aggregations. Fixed by building date strings from local 
   `getFullYear()` / `getMonth()` / `getDate()` instead of going through UTC.
2. **Canvas charts without libraries** are very doable — bar, pie/donut, and line 
   charts can all be hand-rolled with basic `<canvas>` 2D context calls, keeping 
   the file dependency-free.
3. **LocalStorage as the only backend** works well for personal, single-user 
   tools, but requires careful default/fallback handling (e.g. don't let a 
   fallback value silently mask a real zero).
4. **Rule-based "AI insights"** (savings rate thresholds, budget overage checks, 
   subscription-load percentage) can feel personalized without needing an actual 
   model — just clear thresholds tied to the user's real data.

## Files in this folder
- `Personal-Financial-Command-Center.html` — the finished dashboard
- Screenshots of the dashboard in use   





# Personal Financial Command Center

You are an expert financial planner, budgeting specialist, investment advisor, UI/UX designer, data visualization expert, and senior frontend developer.

Before generating anything, ask the user the following questions ONE AT A TIME in MCQ format only, with typed input only as the last option.

1. Who is this financial dashboard for?
(Offer options such as Student, Salaried Employee, Freelancer, Business Owner, Family, Investor, Retired, etc.)

2. Continue asking follow-up questions until the user's financial profile has been narrowed sufficiently to personalize the dashboard.
Do not stop after identifying only the user type. Use your own judgment to determine when enough information has been collected.

3. Would you like Claude to automatically design the dashboard, or would you like to customize the modules?
If the user chooses customization, ask which financial modules they want included.

After collecting all responses, generate a premium single-page HTML application called **"Personal Financial Command Center."**

The application should help users understand, manage, and improve their financial health through an interactive dashboard rather than acting as a simple expense tracker.

Include an overview dashboard followed by relevant financial modules based on the user's profile. These may include income, expenses, budgets, savings, debt, loans, investments, subscriptions, goals, cash flow, financial insights, calculators, planning tools, reports, and visualizations where appropriate.

Include interactive charts, financial summaries, AI-generated recommendations, "what-if" simulations, progress tracking, and a financial health score tailored to the user's situation.

Conclude with financial tips, planning checklists, useful resources, and additional AI prompts for improving financial literacy.

Generate everything as a single self-contained HTML file using only HTML, CSS, and JavaScript without external libraries or frameworks.

Design the interface as a polished commercial financial platform with responsive design, dark mode, smooth animations, local storage, printable reports, and an intuitive user experience.