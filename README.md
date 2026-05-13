# Agile Delivery Health Analytics | Power BI

Power BI Agile Delivery Intelligence dashboard designed to monitor sprint predictability, velocity stability, delivery health and team performance across a simulated multi-team Agile environment.

---

## Project Summary

This project simulates an Agile delivery environment with 15 sprints and 3 teams, transforming sprint-level delivery data into an executive-ready Power BI dashboard.

The dashboard focuses on:

- Sprint predictability
- Velocity stability
- Delivery gap
- Sprint health status
- Team delivery maturity
- Agile performance trends

The goal is to move beyond basic Agile reporting and provide a structured view of delivery risk, planning discipline and operational maturity.

---

## Business Problem

Agile teams often track velocity, completed work and sprint status, but these metrics alone do not explain whether delivery is stable, predictable or at risk.

This dashboard addresses that gap by combining delivery performance, predictability and health scoring into a structured reporting model for PMO, Scrum Masters, Delivery Managers and executive stakeholders.

---

## Dataset

The dataset is fictional and was created to simulate a realistic Agile delivery scenario.

It includes:

- 15 sprints
- 3 Agile teams (A, B and C)
- Sprint-level delivery metrics
- Daily burndown records
- Story points committed and completed
- Task completion data
- Sprint status classification

### Team narrative

| Team | Delivery pattern |
|---|---|
| Team A | Strong benchmark team, stable but not perfect |
| Team B | Initially unstable, then progressively recovers |
| Team C | Gradual transformation journey toward more stable delivery |

The dataset includes repeated sprint records by burndown day. Because of this, DAX measures were designed to avoid inflated KPIs caused by daily sprint granularity.

---

## Dashboard Pages

### 1. Agile Delivery Health

Monitors sprint health using a scoring model based on sprint predictability and pending work ratio.

Key visuals:

- Healthy Sprint %
- Critical Sprint Count
- Average Health Score
- Health Score by Team
- Health Score Evolution
- Sprint Health Matrix

![Agile Delivery Health](images/01_agile_delivery_health.png)

---

### 2. Predictability vs Stability

Compares teams based on delivery maturity, sprint predictability and velocity stability.

Key visuals:

- Sprint Predictability
- Velocity Stability Index
- Team Delivery Maturity Map
- Predictability Detail by Sprint and Team

![Predictability vs Stability](images/02_predictability_vs_stability.png)

---

### 3. Sprint Delivery Performance

Tracks delivery evolution across sprints.

Key visuals:

- Completed Story Points
- Committed Story Points
- Average Velocity
- Delivery Gap %
- Velocity and Predictability Trend
- Committed vs Completed Story Points

![Sprint Delivery Performance](images/03_sprint_delivery_performance.png)

---

## Key Metrics

| Metric | Purpose |
|---|---|
| Sprint Predictability | Measures completed story points versus committed story points |
| Delivery Gap % | Quantifies the gap between committed and completed work |
| Avg Velocity | Tracks average delivery capacity |
| Velocity Stability Index | Measures consistency of velocity over time |
| Healthy Sprint % | Shows the proportion of healthy sprints |
| Critical Sprint Count | Identifies high-risk sprint periods |
| Avg Health Score | Summarizes Agile delivery health |

---

## Final Dashboard Results

| KPI | Result |
|---|---:|
| Sprint Predictability | 88% |
| Velocity Stability Index | 85% |
| Completed Story Points | 534 |
| Committed Story Points | 606 |
| Avg Velocity | 23.3 |
| Delivery Gap | 11.9% |
| Healthy Sprint % | 33% |
| Critical Sprint Count | 4 |
| Avg Health Score | 2.2 |

---

## Key Insights

- Team A operates as the delivery benchmark, showing the highest predictability and velocity stability.
- Team B starts with low delivery maturity but shows progressive recovery across the sprint timeline.
- Team C follows a gradual transformation pattern, improving over time but with lower consistency than Team A.
- Overall sprint predictability reaches 88%, with an 11.9% delivery gap.
- Velocity and predictability improve progressively, suggesting better planning discipline and delivery maturity.
- The health scoring model is intentionally strict, combining predictability and pending work ratio to highlight delivery risk.

---

## Technical Approach

The Power BI model uses a sprint-level dataset combined with daily burndown records.

Since sprint metrics are repeated across burndown days, direct column aggregation would inflate KPIs. To solve this, DAX measures aggregate values at the unique SprintID + TeamName level.

Example:

```DAX
Committed Story Points =
SUMX(
    SUMMARIZE(
        'Agile_sprint',
        'Agile_sprint'[SprintID],
        'Agile_sprint'[TeamName],
        "CommittedSP", MAX('Agile_sprint'[StoryPoints])
    ),
    [CommittedSP]
)

Created by Bruno Fierro – Senior PMO & Project Manager | More projects on my GitHub | Project management & PMO insights on my website.
