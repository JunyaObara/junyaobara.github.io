# First-Pass Privacy Compliance Review 
# using Amazon Bedrock Knowledge Bases



Personal project. Public, non-confidential summary.

This repository documents a statute-grounded PoC that turns early-stage software requirements into privacy-risk triage outputs for three U.S. privacy laws:

- **BIPA** (Illinois Biometric Information Privacy Act)
- **CIPA** (California Invasion of Privacy Act)
- **VPPA** (Video Privacy Protection Act)

The goal is **not** to automate legal advice. The goal is to produce a **traceable first-pass triage** that can reduce legal review bottlenecks by returning:

- an external verdict label: `BLOCKER / NEEDS_REVIEW / CLEARED`
- human routing when review is needed: `DEV / LEGAL / POLICY`
- statute-grounded evidence and remediation-oriented recommendations

---

## What this repository is intended to prove

This repo is meant to show that I built a PoC with:

- **held-out evaluation**, not only in-sample validation
- **cold-run execution**, not a warm-cache vanity benchmark
- **artifact-backed auditability**
- explicit separation of **`run_ok`** and **`claim_ready`**
- honest disclosure of benchmark limitations

It is **not** meant to claim production-ready legal accuracy.

---

## Final held-out cold test

### Protocol

- **Target**: `data/spec_all_test_final.v1.0.2.jsonl`
- **Protocol kind**: `holdout`
- **In-sample**: `false`
- **Checklist source**: `FROZEN_VALIDATION_CHECKLISTS`
- **Bootstrap overlap**: `0`
- **Cold run**: yes
- **Cache namespace hardened**: yes
- **Runner input contains expected labels**: no
- **Visible prompt label leakage count**: 0

### Primary results

- **Test samples**: **42**
- **Outcome accuracy**: **83.3%**
- **Routing accuracy**: **73.1%** on **26 routing-applicable samples**
- **Basis citation F1**: **91.9%**
- **Governing coverage F1**: **69.8%**

### Important caveat

The run itself succeeded, but the benchmark gate still says:

- **`run_ok = true`**
- **`claim_ready = false`**

Main reasons:

- coverage warnings are still present
- KB provenance is incomplete
- the validation-derived checklist source still contains conflicting answer buckets
- the benchmark family is still synthetic / template-only

This is intentional. I treat unsupported claims as a failure mode and surface them instead of hiding them.

---

## What the result does and does not mean

### What it means

The PoC demonstrates:

- non-trivial held-out performance under **cold** conditions
- strong **basis-citation quality**
- a reproducible, statute-grounded evaluation pipeline
- explicit risk gating around benchmark validity and claim scope

### What it does **not** mean

This result does **not** prove:

- production-ready legal accuracy
- real-world performance on lawyer-authored free-form documents
- complete explainability coverage across all three laws

In the current test pack, **support-citation gold is incomplete outside CIPA**, so support/explainability is **not** used as a headline KPI.

---

## Why the benchmark is still limited

This PoC was built by an individual, without access to a large lawyer-authored benchmark. The current benchmark family is therefore:

- statute-derived
- checklist-derived
- template-heavy

That makes it useful for:

- regression testing
- held-out testing within the same benchmark family
- traceability and systems evaluation

But it is still limited for:

- broad real-world legal generalization claims
- external validity claims beyond the current benchmark family

---

## Public evidence included in this repository

Recommended files to review first:

- `validation_final.json`
- `benchmark_readiness.json`
- `effective_config.json`
- `run_eval_out/summary.json`
- `classification_metrics_by_law.json`
- `run_eval_out/worst_slice_summary.json`
- `coverage_report.json`
- `audit_checklist_leakage.report.json`
- `llm_costs.csv`
- `section24_final_test_holdout_cold_20260307T090416Z.zip.sha256`

These files show:

- protocol and cold-run conditions
- model / region / KB configuration
- primary scores and denominators
- claim-readiness gate reasons
- leakage / overlap checks
- cost and cache behavior
- immutable checksum for the evidence pack

---

## Why some raw files are not public

I do **not** publish the full held-out test text or the full raw trace set publicly, because that would weaken the benchmark for future reuse and would expose raw prompt / dataset details that are not necessary for a recruiter-facing summary.

Public repo = curated, recruiter-safe evidence.

Private evidence pack = full forensic record, preserved separately for later audit if ever needed.

---

## Project framing for interviews

The honest framing is:

> This is not a production legal-advice system. It is a statute-grounded privacy-risk triage PoC with a held-out cold test, audit-style evidence packaging, and explicit benchmark gates that prevent me from overstating unsupported claims.

That is the point of the project.

---

## Notes

- Personal project only
- Public summary only
- No employer confidential information is included here
