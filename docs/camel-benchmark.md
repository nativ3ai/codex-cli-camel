# CaMeL Guard Benchmark

## Harness

- Script: `benchmarks/camel_guard/benchmark.py`
- Dataset: `benchmarks/camel_guard/samples.json`
- Output: `benchmarks/camel_guard/latest.json`

## Run

```bash
python3 benchmarks/camel_guard/benchmark.py
```

## Reported metrics

| Metric | Meaning | Why it matters |
| --- | --- | --- |
| sample count | number of evaluated benchmark prompts | confirms dataset size and comparability |
| threshold | score boundary for `allow` vs `block` | defines policy strictness |
| accuracy | exact match rate vs expected label | overall classification quality |
| benign false-positive rate | benign prompts incorrectly blocked | utility cost / user friction |
| malicious detection rate | malicious prompts correctly blocked | security effectiveness |
| throughput (samples/sec) | scan speed in harness | runtime overhead estimate |

## Methodology-to-benchmark mapping

| CaMeL methodology objective | Benchmark evidence in this repo |
| --- | --- |
| Resist instruction override in untrusted inputs | malicious detection rate on attack set |
| Preserve utility on benign workflows | benign false-positive rate and benign sample outcomes |
| Keep defense operationally deployable | throughput metric and deterministic scoring |
| Support progressive rollout | monitor/enforce behavior comparison in report |

Role model reference:
- [CaMeL role mapping](./camel-role-mapping.md)

## Latest result snapshot

From `benchmarks/camel_guard/latest.json`:

| Metric | Value |
| --- | ---: |
| samples | 8 |
| threshold | 6 |
| accuracy | 1.0 |
| benign false-positive rate | 0.0 |
| malicious detection rate | 1.0 |
| throughput (samples/sec) | 536334.58 |

## Token-cost delta (battle-tested reference)

Reference source:
- NousResearch Hermes PR #3987: https://github.com/NousResearch/hermes-agent/pull/3987

| Metric | Value |
| --- | ---: |
| legacy total tokens | 4447 |
| monitor total tokens | 5548 |
| enforce total tokens | 6085 |
| monitor vs legacy | +24.76% |
| enforce vs legacy | +36.83% |
| enforce vs monitor | +9.68% |

Interpretation:
- `monitor` overhead is lower than `enforce`, consistent with observe-first rollout.
- these values are not synthetic estimates; they are imported from the live benchmark evidence in the referenced Hermes PR.

Use this benchmark for regression tracking when modifying guard rules or thresholds.
