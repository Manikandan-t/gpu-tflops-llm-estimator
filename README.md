# 🎯 GPU TFLOPS & LLM Throughput Estimator

## 📖 Welcome — What This Tool Teaches You

If you've ever stared at NVIDIA’s glossy datasheets claiming *“4,500 TFLOPS!”* and then watched your actual LLM crawl along at 40 tokens per second, this guide is for you.

The gap between headline numbers and real-world performance is massive—often **10× to 50×**. Understanding *why* that gap exists is what separates engineers who choose the right hardware from those who burn through budgets with little to show for it.

---

## 🎯 Who Is This For?

This tool assumes **zero prior knowledge** of GPU architecture or LLM inference.

By the end, you will be able to:

* Understand what a **TFLOP** actually is and how to compute it from hardware specs
* Choose the right GPU for LLMs ranging from **7B to 405B parameters**
* Estimate **real-world throughput**, not misleading peak numbers
* Identify whether your workload is **memory-bound vs compute-bound**
* Build a **credible Total Cost of Ownership (TCO)** model
* Avoid the most common (and expensive) mistakes in GPU selection

---

## 🧭 How to Use This Tool

This is not meant to be read linearly.

* Start with **Fundamentals** for conceptual grounding
* Use the **Calculator** to experiment and build intuition
* Refer to **Specs**, **Throughput Math**, and **TCO** when designing real systems

Think of this as a **learning tool + reference manual**, not a blog post.

---

## 💡 The One Big Idea You Must Understand

> **For most real LLM inference workloads, memory bandwidth matters more than compute TFLOPS.**

This is the single most important concept in GPU selection.

A GPU with:

* **100 TFLOPS + 4 TB/s bandwidth**

will often outperform:

* **200 TFLOPS + 2 TB/s bandwidth**

This is counterintuitive—but critical.

### Why This Happens

During inference (especially decoding):

* Each generated token requires reading large portions of the model from memory
* Compute units finish their work quickly
* Then they **stall, waiting for data**

This makes **memory bandwidth the bottleneck**, not raw compute.

### Real-World Example

* **H100 vs H200**

  * Same compute capability
  * H200 has significantly higher memory bandwidth
  * Result: ~**1.9× better performance** on Llama-70B

The only meaningful difference? **Memory bandwidth (4.8 TB/s vs 3.35 TB/s)**.

---

## 🧠 Key Takeaway

For decode-heavy workloads:

> **Bandwidth is the real currency.**

We’ll explore this deeper using the **roofline model** in the Fundamentals section—but keep this idea front and center as you go.

---

This version significantly improves accuracy, coverage, and depth.

### 🔧 Corrections & Accuracy Fixes

* Fixed **B200 Tensor Core count** (640, not 528)
* Corrected **RTX PRO 6000 FP16 performance** (~480–500 TFLOPS dense, not 1,805)
* Proper distinction between **dense vs sparse TFLOPS** across all sections

---

### 🆕 New Hardware Coverage

* B200A
* B300 (Blackwell Ultra)
* GB200 NVL72 rack
* GB300 NVL72 rack
* Preview: **Vera Rubin NVL72** (expected H2 2026)

---

### 📐 Improved Modeling & Formulas

* Full **FLOPs-per-token derivation**, including:

  * Attention
  * Feed-forward networks (FFN)
  * Embeddings

No more oversimplified formulas like:

```
2 × d² × layers
```

---

### 📚 New Learning Sections

* **Roofline Model**

  * Visual + interactive explanation
  * Automatic regime detection (memory vs compute bound)

* **TCO Framework**

  * Realistic pricing (April 2026)
  * Infrastructure-level cost modeling

* **Quantization Tradeoffs**

  * Real benchmark comparisons
  * Performance vs accuracy insights

* **Model-to-Hardware Mapping**

  * Practical selection guidelines
  * From small (7B) to frontier-scale (405B) models

---

## ⚠️ Final Note

This tool is designed to build **intuition that sticks**.

Don’t rush through it.

Jump between sections, experiment with the calculator, and revisit the reference material when making real decisions.

Because in this space, **intuition + first-principles thinking** is what saves time, money, and failed deployments.
