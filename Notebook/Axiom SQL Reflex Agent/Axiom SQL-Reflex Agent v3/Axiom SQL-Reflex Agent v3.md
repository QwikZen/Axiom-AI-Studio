# Axiom SQL-Reflex (v3.0)
### Execution-Aware, Semantic-Audited, Industry-Scale Text-to-SQL Agent

---

## Executive Summary
**Axiom SQL-Reflex v3** is a research-grade autonomous system designed to bridge the gap between "toy demos" and production-ready data intelligence. Developed at **Axiom AI Studio (QwikZen)**, v3 moves beyond syntax-checking to implement **Answer-Level Semantic Validation**.

While previous versions focused on "Retrying SQL," v3 treats the database as an active participant in a **Reflexive Reasoning Loop**. It ensures that correctness is not just about code that *runs*, but about data that *answers the question*.

---

## System Architecture: The "Pentagon" Orchestration
V3 decomposes the Text-to-SQL pipeline into five specialized agents working in a continuous feedback loop.

### 1. The Cartographer (Schema RAG)
* **Tech:** `FAISS` + `Sentence-Transformers`.
* **Role:** Performs high-entropy schema retrieval to ground the agent in the real 1GB dataset, preventing column hallucinations.

### 2. The Architect (SQL Generator)
* **Tech:** `Llama-3-8B-Instruct` (Local GGUF).
* **Role:** Generates multiple high-performance SQL hypotheses specifically optimized for **DuckDB** analytical syntax.

### 3. The Verifier (Execution Sandbox)
* **Tech:** `DuckDB` (Analytical Engine).
* **Role:** Executes SQL against a 1GB market dataset. It catches syntax errors and feeds the "Instructional Pain" back to the Architect.

### 4. The Semantic Auditor (The Brain)
* **Innovation:** Verifies if the *content* of the result matches the *intent* of the question.
* **Logic:** Rejects "Empty sets," "Type mismatches," or "Aggregation errors" (e.g., returning 100 rows when the user asked for a "Max" value).

### 5. The Reflex Controller (Convergence)
* **Role:** Manages the "Retry Budget" and convergence metrics. It ensures the system settles on a stable, validated answer.

---

## 🛠️ Key Technical Moats
* **Industry-Scale Backend:** Uses DuckDB to handle millions of rows of NASDAQ stock data with sub-second latency.
* **Local Inference:** Powered by Meta Llama 3, ensuring zero API dependency and full privacy.
* **Composite Agent Score:** A multi-dimensional metric (0-100) that evaluates accuracy, semantic pass rate, and latency stability.

---

## Performance Benchmarks (The v3 Leap)

| Metric | Formula / Description | V3 Performance |
| :--- | :--- | :--- |
| **Composite Agent Score** | Weighted Accuracy + Latency + Stability | **88.5 / 100** |
| **Execution Accuracy** | Successful Runs / Total Runs | **96.4%** |
| **Semantic Accuracy** | Logic-matching results / Executed SQL | **94.2%** |
| **Recovery Rate** | Success after initial failure | **~90%** |
| **Avg Latency** | Inference-time compute per iteration | **~0.85s** |

---

## Visual Analysis: Convergence & Behavior

### 1. Execution-Reflex Convergence
V3 typically converges to a correct, semantically-validated answer in **1.14 iterations**. This suggests the "First-Attempt" logic is strong, but the "Reflex" serves as a critical safety net.

### 2. Semantic Pass Rate
Unlike v1/v2, v3 shows a high correlation between "SQL running" and "Answer being correct," thanks to the **Semantic Auditor** filtering out valid-but-wrong SQL.

---

## Sample Execution Trace
```text
[Reflex Iteration 1]
→ Cartographer: Mapping 'highest price' to column 'high'
→ Architect: Generating SELECT MAX(high) FROM stocks;
→ Verifier: Execution Successful (1 row)
→ Semantic Auditor: Pass (Aggregation matches 'highest' intent)
✅ Success in 0.84s (Composite Score: 91.2)
