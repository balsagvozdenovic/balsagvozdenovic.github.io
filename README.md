# balsagvozdenovic.github.io
ASMAF: Advanced SOC Maturity Assessment Framework
ASMAF is my custom Security Operations Center (SOC) maturity grading system, built to evaluate how prepared an organization really is across critical operational domains. This README explains how I created it, the sources I used, and why certain design choices were made.

1. Building the Question Set

I started by analysing multiple SOC maturity frameworks (SOC-CMM, ISO/IEC 27001 audits, and vendor whitepapers).
From these, I extracted overlapping themes and distilled them into 32 initial questions covering governance, risk, telemetry, detection, hunting, investigation, incident response, automation, workforce, and architecture.
During testing, I identified two redundant or ambiguous questions that didn’t add meaningful differentiation (one overlapped with case management workflows, the other duplicated risk-based prioritization already covered elsewhere). I removed them to improve clarity and scoring consistency, leaving 30 final questions.
Each question is weighted according to its impact (e.g., logging coverage has higher weight than informal collaboration). Evidence requirements were added under each question to encourage objective scoring.

2. Scoring Logic

Each response is graded 0-4, matching ASMAF’s maturity levels:

0 = Not performed/ad hoc

1 = Initial / compliance-driven

2 = Documented / resourced

3 = Policy-guided / measurable

4 = Optimized / proactive

Weighted answers roll up into domain scores. These are averaged and normalized to produce an overall SOC maturity percentage.

3. Benchmarks Integration
I didn’t want a static scoring table—so I added industry benchmarks for context.
Benchmarks are included for Finance, Healthcare, and Tech sectors, normalized to a 0–100 scale for direct comparison on a radar chart.

To build these, I synthesized:

  SOC-CMM community survey data and public results.
  
  Breach cost and dwell-time statistics from IBM/Ponemon.
  
  Studies by Wavestone, CYE, Cisco, SANS, and vendor SOAR adoption surveys.
  
  My own mapping of adoption rates, dwell times, and maturity levels to ASMAF’s 10 domains.

This approach keeps the benchmarks evidence-backed while aligning them to the ASMAF format your HTML visualizations require.

4. Data & Front-End

The Excel workbook (SOC_Maturity_Grading_Framework.xlsx) stores the structured question set, weights, and scoring model.
An HTML/JavaScript front-end loads this data via JSON (soc_questions.json) to display an interactive radar chart.
I replaced the placeholder benchmark percentages in soc_questions.json with the researched values, ensuring consistency with the final 30-question set.
The HTML code uses fetch() to read the JSON and drawBenchmarkChart() to render Finance, Healthcare, and Tech curves alongside the user’s own assessment.

5. Why Two Questions Were Removed

The removed items were:

  “Do you maintain an updated runbook repository?”, as ito verlapped heavily with the collaboration & knowledge question.
  
  “Is enterprise risk formally tied to SOC use-case design?”, as it already addressed by a more specific risk prioritization item.

By cutting these, I avoided double-weighting the same behaviors and streamlined the assessment to reduce fatigue without losing coverage.

6. Key Takeaways for Users

Transparent: Every question cites its evidence sources (program charters, KPI dashboards, hunt calendars, etc.).

Weighted & Normalized: Scores are scaled to produce an accurate maturity percentage.

Benchmark-Aware: Users can visually compare their SOC maturity to real-world industry baselines.

Adaptable: The benchmark section can be extended for new sectors by adding keys in the JSON.

Clear Output: The radar chart and percentage output provide an immediate picture of strengths, gaps, and priorities.

7. How to Update Benchmarks

To update benchmarks in the future, edit soc_questions.json under "benchmarks" with new percentages for each domain and sector. The radar chart will update automatically on reload.
