# 🧮 Math for Machine Learning: from zero to pro

An applied course in the math you actually need for ML and DL. No academic dryness, no deriving every theorem in a row, no "let's first slog through 30 pages of definitions". Every lesson: **short theory → formula → NumPy code → 5–10 exercises**.

> The goal of this course is for you to open an arXiv paper and understand what is written. For deriving a gradient in backprop to be routine, not magic. For you to know **why this particular formula**, not "because that's how the library does it".

---

## 🎯 Who this is for

- **High-school math at a C level.** The course starts from the very basics.
- **Engineers without a math-school background** who can code but stumble on calculus and linear algebra.
- **Students** who want to see how abstract math becomes working models.
- **Anyone who read a roadmap, hit "gradient with respect to a matrix", and closed the tab.**

After the course you will be able to: derive a loss gradient by hand, implement linear regression via the normal equations, write PCA via SVD, and understand what attention does inside a transformer.

---

## 📚 Course structure

12 lessons split into 4 blocks. Each lesson is a separate file with theory, code, and practice. Go strictly in order.

### Block I. Linear algebra (foundation)

| # | Lesson | What's inside |
|---|--------|---------------|
| [01](./01-vectors.md) | **Vectors and operations** | Addition, scalar product, dot product, norm, cosine of angle. Why this matters for embeddings. |
| [02](./02-matrices.md) | **Matrices and linear maps** | Matrix multiplication as composition of mappings. Transpose, inverse. |
| [03](./03-eigen-svd.md) | **Eigenvalues and SVD** | Spectral decomposition, SVD, PCA from scratch in NumPy. |

### Block II. Calculus (for optimization)

| # | Lesson | What's inside |
|---|--------|---------------|
| [04](./04-derivatives.md) | **Derivatives and gradients** | Derivative as a rate, partial derivatives, gradient. Geometry of gradient descent. |
| [05](./05-chain-rule.md) | **Chain rule and backprop** | Function composition, chain rule, hand-derived backprop for a two-layer network. |
| [06](./06-matrix-calculus.md) | **Matrix calculus** | Gradient with respect to a vector and a matrix. Jacobian, Hessian. The formulas you need every day. |

### Block III. Probability and statistics

| # | Lesson | What's inside |
|---|--------|---------------|
| [07](./07-probability.md) | **Probability from scratch** | Events, conditional probability, Bayes' rule. Discrete and continuous distributions. |
| [08](./08-distributions.md) | **Key distributions** | Bernoulli, binomial, normal, Poisson. Central limit theorem via simulation. |
| [09](./09-mle-map.md) | **MLE and MAP** | Maximum likelihood, posterior estimation. Where MSE and cross-entropy come from. |

### Block IV. Math of deep learning

| # | Lesson | What's inside |
|---|--------|---------------|
| [10](./10-optimization.md) | **Optimization** | GD, SGD, Momentum, Adam — formulas and intuition. Saddle points, local minima. |
| [11](./11-information-theory.md) | **Information theory** | Entropy, KL divergence, cross-entropy. Why they show up in classification and VAEs. |
| [12](./12-transformer-math.md) | **The math of transformers** | Attention as softmax(QK^T/√d)V — line by line. Position encoding. Multi-head. |

---

## 🛠️ How to study

1. **Install Python 3.12+, NumPy, Matplotlib, Jupyter.** 10 minutes.
2. **Open a lesson and read the theory part.** 20–30 minutes.
3. **Retype the code examples by hand** (do not copy — type). Run, break, fix.
4. **Do every exercise at the end of the lesson.** Not optional. Without practice the course does not work.
5. **Put your solutions into a repo** `math-for-ml-solutions` — it becomes part of your portfolio.
6. **Move to the next lesson only after closing the current one.** No skipping.

**Pace:** 1–2 lessons a week. The whole course is 2–3 months of steady work or 6 weeks of intensive study.

---

## 🧰 What you need

```bash
pip install numpy matplotlib scipy jupyter
```

That's it. No heavy frameworks at this stage — we want to see the math, not hide it behind `model.fit()`.

---

## 🚫 What this course is not

- Formal math-department-level proofs. If you need rigor, take Axler, Strang, or Spivak.
- Filler and pretty pictures without substance.
- Exercises like "find the derivative of a 5th-degree polynomial". Only tasks that move you closer to real ML problems.
- Statements like "just memorize the formula". Each formula is derived or at least explained geometrically.

---

## 📖 Read alongside

- **3Blue1Brown — Essence of Linear Algebra, Essence of Calculus** (YouTube, free). The best intuition visualization out there.
- **Mathematics for Machine Learning** — Deisenroth, Faisal, Ong. Free PDF at [mml-book.github.io](https://mml-book.github.io).
- **Deep Learning Book** — Goodfellow, Bengio, Courville. Chapters 2–4 map perfectly onto this course.
- **The Matrix Cookbook** — a reference for matrix calculus. Keep it open in a tab.

---

## ✅ Final checklist after the course

You have finished the course if, without help, you can:

- Derive the gradient of MSE with respect to the weights of linear regression.
- Explain why cross-entropy naturally follows from MLE for classification.
- Write PCA via SVD in 15 lines of NumPy.
- Explain what each operation in `softmax(QK^T / sqrt(d)) @ V` does.
- State how Adam differs from SGD and why it is usually better.
- Read a random page from a modern ML paper and understand the formulas.

If even one item is shaky, go back to the matching lesson.

---

> Math in ML is not an obstacle but a tool. Once you see it, models stop being black boxes. [← Back to roadmap](../README.md)
