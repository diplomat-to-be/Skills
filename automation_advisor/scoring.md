# Automation Advisor — Scoring Rubric

## Dimension Scores

Each dimension is scored 0–25. Higher = stronger case for automation.

### Frequency (Q1)

| Answer                    | Score |
|--------------------------|-------|
| Multiple times per day   | 25    |
| Daily                    | 20    |
| Weekly                   | 12    |
| Monthly or less          | 5     |

### Time per Occurrence (Q2)

| Answer              | Score |
|---------------------|-------|
| Over 30 minutes     | 25    |
| 10–30 minutes       | 20    |
| 5–10 minutes        | 12    |
| Under 5 minutes     | 5     |

### Error Cost (Q3)

| Answer                              | Score |
|-------------------------------------|-------|
| Financial loss or client impact     | 25    |
| Significant rework (1+ hours)       | 18    |
| Minor inconvenience, quick fix      | 8     |
| No real consequences                | 3     |

### Longevity (Q5)

| Answer                                   | Score |
|------------------------------------------|-------|
| Years (core business process)            | 25    |
| 6–12 months (current project/quarter)    | 18    |
| 1–6 months (temporary initiative)        | 10    |
| Unclear or short-lived                   | 3     |

## Modifiers

Applied after summing the 4 dimension scores.

### Input Variability Modifier (Q4)

| Answer                                      | Modifier |
|---------------------------------------------|----------|
| Always the same structure and format        | +5       |
| Mostly the same with minor variations       | +2       |
| Moderate variation, but patterns exist      | 0        |
| Every time is completely different          | −10      |

### Automation Approach Modifier (Q7)

| Answer                                                        | Modifier |
|---------------------------------------------------------------|----------|
| Fully rule-based: clear if/then steps                         | +5       |
| Mostly rule-based with occasional edge cases                  | +2       |
| Requires interpretation of unstructured data                  | −3       |
| Heavily creative or relationship-dependent                    | −10      |

## Total Score Calculation

```
Total = Frequency + Time + Error Cost + Longevity
      + Input Variability Modifier
      + Automation Approach Modifier
```

Clamp to range [0, 100].

## Verdict Thresholds

| Total Score | Verdict            | Recommendation                          |
|-------------|--------------------|-----------------------------------------|
| 70–100      | Automate now       | Build it. ROI is clear.                 |
| 40–69       | Consider carefully | Prototype first. Measure for 2 weeks.   |
| 0–39        | Stay manual        | Not worth the investment right now.     |

## Break-Even Calculation

All values come from the user's own answers — no defaults.

```
Task performer rate = Q9 (who does the manual work now)
Developer rate      = Q10a (who will build the automation — may differ from Q9)
AI multiplier       = Q10b: 0.5 if AI-assisted (Claude Code etc.), 1.0 if manual
Raw build hours     = Q10c midpoint (e.g. "weekend project" → 12)
Minutes per round   = Q2 midpoint (e.g. "10–30 min" → 20)
Rounds per month    = Q1 mapped:
                        Multiple times/day → 60 (assume 3×/day × 20 workdays)
                        Daily              → 20
                        Weekly             → 4
                        Monthly or less    → 1

Effective build hours = raw build hours × AI multiplier
Build cost            = effective build hours × developer rate
Monthly manual cost   = (minutes per round / 60) × rounds per month × task performer rate
Efficiency            = 0.85 base
                        − 0.10 if Q4 = "Every time different"
                        − 0.05 if Q7 = "Requires interpretation"
Monthly savings       = monthly manual cost × efficiency
Break-even months     = build cost / monthly savings
```

Always show the full calculation with plugged-in numbers so the user
can verify and adjust assumptions.

## Approach Decision Tree

```
Score ≥ 70?
├── YES → Check Q7 (automation approach)
│   ├── Fully rule-based       → Deterministic script
│   ├── Mostly rule-based      → Hybrid (script + LLM for edges)
│   ├── Needs interpretation   → AI agent / LLM workflow
│   └── Creative/relationship  → LLM-assisted drafts + human review
├── 40–69 → Prototype
│   └── Build minimal version, measure actual time saved for 2 weeks
└── < 40 → Stay manual
    └── Set a calendar reminder to reassess in 3 months
```
