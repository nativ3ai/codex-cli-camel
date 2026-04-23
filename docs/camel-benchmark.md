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

## Latest result snapshot

From `benchmarks/camel_guard/latest.json`:

| Metric | Value |
| --- | ---: |
| samples | 8 |
| threshold | 6 |
| accuracy | 1.0 |
| benign false-positive rate | 0.0 |
| malicious detection rate | 1.0 |
| throughput (samples/sec) | 456074.47 |

Use this benchmark for regression tracking when modifying guard rules or thresholds.
