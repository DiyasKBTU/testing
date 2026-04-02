# AgroFusion Score 🌾

> Explainable decision-support system for merit-based agricultural subsidy allocation in Kazakhstan.  
> Built for **Decentrathon 5.0 — AI for Government, Case 2**.

---

## Overview

AgroFusion Score is an **AI/data-driven prototype** for ranking agricultural subsidy applications based on merit rather than submission order.

The system helps a ministry or committee:

- **rank** applicants using transparent scoring logic,
- **explain** why each application received its result,
- **flag risks** that require manual review,
- **form a shortlist** for commission review,
- **analyze newly uploaded applications** without rebuilding the whole system from scratch.

This is a **decision-support tool**, not an automatic approval engine.  
The final decision remains with a human commission.

---

## Problem

Today, agricultural subsidies are often distributed by a **first-come-first-served** logic: whoever submits a complete application earlier has a better chance of receiving funding before the budget runs out.

This creates several problems:

- effective farms may lose funding to faster applicants,
- prior subsidy usage quality is not sufficiently considered,
- risk factors are hard to compare consistently,
- commissions spend too much time on manual triage.

The hackathon task requires a system that uses **AI/ML and data analysis** to rank applicants, explain results, and support human review.

---

## Solution

AgroFusion Score implements a **hybrid scoring pipeline**:

1. **Rule-based explainable score**  
   Calculates the core score from transparent business logic:
   - historical performance proxy,
   - compliance / discipline signals,
   - geo / eco-risk proxy.

2. **ML-based differentiation layer**  
   Adds a data-driven ranking signal to separate similar applications more finely.

3. **Final recommendation engine**  
   Produces one of several recommendations:
   - approve as priority,
   - approve with caution,
   - manual review,
   - defer due to high risk,
   - reject if baseline eligibility fails.

4. **Interactive review interface**  
   Lets the user:
   - filter ranked applications,
   - inspect shortlist,
   - open a detailed card for each application,
   - upload new data for additional scoring.

---

## Why this is useful for government

AgroFusion Score is designed for **human decision support** in subsidy allocation.

It helps a commission:

- move from queue-based distribution to **merit-based prioritization**,
- make decisions faster using a ranked shortlist,
- understand the drivers behind each result,
- keep the final authority with human experts.

This matches the hackathon requirement that AI must **assist**, not replace, the expert.

---

## Core Scoring Logic

Each application first receives a **rule-based score (0–100)** from three components.

### 1. Historical Score
Measures an applicant’s past effectiveness proxy.

Signals used in MVP:
- historical subsidy amount,
- historical livestock delta proxy,
- norm-to-request relationship,
- previous application patterns.

### 2. Compliance Score
Measures execution discipline and operational risk.

Signals used:
- violations count,
- mortality-related risk flag,
- compliance penalties with score caps.

### 3. Eco Score
Measures ecological / feed sufficiency risk.

Signals used:
- feed availability proxy by region,
- livestock density / headcount proxy by district,
- eco risk zone:
  - green,
  - yellow,
  - red.

---

## Farm Route Logic

Applications are classified into one of three routes depending on subsidy direction:

- **Extensive** — meat / pasture / breeding-oriented livestock logic
- **Intensive** — poultry / swine / high-intensity production logic
- **Hybrid** — mixed / dairy / AI-service related logic

Each route has different score weights for:
- historical factors,
- compliance,
- eco risk.

---

## Hybrid Final Score

After the explainable rule-based score is computed, the system applies an additional **ML ranking layer**.

### Final combined score

```text
Final Combined Score = 60% Rule-Based Score + 40% ML Score
