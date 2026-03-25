# rz-data-analysis

Statistical analysis, A/B testing, and causal attribution — shared methodology.

## Scope

The analytical engine powering both rz-product-optimization and rz-growth-ops. Provides a rigorous six-step pipeline for any data analysis task, plus a dedicated A/B testing framework.

## Reference

This skill extends **FL Playbook: data-analysis**. The canonical methods live in:

```
../fl-playbook/data-analysis/
```

## Six-Step Pipeline

```
DATA SOURCE → USER GROUP → METRIC → INSIGHTS → CONCLUSION → VISUAL DELIVERY
```

| Step | Purpose | FL Playbook Reference |
|---|---|---|
| DataSource | Input, filters, field definitions | `methods/fundamentals.md` |
| UserGroup | Breakdown rules and cohort definitions | `methods/fundamentals.md` |
| Metric | KPI calculations with precision | `methods/fundamentals.md` |
| Insights | Cross-tabulate groups x metrics | `methods/fundamentals.md` |
| Conclusion | Compare findings to hypothesis | `methods/fundamentals.md` |
| VisualDelivery | Format for audience | `methods/fundamentals.md` |

## A/B Testing Framework

Defined in `fl-playbook/data-analysis/methods/ab-testing.md`:

- **Three constraints**: MDE, sample size, confidence level (know 2, derive 1)
- **Pre-experiment**: AA testing, SRM checks, baseline confirmation
- **Validity threats**: selection bias, Simpson's Paradox, novelty effect, Hawthorne effect
- **Stopping rules**: based on sample adequacy, not p-value peeking

## RZ Layer

Personal extensions:

- **Personal finance analysis** — apply the six-step pipeline to investment portfolio review (feeds rz-finance)
- **Health data analysis** — structured analysis of fitness, sleep, and nutrition data (feeds rz-health)
- **Self-experiments** — rigorous personal N=1 experiments with proper baselines and controls
