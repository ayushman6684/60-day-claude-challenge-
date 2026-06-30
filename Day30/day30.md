### 5 Supply Chain Decisions:
1. **Supplier Strategy** — Single / Dual / Multi-Supplier Network
2. **Factory Location** — Domestic / Nearshore / Offshore
3. **Warehouse Strategy** — Central / Regional Hubs / Micro-Fulfillment
4. **Transportation Mode** — Road / Rail / Ocean / Air Freight
5. **Inventory Strategy** — Lean JIT / Balanced Buffer / High Safety Stock

---

## 📊 Live Metrics (update after every decision)
| Metric | Description |
|---|---|
| 💰 Cost Efficiency | How lean your cost structure is |
| ⚡ Delivery Speed | How fast goods reach customers |
| 🛡️ Resilience | How well you survive disruptions |
| 😊 Customer Satisfaction | Overall service level |
| 🌱 Sustainability | Environmental footprint |

---

## 🏆 Final Dashboard Includes
- **Overall Score** (0–100) with letter grade (A+ to F)
- **Chain Visualization** — icons for each node
- **Strengths & Weaknesses** analysis
- **Biggest Risk** identification
- **Top 3 Practical Improvements*

## 🧠 Key Learnings

### Supply Chain Concepts
- **Single-source risk** — Toyota's 1997 brake supplier fire stopped 70% of output for 2 weeks
- **JIT vs Safety Stock** — 2021 chip shortage proved pure JIT is fragile at scale
- **Nearshoring trend** — Mexico became #1 US trade partner in 2023
- **Modal shift** — Rail is 75% cheaper than trucking per ton-mile with 3× lower emissions
- **Micro-fulfillment** — Only profitable at high urban order density

### React / Frontend Concepts
- `useState` for multi-step wizard flow with phase management
- Effect delta tracking — storing `prevMetrics` to show +/- changes per decision
- Reusable components: `MetricsRow`, `StepCard`, `ChainViz`, `ScoreRing`
- SVG `stroke-dashoffset` technique for animated circular score ring
- CSS `conic-gradient` and custom property `--pct` for dynamic ring fill
- Babel Standalone in browser — **no `export default`**, no ES module syntax
- CSS `@import` inside `<style>` can silently fail — use system fonts for offline apps

### Common Pitfalls Fixed
| Bug | Root Cause | Fix |
|---|---|---|
| Blank page | `export default function App()` | Browser Babel doesn't support ES modules |
| Fonts not loading | `@import` in `<style>` | Switched to `system-ui` font stack |
| File blocked | Downloaded from internet | Right-click → Properties → Unblock |

---

## 🔗 Resources
- [React CDN Setup](https://react.dev/learn/add-react-to-an-existing-project)
- [Babel Standalone Docs](https://babeljs.io/docs/babel-standalone)
- [Supply Chain 101 — Investopedia](https://www.investopedia.com/terms/s/supplychain.asp)

---

*Built as part of my 30-day frontend challenge — Day 30/30* 🎉
////////////////////////////////////////////////////////////////

You are an expert frontend developer, UX designer, game designer, and supply chain consultant.

Build a complete single-file HTML app named 'Supply Chain Builder'.

Design it so a complete beginner can understand supply chains. Before every decision, explain what the concept means, why it matters, and how it affects a business.

Requirements:

* Output ONLY one HTML file.
* React via CDN + Babel JSX.
* Plain HTML, CSS, and JavaScript only.
* No Tailwind, npm, backend, APIs, images, or external assets.
* Runs offline by opening the HTML file.
* No placeholders or incomplete features.

Flow:

1. Welcome screen introducing supply chains in simple language.
2. Generate a random company (industry, products, countries served, demand level).
3. Guide the player through building their supply chain by choosing:
   * Number of suppliers (single or multiple)
   * Factory location
   * Warehouse strategy
   * Transportation method (road, rail, sea, air)
   * Inventory strategy (low, balanced, high)
4. After every choice, explain the trade-offs in plain English.
5. Display live business metrics that update after each decision:
   * Cost
   * Delivery Speed
   * Risk
   * Customer Satisfaction
   * Sustainability
6. At the end, generate a dashboard with an Overall Supply Chain Score (0-100), strengths, weaknesses, biggest risk, and three practical improvements.

Design:

* Premium enterprise dashboard.
* Dark theme.
* Responsive.
* Smooth transitions.
* Rounded cards.
* Hover effects.
* Animated progress bars.
* Replay button.

Randomize company details each playthrough. Organize the app into reusable React components using useState. Ensure every button works and return ONLY the complete HTML inside one code block.