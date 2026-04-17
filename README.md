# Cache Timing Side-Channel Analysis of T-Table AES on RISC-V

A portfolio repository for an **experimental cache side-channel study** targeting a **T-table AES implementation** on a **RISC-V platform**.

The project evaluates how an access-driven **Prime+Probe** attack behaves on **real hardware**, with a focus on **leakage observability**, **cache-set classification**, and **partial key inference** under realistic but controlled conditions.

## 🔍 Overview

This work studies the practical feasibility of a **cache timing side-channel attack** against **AES implemented with T-tables**.

The attack targets the **private L1 data cache** of a **BeagleV Fire / PolarFire SoC** platform and investigates how much key-dependent information remains recoverable once real-world noise sources are taken into account.

Rather than proposing a completely new attack, the project **replicates and adapts a known Prime+Probe methodology** to a specific **RISC-V microarchitecture**, then measures how architectural constraints, cache geometry, and system noise affect exploitability.

## ⚙️ Technical Focus

- **Prime+Probe** attack methodology
- **T-table AES** leakage model
- **RISC-V / PolarFire SoC** evaluation platform
- **Private L1 data cache** as attack target
- **Per-set cache analysis**
- **Noise-aware statistical classification**
- **Partial AES key recovery**
- **Controlled real-hardware experimentation**

## 🧠 Main Contributions

- Development and validation of a **cache-timing measurement framework** on real RISC-V hardware
- Experimental evaluation of **access-driven leakage** at **cache-set granularity**
- Separation of the attack into three stages:
  - **leakage detection**
  - **cache-set classification**
  - **key inference**
- Analysis of how **noise**, **cache-set heterogeneity**, and **measurement aggregation** affect attack quality
- Empirical characterization of the gap between **theoretical leakage** and **practical exploitability**

## 📊 Results Snapshot

| **Area** | **Result** |
|---|---|
| **Target platform** | **BeagleV Fire / Microchip PolarFire SoC** |
| **Architecture** | **RISC-V** |
| **Attack type** | **Prime+Probe** |
| **Target resource** | **Private L1 data cache** |
| **Victim** | **T-table AES implementation** |
| **Leakage granularity** | **Cache-set / cache-line level** |
| **Key information recovered** | **Most significant 4 bits of AES key bytes** |
| **Single-round inference** | **100% accuracy on high nibbles** |
| **Single-run time** | **~2 min 52 s** |
| **Multi-round behavior** | **Inference accuracy degrades as AES rounds increase** |
| **Key observation** | **Leakage quality is highly non-uniform across cache sets** |

## 🧪 Methodology

The attack is implemented under a **controlled threat model** in which attacker and victim are **time-multiplexed on the same core**, enabling temporal sharing of the **private L1 cache**.

The workflow is structured as follows:

1. **Prime** selected cache sets with attacker-controlled data  
2. Let the **victim execute AES**, producing key-dependent T-table accesses  
3. **Probe** the same sets and classify access latency  
4. Aggregate observations across repeated runs  
5. Rank key candidates using the inferred cache activity

A major part of the work is devoted to **noise mitigation**, including:
- **pointer chasing**
- **median-based aggregation**
- **outlier rejection**
- **per-set thresholding**
- exclusion of **non-informative cache sets**

## 📌 Key Findings

- **Leakage is clearly observable** on the target platform in the controlled setting
- **Reliable exploitation** requires more than raw timing measurements
- **Per-set analysis matters**: some cache sets are informative, others are structurally noisy
- **Aggregation improves prediction accuracy**, but cannot fully compensate for intrinsically bad sets
- **Perfect partial key recovery** is achieved only in the **single-round** setting
- The work highlights the difference between **side-channel existence** and **practical attack effectiveness**

## 🔒 Limitations

This project intentionally studies a **favorable but explicit** setting.

Important assumptions include:
- attacker and victim scheduled on the **same core**
- attack restricted to the **L1 data cache**
- **chosen or known plaintexts**
- **page-aligned T-tables**
- **minimal system load**
- analysis focused on the **first AES round**

These choices make the experiment interpretable and reproducible, but they also limit generality.

## 📄 Repository Content

- **`Report_SP_Fortunelli.pdf`** — full technical report

## 📘 Report

[**Open the report**](./Report_SP_Fortunelli.pdf)

## 🔒 Source Code Availability

The source code is **not publicly available** for academic reasons.  
It can be shared upon request for **recruiting purposes**.