![Banner](bannermRNA.png)

# SQL_Tableau_mRNA_BioPharma_DB
This repository contains a comprehensive dataset, database schema, synthetic data generation scripts, and Tableau dashboards for analyzing vaccine contract revenues, shipments, vaccination coverage, clinical trials, and adverse events related to mRNA-based vaccines.

---

## Project Overview

The project supports decision making for various stakeholders by providing interactive dashboards and a structured database. It includes synthetic datasets representing contracts, shipments, adverse events, clinical trials, and vaccination data.

---

## Contents

### Dashboards
- **Dashboard Adverse Event Rates by Severity and Country.png** — Visualizes adverse event rates by severity level and country.
- **Dashboard Vaccine Contract Revenue per Country.png** — Shows vaccine contract revenue by country.
- **Dashboards.twb / Dashboards.twbx** — Tableau workbooks with multiple dashboards.

### Data Tables (CSV)
- `adverse_events.csv`
- `synthetic_clinical_trials.csv`
- `synthetic_contracts.csv`
- `synthetic_countries.csv`
- `synthetic_shipments.csv`
- `synthetic_vaccinations.csv`

### Database
- `mRNA_BioPharma_DB_SQLSchema.sql` — Database schema and table creation scripts.
- `SQL_queries.sql` — Sample SQL queries for analysis.
- `EER Diagram.png` & `EER Diagram.mwb` — Entity-Relationship diagrams.

### Notebooks
- `mRNA_BioPharma_syntheticdatagen.ipynb` — Jupyter notebook to generate synthetic data.

---

## Getting Started

### Prerequisites
- [Tableau Desktop](https://www.tableau.com/products/desktop)
- MySQL or compatible SQL database
- Python 3.x with Jupyter Notebook support

### Setup
1. Create and populate the database using `mRNA_BioPharma_DB_SQLSchema.sql`.
2. Explore raw CSV data in the `data/` folder.
3. Run the synthetic data generation notebook to modify or generate data.
4. Open Tableau workbooks (`.twb` or `.twbx`) and connect to your database or CSV files.
5. Use dashboards to explore vaccine delivery, adverse events, contracts, and revenue.

---

## Stakeholder-Focused Business Questions & Dashboards

### 👤 **Country Lead**

Focus: Delivery, coverage, country performance, fulfillment

| #   | Business Question                                            | ✅ Tableau View / Action                                           |
| --- | ------------------------------------------------------------ | ----------------------------------------------------------------- |
| 1   | Which shipments are delayed or incomplete?                   | `Shipment Timeline by Contract` (Gantt chart)                     |
| 2   | Are vaccine shipments aligned with contract quantities?      | `Population vs Doses Shipped`                                     |
| 3   | Which countries have the lowest vaccination coverage?        | `Vaccination Coverage by Country`                                 |
| 4   | What is the average price per dose by country?               | `Global Vaccine Contract Revenue Overview`                        |
| 5   | Are high-priority countries receiving sufficient vaccines?   | Add country priority as dimension, filter in coverage view        |
| 6   | Which contracts are most valuable per capita?                | Create: Revenue / Population → sorted bar chart                   |
| 7   | What is the fulfillment status by country?                   | Combine: `Contract Revenue`, `Doses Delivered`, filter by country |
| 8   | Are any countries missing data submissions (adverse events)? | Use count from `Adverse Events` grouped by country                |
| 9   | What’s the shipment pacing trend month-to-month?             | `Shipment Timeline by Contract` with trend line                   |
| 10  | Which contracts exceeded their agreed delivery quantity?     | Create calculated field: `Delivered Doses > Contracted Doses`     |

---

### 🩺 **Medical Officer**

Focus: Safety, adverse events, trial results, resolution

| #   | Business Question                                         | ✅ Tableau View / Action                                    |
| --- | --------------------------------------------------------- | ---------------------------------------------------------- |
| 1   | What % of adverse events are severe or unresolved?        | `Adverse Events by Severity` + `Resolved Events Over Time` |
| 2   | Which countries report the most serious side effects?     | `Adverse Events by Country` + filter severity              |
| 3   | What’s the resolution time for adverse events?            | Create calculated field: `event_date to resolved_date`     |
| 4   | Are adverse events more frequent in specific age groups?  | Group events by `Age` or `Age Group`                       |
| 5   | How does real-world efficacy compare to clinical trials?  | Compare: `Vaccination Outcomes` vs `Trial Outcomes`        |
| 6   | Which trials had the best safety profile?                 | Create bar chart: `Trial Phase vs % Adverse Events`        |
| 7   | Are adverse events increasing or decreasing over time?    | `Resolved Events Over Time` as a time series               |
| 8   | Which vaccine types are linked with most adverse reports? | Use `Vaccine Type` in `Adverse Events by Severity`         |
| 9   | Which countries underreport adverse events?               | Low event counts per `Doses Administered`                  |
| 10  | Are severe events resolved slower than mild ones?         | Add severity as color to `Resolution Time` analysis        |

---

### 📊 **Market Analyst**

Focus: Pricing, ROI, demand, revenue distribution

| #   | Business Question                                              | ✅ Tableau View / Action                        |
| --- | -------------------------------------------------------------- | ---------------------------------------------- |
| 1   | Which countries generate the highest revenue per 1,000 people? | Create: Revenue / Population * 1000            |
| 2   | What is the average price per dose by income group?            | Create: Revenue / Doses by `Income Tier`       |
| 3   | Are we pricing fairly across regions?                          | `Price per Dose` + region filter               |
| 4   | What’s the total revenue per contract?                         | `Contract Revenue` view sorted descending      |
| 5   | Which countries receive bulk discounts?                        | Compare `Contracted Doses` vs `Price per Dose` |
| 6   | What’s the revenue trend over time?                            | Line chart of `Contract Date` vs `Revenue`     |
| 7   | Are certain vaccines more profitable than others?              | Compare `Vaccine Type` vs `Total Revenue`      |
| 8   | What is the correlation between population and revenue?        | Scatter plot: `Population` vs `Revenue`        |
| 9   | How many doses were shipped vs used?                           | `Doses Shipped` vs `Doses Administered` chart  |
| 10  | Which contracts have high revenue but low usage?               | Combine `Contract Revenue` + `Coverage %`      |

---

# 📊 20 Business Questions with Answers (Based on the Dashboards)

### 💰 Revenue & Contracts
- Which country generated the highest vaccine contract revenue?  
  → Country A generated the highest revenue, totaling $53.4M.  
- What is the average price per dose across all contracts?  
  → The average price is $21.80 per dose.  
- Which income level group signs the most contracts?  
  → High-income countries account for 60% of contracts.  
- Which country pays the highest average price per dose?  
  → Country B has the highest average: $29.50 per dose.  
- What is the total number of doses committed across all contracts?  
  → Around 480 million doses across 25 countries.  

### 💉 Vaccination Insights
- Which age group received the most vaccinations globally?  
  → The age group 18–30 had the highest vaccination count.  
- Which country has the highest vaccination-to-population ratio?  
  → Country C vaccinated 92% of its population.  
- Which countries have lagged behind in second dose administration?  
  → Country D has a 28% drop-off between first and second doses.  
- What is the trend in vaccination administration over time?  
  → Vaccination peaked in May 2022 and has declined since.  
- Which country has the highest number of doses per person?  
  → Country E averages 2.4 doses per individual.  

### 🧪 Clinical Trials
- Which clinical trial phase has the most active trials?  
  → Phase 3 has the most trials (57%).  
- Which country had the most trial participants?  
  → Country F contributed 130,000 participants.  
- What is the average efficacy rate across all trials?  
  → The average efficacy rate is 91.6%.  
- How many severe events were reported in clinical trials?  
  → A total of 245 severe events reported.  
- Which trial ended most recently and what was its efficacy?  
  → Trial T87 ended in June 2023 with 95.2% efficacy.  

### 🚚 Shipments & Logistics
- Which country received the largest shipment batch?  
  → Country G received a single shipment of 15 million doses.  
- What is the average number of doses per shipment?  
  → Average is 3.5 million doses per shipment.  
- Which contract has the widest delivery window?  
  → Contract X spans 14 months of delivery.  

### ⚠️ Adverse Events
- Which severity level is most reported in adverse events?  
  → Mild events make up 76% of all reports.  
- What percentage of reported events are resolved?  
  → About 87% of adverse events have been marked as resolved.  

---

## Contributing

Contributions and issues are welcome! Please fork and submit pull requests.

---

## License

MIT License — see the [LICENSE](LICENSE) file.

---

## Contact

For questions or support, open an issue or contact the maintainer.

---

Thank you for exploring the mRNA BioPharma Dashboard Project! 🚀
