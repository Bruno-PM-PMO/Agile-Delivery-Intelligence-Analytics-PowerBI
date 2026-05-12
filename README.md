# Agile-Delivery-Health-Analytics-PowerBI
Power BI Agile Delivery Intelligence dashboard simulating a multi-team environment to monitor sprint predictability, velocity stability, health status and delivery performance.

## Project Summary

Power BI dashboard designed to monitor Agile delivery health across a simulated multi-team environment.

The project focuses on sprint predictability, velocity stability, delivery gap, and sprint health status, transforming Agile delivery data into actionable insights for PMO, Scrum Masters, Delivery Managers, and executive stakeholders.

## Business Problem

Agile teams often track velocity and completed work, but these metrics alone do not explain whether delivery is predictable, stable, or at risk.

This dashboard addresses that gap by combining delivery performance, predictability, and health scoring into a structured Power BI report.

## Dataset

The dataset is fictional and simulates 15 sprints across 3 Agile teams:

- Team A: mature and stable delivery team.
- Team B: initially unstable, with progressive recovery.
- Team C: gradual transformation and improvement over time.

The dataset includes sprint-level metrics and daily burndown records, while Power BI measures were designed to avoid duplicated values caused by daily sprint granularity.

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

### 2. Predictability vs Stability

Compares teams based on delivery maturity, predictability, and velocity stability.

Key visuals:
- Sprint Predictability
- Velocity Stability Index
- Team Delivery Maturity Map
- Predictability Detail by Sprint and Team

### 3. Sprint Delivery Performance

Tracks delivery evolution across sprints.

Key visuals:
- Completed Story Points
- Committed Story Points
- Average Velocity
- Delivery Gap %
- Velocity and Predictability Trend
- Committed vs Completed Story Points

## Key Metrics

| Metric | Purpose |
|---|---|
| Sprint Predictability | Measures completed story points versus committed story points |
| Delivery Gap % | Quantifies the remaining delivery gap |
| Avg Velocity | Tracks average delivery capacity |
| Velocity Stability Index | Measures consistency of velocity over time |
| Healthy Sprint % | Shows the proportion of healthy sprints |
| Critical Sprint Count | Identifies high-risk sprint periods |
| Avg Health Score | Summarizes Agile delivery health |

## Key Insights

- Team A operates as the delivery benchmark, with high predictability and strong velocity stability.
- Team B starts with low predictability but shows progressive recovery over the sprint timeline.
- Team C improves gradually, reflecting a transformation journey toward more stable delivery.
- Overall predictability reaches 93%, with a delivery gap of 6.9%.
- Velocity and predictability improve together, suggesting better planning discipline and delivery maturity.

## Tools & Approach

- Power BI
- Power Query
- DAX
- Data modeling
- Agile delivery metrics
- PMO reporting logic
