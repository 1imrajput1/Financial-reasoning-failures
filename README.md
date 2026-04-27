# Financial Reasoning Failures in Indian SME Data
### A ground-truth taxonomy of how AI breaks on fragmented financial data — starting from India, generalizing globally

**Built by Manaswi Rajput | Mumbai, India | 2026**

## Why This Exists

Scammers stole over $1 trillion globally in the past 12 months alone.  Fraud scams and bank fraud schemes totaled $442 billion in projected losses globally in 2025.  Most AI fraud detection systems deployed today were built for structured, Western financial data — clean ledgers, standardized formats, mature regulatory infrastructure.

They were not built for India.

India has 63 million small and medium businesses. Most of them record financial transactions across incompatible, informal systems simultaneously — Tally ERP, handwritten ledgers, GST portals, WhatsApp invoices, and Excel sheets that were never designed to talk to each other. The result is financial data that is fragmented by design, inconsistent by necessity, and invisible to every existing AI fraud detection system.

Global e-commerce fraud losses are forecast to more than double from over $40 billion in 2024 to more than $100 billion by 2029.  The emerging markets — India, Southeast Asia, Sub-Saharan Africa, Latin America — are where this growth will be sharpest, and where existing tools will fail most completely.

This repository documents why they fail. Not theoretically. From the ground up.

## What This Repository Is

This is a living taxonomy of **financial reasoning failures** — specific, documented cases where AI systems, automated tools, or logical reconciliation frameworks break when applied to real Indian SME financial data.

Each failure is documented with:
- The data pattern that caused the failure
- Why standard systems misclassify or miss it
- What correct reasoning looks like
- Confidence level of the failure classification
- Whether it is benign, suspicious, or definitively fraudulent

This is not a product. It is infrastructure — the ground truth layer that any AI system operating on Indian financial data needs to be evaluated against.

## Failure Pattern #001: The Timing Gap Misclassification

**Category:** Bank Reconciliation Error  
**Risk Level:** Medium — frequently misclassified as fraud when benign, and as benign when suspicious  
**Documented:** February 2026, Mumbai CA firm workflow observation

### What Happens

A payment of ₹47,500 appears in a vendor's bank statement on March 31. The corresponding invoice in the company's Tally ledger is dated April 3 — three days later.

Standard reconciliation logic flags this as: **MISMATCH — payment precedes invoice.**

A naive fraud detection system escalates it as: **SUSPICIOUS — payment made before goods/services confirmed.**

### Why Both Are Wrong

In Indian SME practice, particularly in manufacturing and trading sectors, advance payments to vendors before invoice generation are standard operating procedure — especially at financial year end (March 31 in India). Vendors receive payment to secure year-end orders. The invoice follows after goods are confirmed dispatched, sometimes days later.

This pattern appears in approximately 23-31% of all year-end transactions in trading and manufacturing SMEs based on CA firm workflow observations. Flagging all of them as suspicious would overwhelm any audit team and destroy trust in the detection system immediately.

### What Correct Reasoning Looks Like

A well-calibrated system should ask:
1. Is this payment within 7 days of invoice date? → If yes, timing gap flag should be LOW priority
2. Does this vendor have a history of advance payment patterns? → If yes, this is expected behavior
3. Is the amount round-numbered AND significantly large AND to a new vendor? → If yes, escalate
4. Does this occur specifically in March? → Apply year-end advance payment prior before escalating

The failure is not detecting the mismatch. The failure is **not knowing what the mismatch means in Indian financial context.**

### Why This Matters Globally

This identical failure pattern exists in any market where informal payment norms predate formal invoicing infrastructure — Indonesia, Nigeria, Brazil, Vietnam. The solution is not a better algorithm. It is a better evaluation framework that encodes real-world payment behavior before classifying anomalies.

## What Is Being Built

A Python-based reconciliation and anomaly detection engine that:
- Ingests bank statements, Tally ledger exports, and GST data simultaneously
- Applies Indian-context reasoning before flagging anomalies
- Outputs structured failure classifications with confidence levels and alternative hypotheses
- Builds toward a synthetic Indian financial dataset that can be used to train and evaluate future AI systems

The tool is being developed from inside real CA firm workflows — not from theory.

## Current Status

- [x] Bank statement vs ledger reconciliation tool — Excel version complete
- [x] Failure Pattern #001 documented (this file)
- [ ] Python version of reconciliation engine — in progress
- [ ] Failure Pattern #002: Vendor name normalization failures across GST and Tally
- [ ] Failure Pattern #003: Round-number bias in fraud detection on Indian SME data
- [ ] Synthetic data generator for Indian financial reasoning evaluation

## The Global Argument

India is not a niche market. It is the proving ground.

The problem of fragmented, informally-recorded financial data is not uniquely Indian. It is the defining condition of every economy where most people entered formal finance before the infrastructure was ready for them. Southeast Asia. Sub-Saharan Africa. Latin America.

AI systems built and evaluated only on Western financial data will fail in all of these markets — silently, at scale, with real consequences for real people.

This taxonomy starts in India because India has the highest density of this problem and because this is where genuine domain access exists. The failure patterns documented here will generalize. That is the point.

## Contact

Manaswi Rajput
manaswi.rajput22@spit.ac.in
Mumbai, India
