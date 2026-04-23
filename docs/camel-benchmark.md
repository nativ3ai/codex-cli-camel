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

- sample count
- threshold
- classification accuracy (`allow` vs `block`)
- benign false-positive rate
- malicious detection rate
- throughput (samples/sec)
- monitor/enforce mode comparison table

## Latest result snapshot

From `benchmarks/camel_guard/latest.json`:

- samples: `8`
- accuracy: `1.0`
- benign false-positive rate: `0.0`
- malicious detection rate: `1.0`

Use this benchmark for regression tracking when modifying guard rules or thresholds.
