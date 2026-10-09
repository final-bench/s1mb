<div align="center">

# 🏆 Darwin-27B-ZTC-v2 — #1 on S1MB

### The System One Mosaic Benchmark, ranked #1 of 102 models. A typed-decision judge that scores a decision in a single forward pass, with zero generated tokens.

[![S1MB #1](https://img.shields.io/badge/S1MB-%231_of_102-ff6b8b?style=for-the-badge)](https://huggingface.co/spaces/hotchpotch/S1MB-leaderboard)
[![Model](https://img.shields.io/badge/%F0%9F%A4%97_Model-Darwin--27B--ZTC--v2-ffb020?style=for-the-badge)](https://huggingface.co/FINAL-Bench/Darwin-27B-ZTC-v2)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue?style=for-the-badge)](LICENSE)

[![Website](https://img.shields.io/badge/Website-vidraft.net-4ea8ff)](https://vidraft.net)
[![Stars](https://img.shields.io/github/stars/final-bench/s1mb?style=social)](https://github.com/final-bench/s1mb)
[![ZTC](https://img.shields.io/badge/Method-ZTC-6f42c1)](https://github.com/final-bench/ztc)
[![X](https://img.shields.io/badge/%F0%9D%95%8F-@VIDRAFT__ai-000000)](https://x.com/VIDRAFT_ai)
[![Threads](https://img.shields.io/badge/Threads-@vidraft__lab-101010)](https://www.threads.com/@vidraft_lab)

</div>

---

**Darwin-27B-ZTC-v2** is VIDRAFT's typed-decision judge. On the **System One Mosaic Benchmark (S1MB)** it ranks **#1 overall among 102 models**. It reads a decision problem — a condition, a set of choices, a score to assign — and returns its judgement in **one forward pass, generating zero tokens**, using the [ZTC (Zero-Token Confidence)](https://github.com/final-bench/ztc) method.

The weights are on Hugging Face. This repository holds the result, the benchmark context, and how to run the model.

## 🥇 The result

| Rank | Benchmark | Field | Models | Result |
|---|---|---|---|---|
| **#1** | S1MB (System One Mosaic Benchmark) | Typed decisions | 102 | **1st overall** |

- Leaderboard: https://huggingface.co/spaces/hotchpotch/S1MB-leaderboard
- Typed-decision accuracy: **0.743** zero-shot, #1.
- Decisions are scored with **zero generated tokens**, so judgement is deterministic and one forward pass per item.

## 🧠 What S1MB measures

S1MB (System One Mosaic Benchmark) evaluates a model's fast, intuitive "System 1" decision quality across a mosaic of typed decision tasks: given a condition and candidate choices, pick and score the right one. It is a decision benchmark, not a text-generation benchmark, which is exactly what a zero-token judge is built for.

## 🤗 The model

| Model | Role | Params | Hugging Face |
|---|---|---|---|
| **Darwin-27B-ZTC-v2** | Typed-decision judge, **#1 on S1MB** | 27B | [link](https://huggingface.co/FINAL-Bench/Darwin-27B-ZTC-v2) |
| Darwin-27B-ZTC | Typed-decision judge (v1) | 27B | [link](https://huggingface.co/FINAL-Bench/Darwin-27B-ZTC) |
| Darwin-397B-ZTC | Largest judge | 397B | [link](https://huggingface.co/FINAL-Bench/Darwin-397B-ZTC) |

The full ZTC family (including the ZTC-Judge answer-verification line) lives at **[github.com/final-bench/ztc](https://github.com/final-bench/ztc)**.

## ⚡ How it works (ZTC)

```
text  = template(condition, choices)
h     = model(text).last_hidden_state[last_non_pad_token]   # one forward pass, 0 tokens generated
score = ((h - mu) / sd) @ w                                 # calibrated probe -> decision
```

- **Zero tokens:** no decoding loop, so the decision is deterministic and cheap.
- **One pass:** one forward pass per decision, fast enough to run on every item.
- **Calibrated:** the probe is fitted leave-one-domain-out, so reported figures come from domains the probe never saw.

Full method and inference code (`ztc_judge.py`, `usage_curve.py`): **[github.com/final-bench/ztc](https://github.com/final-bench/ztc)**.

## 🚀 Usage

```python
from transformers import AutoModel, AutoTokenizer
# weights: https://huggingface.co/FINAL-Bench/Darwin-27B-ZTC-v2
# decision scoring code: https://github.com/final-bench/ztc
```

See the model card and the ztc repository for the exact decision template and probe parameters.

## ❓ FAQ

<details><summary><b>Which model is #1 on S1MB?</b></summary>
Darwin-27B-ZTC-v2 by VIDRAFT is #1 overall on the System One Mosaic Benchmark among 102 models.
</details>

<details><summary><b>What is the System One Mosaic Benchmark (S1MB)?</b></summary>
S1MB evaluates fast, intuitive "System 1" typed-decision quality: given a condition and candidate choices, pick and score the right one. It is a decision benchmark rather than a text-generation benchmark.
</details>

<details><summary><b>How does a model decide with zero tokens?</b></summary>
Darwin-27B-ZTC-v2 uses ZTC (Zero-Token Confidence): it reads the problem in one forward pass, takes the final-layer hidden state, and applies a calibrated probe to produce a decision, generating no text at all. This makes it deterministic and one forward pass per decision.
</details>

<details><summary><b>Where are the weights and the code?</b></summary>
Weights: Hugging Face FINAL-Bench/Darwin-27B-ZTC-v2. Method and inference code: github.com/final-bench/ztc.
</details>

## 📫 Connect

🌐 [vidraft.net](https://vidraft.net) · 🤗 [FINAL-Bench](https://huggingface.co/FINAL-Bench) · 🛡️ [ZTC](https://github.com/final-bench/ztc) · 🧵 [@vidraft_lab](https://www.threads.com/@vidraft_lab) · 𝕏 [@VIDRAFT_ai](https://x.com/VIDRAFT_ai) · ✉️ `vidraft@mail.vidraft.net`

## 📜 License

Apache-2.0 · Built by **VIDRAFT** · *Beyond AI, Toward AGI.*

<div align="center"><sub>S1MB · System One Mosaic Benchmark · typed decisions · decision AI · zero-token · ZTC · Darwin-27B-ZTC-v2 · #1 leaderboard · VIDRAFT</sub></div>
