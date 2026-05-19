# Agile Delivery Intelligence Analytics | Power BI

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

<img width="1333" height="792" alt="image" src="https://github.com/user-attachments/assets/8dd5ea2b-500d-4c2f-a127-adef52cd9861" />

## Sprint Health Scoring Logic

The Sprint Health Score is the core business rule of the dashboard.

It combines two dimensions:

1. **Sprint Predictability** — how much committed work was actually completed.
2. **Pending Task Rate** — how much work remained unfinished at the end of the sprint.

The model is intentionally strict because a sprint should not be considered healthy only because it delivered many story points. A sprint can have high predictability but still carry operational risk if too much work remains pending.

```DAX
Sprint Health Score =
VAR Predictability =
    [Sprint Predictability %]

VAR PendingRate =
    [Pending Task Rate]

RETURN
SWITCH(
    TRUE(),

    Predictability >= 0.88 &&
    PendingRate <= 0.20,
    3,

    Predictability >= 0.75 &&
    PendingRate <= 0.32,
    2,

    1
)
```

## Score interpretation
| Score | Status   | Interpretation                                                               |
| ----- | -------- | ---------------------------------------------------------------------------- |
| 3     | Healthy  | Strong delivery performance, high predictability and controlled pending work |
| 2     | Warning  | Acceptable delivery performance, but with planning or execution risk         |
| 1     | Critical | Low predictability and/or excessive pending work requiring attention         |

## Threshold rationale
| Threshold                                   | Reasoning                                                                             |
| ------------------------------------------- | ------------------------------------------------------------------------------------- |
| Predictability ≥ 88% and Pending Rate ≤ 20% | Indicates a healthy sprint with strong delivery alignment and limited unfinished work |
| Predictability ≥ 75% and Pending Rate ≤ 32% | Indicates partial delivery control, but with visible risk                             |
| Below those thresholds                      | Indicates delivery instability or planning/execution issues                           |

This scoring model supports a more realistic Agile health view than velocity alone. It prevents the dashboard from treating a high-output sprint as healthy when unfinished work remains too high.

---

### 2. Predictability vs Stability

Compares teams based on delivery maturity, sprint predictability and velocity stability.

Key visuals:

- Sprint Predictability
- Velocity Stability Index
- Team Delivery Maturity Map
- Predictability Detail by Sprint and Team

<img width="1407" height="790" alt="image" src="https://github.com/user-attachments/assets/b3e0d453-988c-444e-952e-9e77311fa013" />


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

<img width="1407" height="794" alt="image" src="https://github.com/user-attachments/assets/7aff4f23-b8c1-425d-876a-76505423c92f" />


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
  
**- The health scoring model is intentionally strict, combining predictability and pending work ratio to highlight delivery risk.**

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
```
This ensures that sprint-level metrics are calculated correctly despite the daily burndown granularity.

## Tools Used
- Power BI
- Power Query
- DAX
- Data modeling
- Agile delivery analytics
- PMO reporting logic

## Limitations

This version focuses on sprint-level delivery analytics.

Ticket-level flow metrics such as Cycle Time, Lead Time and WIP were intentionally excluded because they require issue-level transactional data with created, started and completed timestamps.

## Impact

This dashboard demonstrates how Agile delivery data can be transformed into an executive-ready monitoring system focused on predictability, stability, delivery risk and team maturity.

It supports better conversations around:

- Sprint planning discipline
- Delivery governance
- Team maturity
- Operational risk
- PMO reporting
_______________________________________________________________________________________________
I welcome suggestions, improvements, and collaborations. Feel free to open issues or send PRs.
Let’s turn data into decisions together.
_______________________________________________________________________________________________
Created by Bruno Fierro – Senior PMO & Project Manager | More projects on my GitHub | Project management & PMO insights on my website.
