# CaMeL Guard Benchmark

## Harness

- Script: `benchmarks/camel_guard/benchmark.py`
- Dataset: `benchmarks/camel_guard/samples.json`
- Output: `benchmarks/camel_guard/latest.json`

## Run

```bash
python3 benchmarks/camel_guard/benchmark.py
```

## Metrics captured

- sample count
- threshold
- classification accuracy (`allow`/`block`)
- blocked sample count
- throughput (samples/sec)

## Notes

This benchmark is deterministic and intended for regression tracking in CI/PR review. It does not replace live-model security evaluation.
