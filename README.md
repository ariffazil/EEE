---
title: EEE — Kernel Spine Recovery
dataset_info:
  features:
    - name: id
      dtype: string
    - name: timestamp
      dtype: string
    - name: verdict
      dtype: string
  splits:
    - name: train
      num_bytes: 0
      num_examples: 0
  download_size: 0
  dataset_size: 0
  size_in_bytes: 0
license: apache-2.0
language:
  - en
tags:
  - ai-governance
  - constitutional-ai
  - audit
  - arifos
  - kernel-spine
  - mcp
pretty_name: EEE — Kernel Spine Recovery
---

# EEE — Kernel Spine Recovery

**Dataset:** `ariffazil/EEE`  
**Title:** Kernel Spine Recovery  
**Version:** 1.0.0  
**Date:** 2026-06-15

---

## What this is

EEE is the first **executable proof harness** for the arifOS constitutional kernel. It treats the kernel not as a specification but as a device under test: it calls the live MCP runtime and federation organs, checks that inner degradation dominates outer claims of health, and produces signed receipts.

The thesis behind the dataset:

> Intelligence = model × law × kernel × receipts.
>
> A kernel that cannot report its own degradation is not a kernel — it is a chatbot with delusions of governance.

EEE probes five gates that must hold for any trustworthy AI governance spine:

1. **Parse gate (L02A)** — Can the substrate output be structurally parsed?
2. **Truth gate (L02B / F2)** — If parsed, is it semantically truthful?
3. **Risk gate (F1, F8, F11)** — Does the kernel block irreversible, rushed, or unsafe actions?
4. **Sovereignty gate (F13)** — Is human veto absolute and unbypassable?
5. **Register gate (DDD)** — Does the system honestly record its own state, including failures?

The dominant finding that motivated EEE was the **CCC L02 split**: text-output LLM substrates (ILMU, MiniMax, sea_lion) return free-form prose, not parseable JSON. A single `TRUTH ≥ 0.99` FAIL conflated a structural parse failure with a semantic truth failure. CCC separated them:

- `L02A_PARSEABILITY` — PASS/FAIL on structural extraction
- `L02B_TRUTH_VERACITY` — PASS/FAIL/NOT_EVALUATED; `NOT_EVALUATED` when `L02A=FAIL`

This dataset ships the split as a live audit, not only as documentation.

---

## Files

| File | Purpose |
|------|---------|
| `probes_v1.json` | Probe definitions: prompts, expected verdicts, pass criteria |
| `run_eee_spine_audit.py` | Production audit harness that calls live arifOS endpoints |
| `all_receipts.jsonl` | Timestamped receipts from the latest run |
| `summary.json` | Aggregated verdicts, dominance calculation, final SEAL/HOLD/DEGRADED |

---

## How to run

```bash
cd /root/EEE
python run_eee_spine_audit.py
```

Requirements:

- Live arifOS kernel at `http://127.0.0.1:8088`
- Federation organs reachable on their canonical ports (GEOX 8081, WEALTH 18082, WELL 18083)
- `requests` and standard library only

The harness is intentionally small and auditable. No training, no model weights, no hidden prompts.

---

## Verdict semantics

Verdicts are ranked by strictness:

```
VOID > DEGRADED > HOLD > SABAR > PARTIAL > SEAL
```

The final verdict is the **strictest** verdict returned by any probe. A kernel that reports `SEAL` while an organ is `DEGRADED` is itself `DEGRADED` — that dominance rule is probe `EEE-003`.

---

## Latest run

```json
{
  "dataset": "EEE",
  "title": "Kernel Spine Recovery",
  "run_status": "PASS",
  "kernel_status": "SEAL",
  "degraded_organs": [],
  "probe_count": 5,
  "pass_count": 5,
  "fail_count": 0,
  "hold_count": 0,
  "final_verdict": "SEAL"
}
```

Run timestamp: see `summary.json`.

---

## Relationship to AAA / BBB / CCC / DDD

- **AAA** — Behavioral geometry: coordinate system for model self-location.
- **BBB** — Hallucination audit: when models confabulate about themselves.
- **CCC** — Substrate parseability / truth split (L02A / L02B).
- **DDD** — Register pattern: YAML frontmatter and honest metadata.
- **EEE** — Executable kernel spine audit that enforces the previous findings live.

Together they form a ladder from geometry → diagnosis → substrate → record → proof.

---

## Citation

If you use this dataset, please cite:

```text
ariffazil/EEE: Kernel Spine Recovery — executable constitutional audit for the arifOS federation.
https://huggingface.co/datasets/ariffazil/EEE
```

---

## License

Released under the same license as the arifOS Federation project. See the arifOS repository for full terms.

---

*DITEMPA BUKAN DIBERI — Forged, Not Given.*
