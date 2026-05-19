[README_GITHUB.md](https://github.com/user-attachments/files/28016236/README_GITHUB.md)
# Information Rocket Dynamics (V9.0)

**Inference-Time Distributional Dynamics and Adaptive Control for LLM Reasoning**

An empirical study of **prompt-conditioned distributional regimes**, **non-monotonic entropy vs. temperature**, **path-dependent hysteresis**, and a **Schmitt-trigger closed-loop temperature actuator** for streaming LLM inference.

> I am an undergraduate researcher in China. Feedback and collaboration are welcome. This repo focuses on hallucination-related distributional shocks in autoregressive generation and how to detect and mitigate them with reproducible, logprob-based probes.

**Preprint manuscript (Markdown):** unzip `V9_preprint_bundle.zip` → `paper/manuscript.md`  
**Raw V9.0 step log:** `code/closed_loop_data.json` (400 controlled + 400 baseline tokens)

---

## Key results (V9.0, `qwen2.5:7b`, Ollama local)

| Metric | Controlled | Baseline (fixed T=0.65) |
|--------|------------|-------------------------|
| Mean Shannon H | 0.611 | 0.633 |
| Peak Shannon H | **2.289** | 2.644 (**−13.4%** tail clip) |
| Schmitt gate duty | 217/400 (54.3%) | — |

**Claim scope:** streaming **entropy shock clipping** (safety layer), not human-preference or downstream task gains in this release.

---

## Reproduce

**Requirements:** Ollama ≥ 0.12.11, `qwen2.5:7b`, Python 3.10+, `numpy`, `matplotlib`

```bash
git clone https://github.com/reapx739-create/Information-Rocket-Dynamics.git
cd Information-Rocket-Dynamics
# Unzip bundle or copy code from paper/code/ after unzip
unzip V9_preprint_bundle.zip
cd code
pip install numpy matplotlib
python v9.0_closed_loop.py
```

Ollama must be running at `http://localhost:11434`.  
`logprobs` and `top_logprobs` must be set at the **top level** of `/api/chat` (see `ollama_utils.py`).

---

## Bundle contents (`V9_preprint_bundle.zip`)

```
paper/
  manuscript.md          # Full English preprint (Methods = validity backbone)
  VALIDITY_CHECKLIST.md  # Reviewer Q&A map
  figures/               # fig1_schmitt_gate.png, fig2_entropy_comparison.png
code/
  controller.py          # Schmitt + exponential relaxation
  ollama_utils.py          # Token-wise Ollama HTTP client
  v9.0_closed_loop.py    # Main experiment
  closed_loop_data.json  # Reproducibility log
```

---

## Citation (placeholder)

```bibtex
@misc{information_rocket_v9_2026,
  author       = {reapx739-create},
  title        = {Prompt-Conditioned Distributional Regimes and Schmitt-Trigger Closed-Loop Temperature Control for Streaming LLM Inference},
  year         = {2026},
  howpublished = {\url{https://github.com/reapx739-create/Information-Rocket-Dynamics}},
}
```

---

## License

Specify license before wide redistribution (e.g. MIT / CC-BY-4.0). [TODO]

---

## Contact

Open an [Issue](https://github.com/reapx739-create/Information-Rocket-Dynamics/issues) for questions or replication failures.


