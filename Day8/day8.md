# Day 8 — Personal Environmental Health Analyzer

## What I Built
A fully interactive Personal Environmental Health Analyzer dashboard that fetches real-time AQI and water quality data for Indian cities and provides personalized health insights.

## Prompt Used
Act as a Senior Data Analyst, Environmental Researcher, UX Designer, and Frontend Dashboard Developer.
Create a Claude Artifact called:
🌍 Personal Environmental Health Analyzer

DATA RULES
If a dataset is provided, use it. If no dataset is provided, automatically search the web for the latest AQI and water-quality data for the user's current city/location. If location is unavailable, ask for the city name first. Use the most recent available data, cite sources, clean the data, handle missing values, and validate quality before analysis.

ANALYSIS
Generate: cleanest city, most polluted city, highest AQI city, lowest AQI city, average AQI, number of cities analyzed, trends, anomalies, most surprising observation, executive summary.

INTERACTIVE DASHBOARD
Create a fully interactive Claude Artifact with:
📊 Key Metrics: average AQI, highest AQI city, lowest AQI city, number of cities analyzed, environmental health score.
📈 Visualizations: AQI comparison chart, PM2.5 comparison chart, PM10 comparison chart, city ranking chart, AQI distribution chart.
🎛 Interactive Filters: city selector, AQI range filter, pollutant selector, health-risk filter, date filter (if available), city comparison mode.
📋 City Detail Cards: AQI, PM2.5, PM10, air-quality category, health score, water-quality score.
🚦 AQI Categories: Good (Green), Satisfactory (Light Green), Moderate (Yellow), Poor (Orange), Very Poor (Red), Severe (Dark Red).

ENVIRONMENTAL HEALTH ANALYSIS
For the selected city explain AQI impact on lungs, sleep, energy levels, exercise performance, long-term health, and water-quality impact on hair fall, hair dryness, scalp health, skin dryness, acne, and sensitive skin.
Use risk indicators: 🟢 Low, 🟡 Moderate, 🔴 High.

PERSONAL REPORT CARD
Generate an Environmental Health Score (0–100) with breakdowns for Air Quality Score, Water Quality Score, and Overall Environmental Score.
Assign grades for Air Quality (A–F), Water Quality (A–F), Hair Risk, and Skin Risk.

INSIGHTS PANEL
Include: top 3 cleanest cities, top 3 most polluted cities, biggest anomaly, most surprising observation, recommended actions.

PERSONALIZED RECOMMENDATIONS
Provide: daily actions, indoor air improvements, outdoor activity guidance, hair-care recommendations, skin-care recommendations, water-quality improvement suggestions.

DESIGN
Modern, professional, mobile responsive, dark theme, smooth animations, premium UI, clean typography, dashboard-style layout, highly visual, colourful, LinkedIn-shareable.

OUTPUT
Generate a complete downloadable HTML application that is fully responsive and ready to save as index.html.

## Output
- Interactive dashboard with real-time AQI data for 5 cities: Ghaziabad, Delhi, Noida, Gurugram, Chandigarh
- Average AQI: 161.4
- Highest AQI: Delhi (210) — Very Poor
- Lowest AQI: Chandigarh (82) — Satisfactory
- Lung Risk for Ghaziabad: 🔴 High
- Sleep/Energy Impact: Elevated
- Hair/Skin Water Impact: Potential dryness risk

## Key Learning
- Claude can act as multiple expert personas simultaneously (Data Analyst + UX Designer + Health Researcher)
- Combining role-stacking with structured output rules produces production-grade dashboards
- Environmental data + health personalization = highly relevant, shareable AI output
- Prompt engineering with domain-specific output formats yields LinkedIn-worthy artifacts

## Screenshots
[Personal Environmental Health Analyzer Dashboard]

*Generated using Personal Environmental Health Analyzer Prompt*
*@Anthropic @ABTalksOnAI @AnilBajpai*