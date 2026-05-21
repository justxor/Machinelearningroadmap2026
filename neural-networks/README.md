# 🧠 Neural Networks: from zero to production — a practical course

This is the second modular course of the repository. After [math-for-ml/](../math-for-ml/README.md) — it's time to build a neural network by hand and go all the way from a linear neuron to your own transformer, multimodal models, and distributed training.

## Why this course

Most neural-network courses do one of two things:

- They teach you to run pre-built models from Hugging Face and call that "studying neural networks".
- Or they bury you in math and leave you without code that actually runs.

This course is about **the middle**: enough math to know what you're doing, and **a lot of code** that runs locally on CPU or free Colab.

## Who this is for

- You finished [math-for-ml/](../math-for-ml/README.md) or know derivatives, matrices, and basic probability.
- You can write Python and have worked with NumPy.
- You want to **build and train models**, not just call `model.fit()`.

## Stack

- **Python 3.10+**, **PyTorch 2.x**, **NumPy**, **Matplotlib**.
- Optional: **torchvision**, **transformers**, **datasets**, **diffusers**, **peft**, **trl**, **torch_geometric**, **accelerate**.
- Hardware: CPU is enough for most lessons. Lessons 9-18 are more comfortable with a GPU (free Colab works). Lessons 17-18 want two GPUs (or simulate with `torchrun --nproc_per_node=2`).

## Course structure

**Block 1. Foundational neural networks**

- [01. Perceptron and linear models](./01-perceptron.md)
- [02. MLP and backpropagation](./02-mlp-backprop.md)
- [03. Activation functions and weight initialization](./03-activations-init.md)
- [04. Regularization: dropout, BatchNorm, weight decay](./04-regularization.md)
- [05. Optimizers: SGD, Momentum, Adam, AdamW](./05-optimizers.md)

**Block 2. Architectures**

- [06. CNN from scratch: convolutions, pooling, image classification](./06-cnn.md)
- [07. RNN, LSTM, GRU and sequences](./07-rnn-lstm.md)
- [08. Attention and self-attention](./08-attention.md)
- [09. Transformer end to end](./09-transformer.md)

**Block 3. Application and production**

- [10. Embeddings and tokenization](./10-embeddings-tokenization.md)
- [11. Fine-tuning and transfer learning](./11-finetuning.md)
- [12. From model to production: ONNX, quantization, inference](./12-production.md)

**Block 4. Advanced architectures**

- [13. Vision Transformers and multimodal models](./13-vision-transformers.md) — ViT, CLIP, LLaVA, SAM, DINOv2.
- [14. Diffusion models](./14-diffusion.md) — DDPM from scratch, Stable Diffusion, classifier-free guidance.
- [15. RLHF, DPO, and LLM alignment](./15-rlhf-dpo.md) — instruction-tuning, reward model, PPO, DPO, KTO, GRPO.
- [16. Graph Neural Networks (GNN)](./16-gnn.md) — GCN, GAT, message passing, PyTorch Geometric.
- [17. Self-supervised and contrastive learning](./17-self-supervised.md) — SimCLR, MAE, DINO, BERT MLM.
- [18. Distributed training](./18-distributed-training.md) — DDP, FSDP, mixed precision, gradient checkpointing.

## 📋 Cheatsheet

[**cheatsheet.md**](./cheatsheet.md) — a unified reference for the whole course: formulas, default hyperparameters, common pitfalls. Open it when you forget how layer norm is computed or what lr to pick for AdamW.

## 🎯 Capstone projects

After the main blocks of the course come three portfolio projects in the [capstones/](./capstones/README.md) folder:

- [**Capstone 1.** End-to-end image classification](./capstones/01-image-classifier.md) — CNN + augmentations + ONNX + Streamlit demo.
- [**Capstone 2.** MiniGPT on your own dataset](./capstones/02-mini-gpt.md) — BPE + transformer from scratch + chat-style generation.
- [**Capstone 3.** Production-ready RAG assistant](./capstones/03-rag-assistant.md) — embeddings + vector DB + LLM + FastAPI + Docker + monitoring.

Each capstone is a **separate repository** that you put on GitHub and show in interviews.

## How to take it

1. **One lesson per week.** Do not try to cram it all in one weekend.
2. First read the theory, then walk through the code **line by line**, then rewrite the code from scratch **without peeking**.
3. Do **all 8 practice tasks** at the end of each lesson. Without them, the course is useless.
4. After each major block, do the matching capstone in the [capstones/](./capstones/README.md) folder.

## What you will leave with

- An understanding of **what is actually happening** inside `loss.backward()` and `optimizer.step()`.
- The ability to build any modern architecture **from primitives**, not from prebuilt blocks: CNN, RNN, Transformer, ViT, GNN, Diffusion.
- A ready fine-tuning template (LoRA, QLoRA, DPO) that you can reuse at work.
- An understanding of how a model **goes to production** — not "by magic", but via ONNX, quantization, and a REST wrapper.
- Experience with distributed training (DDP, FSDP, mixed precision).
- 3 portfolio projects.

## Principles

- **80% practice, 20% theory.** Formulas are only the ones that pay off during debugging.
- **No magic.** Every lesson has at least one "write the same thing from scratch without libraries" example.
- **Minimal dependencies.** The fewer `pip install`s, the longer your code survives.
- **Reproducibility.** Every code snippet must run unchanged.

---

▶︎ Start: [Lesson 01 — Perceptron and linear models](./01-perceptron.md)
