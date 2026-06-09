# Day 9 — Iterative Prompting & App Development (NutriScope)

## What I Built Today
Used Claude to build NutriScope — a complete Nutrition
Tracker app using iterative prompting in 2 stages.

---

## PROMPT 1 — Build MVP

### Prompt Used:
Build a complete single-file HTML application called NutriScope.

**Requirements:**
- Profile Inputs: Age, Gender, Height, Weight,
  Activity Level, Dietary Preference
- Food Logging: Add Food, Quantity, Unit,
  Editable Table, Remove Entry
- Food Database: 20 common Indian foods
  (Rice, Roti, Dal, Paneer, Curd, Chana, Rajma,
  Banana, Apple, Milk, Oats, Bread, Egg, Chicken,
  Fish, Potato, Poha, Idli, Dosa, Spinach)
- Track: Calories, Protein, Carbs, Fat, Fiber,
  Iron, Calcium, Vitamin C, Vitamin D, Vitamin B12
- Dashboard: Energy Progress, Macro Chart,
  Top Deficiencies, Nutrient Table
- Design: Premium SaaS UI, Dark Theme, Chart.js

### MVP Output:
- Single HTML file — fully functional
- 20 food database with macros + micros
- BMR/TDEE calculation based on profile
- Interactive food logging table
- Macro pie chart (Chart.js)
- Nutrient completion progress bars
- Mobile responsive dark theme UI

---

## PROMPT 2 — Enhanced Application

### Enhancements Added:
- CSV Upload for bulk food logging
- 40 more foods added (60 total)
- Additional micronutrients tracked
- 2-day meal planner
- Risk Analysis panel
- Educational Disclaimer
- Nutrition Sources citations
- Better Charts (line + doughnut)
- Advanced Recommendations engine

### Enhanced Output:
- 60+ food database
- 2-day comparative meal planning
- Risk indicators (deficiency + excess)
- Export to CSV functionality
- Advanced chart visualizations
- Dietary preference-based recommendations
- Educational disclaimers added

---

## Comparison: MVP vs Enhanced

| Feature | MVP (Prompt 1) | Enhanced (Prompt 2) |
|---------|---------------|---------------------|
| Food Database | 20 foods | 60+ foods |
| Micronutrients | 10 | 15+ |
| Meal Planning | None | 2-day planner |
| CSV Support | No | Upload + Export |
| Risk Analysis | Basic | Advanced |
| Charts | 2 charts | 5 charts |
| Recommendations | Basic | AI-powered |

---

## Key Learnings

1. Iterative prompting builds better apps than one-shot prompts
2. Claude can build complete working apps in a single HTML file
3. Prompt 1 = foundation, Prompt 2 = refinement strategy
4. Adding context in Prompt 2 ("enhance existing") is key
5. Single-file HTML apps are perfect for sharing/portfolio

---

## What Surprised Me Most
Claude built a fully functional nutrition calculator
with BMR/TDEE formulas, Chart.js visualizations,
and Indian food database — all in ONE HTML file
with zero backend needed. The iterative approach
made the second version dramatically better.

---

## Screenshots
[NutriScope MVP — Dashboard screenshot]
[NutriScope Enhanced — Full app screenshot]
[Food logging interface]
[Nutrient analysis charts]

---

## Files in This Folder
- day9.md — This documentation file
- nutri_mvp.html — MVP version (Prompt 1 output)
- nutri_enhanced.html — Enhanced version (Prompt 2 output)

---

*Built using Iterative Prompting with Claude AI*
*@Anthropic @ABTalksOnAI @AnilBajpai*
*#60DayClaudeChallenge*