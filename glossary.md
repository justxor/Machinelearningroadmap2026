# 📖 Glossary: ML / DL / LLM / MLOps

An extended dictionary of terms you will encounter in this roadmap and in real work. The goal is not encyclopedic completeness, but **working understanding**: what each term means in plain English, where it shows up, and where to read more.

Structure: term → short definition → example or intuition → where it appears in the courses of this repo.

**Navigation:**
- [ML basics](#-ml-basics)
- [Data and feature engineering](#-data-and-feature-engineering)
- [Metrics and validation](#-metrics-and-validation)
- [Classical ML algorithms](#-classical-ml-algorithms)
- [Neural networks and Deep Learning](#-neural-networks-and-deep-learning)
- [Architectures and layers](#-architectures-and-layers)
- [Transformers and attention](#-transformers-and-attention)
- [LLMs and language model training](#-llms-and-language-model-training)
- [RAG and retrieval](#-rag-and-retrieval)
- [Agents and tool use](#-agents-and-tool-use)
- [Generative AI and multimodality](#-generative-ai-and-multimodality)
- [Fine-tuning and efficiency](#-fine-tuning-and-efficiency)
- [MLOps and production](#-mlops-and-production)
- [Infrastructure and inference](#-infrastructure-and-inference)
- [A/B testing and causal inference](#-ab-testing-and-causal-inference)
- [LLM security](#-llm-security)
- [Careers and roles](#-careers-and-roles)

---

## 🧱 ML basics

**Machine Learning (ML)** — building models that learn from data and make predictions on new inputs. The opposite of writing explicit rules by hand. See [data-science/13-ml-canvas.md](./data-science/13-ml-canvas.md).

**Supervised learning** — the model learns from pairs "input → correct answer". The most common setup (classification, regression). Example: predict apartment price from features.

**Unsupervised learning** — the model finds structure in data without labels. Clustering, dimensionality reduction, anomaly detection. Example: segment customers without predefined groups.

**Self-supervised learning** — the model creates its own task from unlabeled data (predict the next word, restore a masked region). The foundation of pre-training for modern LLMs. See [neural-networks/17-self-supervised.md](./neural-networks/17-self-supervised.md).

**Reinforcement learning (RL)** — an agent learns through interaction with an environment and rewards. Applications: robotics, games, RLHF for LLMs.

**Inductive bias** — assumptions about data structure baked into the model. Convolution assumes locality; attention assumes global relations. Without the right bias, models learn slower or worse.

**Generalization** — how well the model performs on data it has not seen during training. The main goal of ML.

**Overfitting** — the model "memorized" the training set and fails on test. Symptom: low train loss, high val loss.

**Underfitting** — the model is too simple to capture the patterns. Both train and val loss are bad.

**Bias-variance tradeoff** — a fundamental compromise: a too-simple model has high bias (systematic error); a too-complex one has high variance (dependence on the random sample).

**Curse of dimensionality** — as the number of features grows, the volume of the space grows exponentially and data becomes sparse. kNN breaks first, trees suffer less.

---

## 📊 Data and feature engineering

**Feature** — an input variable to the model. For example, user age, text length, pixel RGB value.

**Label / Target** — what the model predicts. "Will buy / won't buy", "price", "image class".

**Feature engineering** — creating new features from raw data. Often gives a bigger quality boost than swapping models. See [data-science/08-feature-engineering.md](./data-science/08-feature-engineering.md).

**One-hot encoding** — encoding a category as a vector of 0s and 1s. "NYC" → [1,0,0], "SF" → [0,1,0]. Simple but blows up dimensionality.

**Target encoding** — replacing a category with the mean target for that category. Strong feature, but prone to leakage without proper CV.

**Embedding** — a numerical representation of an entity (word, image, user, product) as a dense vector. Semantically close entities have close vectors.

**Normalization / Scaling** — bringing features to a common scale (usually [0,1] or zero mean, unit std). Critical for linear models, kNN, and neural networks.

**Data leakage** — information from the test set or the future leaks into training. The model shows inflated quality and breaks in production. The most common cause of "a model that worked in a notebook".

**Data drift** — the distribution of input data changes over time. The model degrades even though it hasn't changed. Treated with monitoring (PSI, KS-test) and retraining.

**Concept drift** — the relationship between features and target changes. Only treated by retraining on fresh data.

**Imbalanced data** — one class is much rarer than the other (fraud: 99.9% non-fraud, 0.1% fraud). Accuracy is useless — use precision/recall, class weights, resampling.

**Train / Validation / Test split** — splitting the dataset. Train for fitting, val for hyperparameter tuning, test for final evaluation (touch it once).

**Stratified split** — split that preserves class proportions. Mandatory under imbalance.

**Time-based split** — for time series: train = past, test = future. Random split here is a guaranteed leak.

**Group split** — when multiple records belong to one entity (user, document). All records of one group must end up in the same split.

---

## 📏 Metrics and validation

**Accuracy** — the fraction of correct predictions. Simple but misleading under imbalance.

**Precision** — of those the model labeled positive, how many actually are. Important when false positives are costly (spam filter: better to let spam through than kill an important email).

**Recall** — of all real positives, how many the model found. Important when false negatives are costly (medicine: better to be safe).

**F1-score** — harmonic mean of precision and recall. A universal metric under imbalance.

**ROC-AUC** — area under the ROC curve across thresholds. Shows class separability independently of threshold.

**PR-AUC** — area under the precision-recall curve. Better than ROC-AUC under strong imbalance.

**MAE / RMSE / MAPE** — regression metrics: mean absolute error, root mean squared error, mean absolute percentage error.

**R² (coefficient of determination)** — share of target variance explained by the model. Ranges from -∞ to 1.

**Cross-validation** — split data into K folds, train K times, average the metric. Reduces dependence on a random split.

**K-Fold CV** — standard variant: K parts, each one becomes the test set in turn.

**Stratified K-Fold** — K-Fold preserving class proportions.

**TimeSeriesSplit** — CV for time series: train grows, test is always in the future.

**Nested CV** — double-nested CV: outer loop for evaluation, inner loop for hyperparameter selection. Protects from hyperparameter leakage.

**Calibration** — how well predicted probabilities match real frequencies. A model can be accurate yet "overconfident". Treated with Platt scaling or isotonic regression.

**Confusion matrix** — a TP/FP/TN/FN table. The base for all classification metrics.

---

## 🌲 Classical ML algorithms

**Linear Regression** — y = Wx + b. The foundation: interpretable, fast, intuitive.

**Logistic Regression** — linear regression + sigmoid → classification. Despite "logistic" in the name, it is a classification model.

**Ridge / Lasso / Elastic Net** — linear regression with L2 / L1 / combined regularization. Lasso zeroes out insignificant coefficients (feature selection).

**Decision Tree** — a sequence of if-else rules learned from data. Interpretable, prone to overfitting.

**Random Forest** — an ensemble of trees on bagging subsamples and random feature subsets. Averaging reduces variance.

**Gradient Boosting** — sequential training of weak models, each correcting the errors of the previous. The best choice on tabular data in 2026.

**XGBoost** — an optimized gradient boosting implementation. The benchmark of speed and quality.

**LightGBM** — Microsoft's boosting with histogram-based splits. Faster than XGBoost on large datasets.

**CatBoost** — boosting with native categorical feature support. Requires less feature engineering.

**kNN (k-nearest neighbors)** — prediction = the answer of the closest neighbors in feature space. Simple but slow, suffers from dimensionality.

**K-Means** — clustering: K centroids, iterative assignment. Sensitive to scale and initialization.

**DBSCAN** — density-based clustering. Finds clusters of arbitrary shape, marks outliers.

**PCA (Principal Component Analysis)** — linear dimensionality reduction via SVD. Preserves maximum variance.

**t-SNE / UMAP** — nonlinear dimensionality reduction for visualization. UMAP is faster and preserves global structure better.

**SVM (Support Vector Machines)** — finding a hyperplane with maximum margin. Was popular before DL, rarely used on large data today.

**Naive Bayes** — Bayes-theorem classifier with feature independence assumption. A simple text baseline.

---

## 🧠 Neural networks and Deep Learning

**Neural Network** — a composition of linear transformations and nonlinearities. Essentially, a large parameterized function.

**Neuron** — the basic unit: y = activation(Wx + b).

**Activation function** — the nonlinearity between layers. Without it, the network is just one big linear regression.

**ReLU** — max(0, x). The standard in hidden layers. Fast and simple, but "dies" for negative inputs.

**GELU** — a smoothed ReLU. Used in transformers. Slightly better quality, slightly slower.

**Sigmoid** — 1/(1+e^-x). Squashes into (0,1). Outdated in hidden layers (vanishing gradients), used in the output of binary classification.

**Softmax** — turns a vector into a probability distribution. The standard at the output of multi-class classification.

**Loss function** — what we minimize. MSE for regression, cross-entropy for classification.

**Cross-entropy** — the standard loss for classification. Penalizes confident wrong predictions more harshly.

**Backpropagation** — algorithm for computing gradients via the chain rule. The heart of neural network training.

**Gradient Descent** — updating weights in the direction opposite to the gradient. The base of all optimizers.

**SGD (Stochastic Gradient Descent)** — GD on a random mini-batch. Noisy but memory-cheap.

**Adam / AdamW** — modern optimizers with adaptive learning rate and momentum. AdamW handles weight decay correctly.

**Learning rate (LR)** — step size for updates. The main hyperparameter. Too large → does not converge; too small → trains forever.

**Learning rate schedule** — a plan for changing LR during training. Warmup + cosine decay is the standard for transformers.

**Warmup** — a gradual LR increase at the start. Stabilizes transformer training.

**Batch size** — how many examples per step. Affects speed, memory, and quality.

**Epoch** — one full pass over the dataset.

**Gradient clipping** — clipping gradients by norm. Protects from exploding gradients in RNNs and transformers.

**Vanishing / Exploding gradients** — gradients shrink or explode in deep networks. Solved by ReLU, batch norm, residual connections, gradient clipping.

**Dropout** — randomly zeroing neurons during training. Regularization against overfitting.

**Batch Normalization** — normalizing activations per batch. Speeds up CNN training.

**Layer Normalization** — normalizing across features within one sample. Used in transformers (batch norm works poorly with variable-length sequences).

**Weight decay** — L2 regularization in neural networks. Pulls weights toward zero.

**Early stopping** — stop training when val loss stops dropping. A defense against overfitting.

**Data augmentation** — artificially expanding the dataset via transformations (rotation, crop, flip for images; synonyms, back-translation for text).

---

## 🏗️ Architectures and layers

**MLP (Multi-Layer Perceptron)** — a fully connected network of several layers. A universal approximator, but it does not exploit data structure.

**CNN (Convolutional Neural Network)** — a convolutional network. Exploits locality and shift-invariance. The standard for images before the ViT era.

**Convolution** — operation: a kernel (filter) slides over the input, computing a dot product at each position. Detects local patterns.

**Pooling** — dimensionality reduction via max or average over a window. Reduces resolution, increases invariance.

**Stride** — the step of the convolution kernel.

**Padding** — adding zeros around the edges to preserve size.

**Receptive field** — the input region influencing one output neuron. Grows with depth.

**Residual connection (skip connection)** — adding the input of a layer to its output. Solves vanishing gradients, allows training networks with >100 layers (ResNet).

**RNN (Recurrent Neural Network)** — processes a sequence step by step, passing a hidden state. Suffers from vanishing gradients on long sequences.

**LSTM (Long Short-Term Memory)** — an RNN with gating. Remembers information across long distances.

**GRU** — a simplified LSTM. Fewer parameters, similar quality.

**Encoder-Decoder** — "input → representation → output" architecture. The base of machine translation before transformers.

**ResNet** — a deep CNN with residual connections. One of the most influential DL architectures.

**EfficientNet** — a CNN family with balanced depth/width/resolution scaling.

**ViT (Vision Transformer)** — a transformer for images. The picture is sliced into patches and processed as a sequence of tokens.

---

## 🔄 Transformers and attention

**Transformer** — an architecture based on self-attention without recurrence. The foundation of all modern LLMs. See [neural-networks/09-transformer.md](./neural-networks/09-transformer.md).

**Attention** — a weighting mechanism: each element decides which other elements to look at and how strongly.

**Self-attention** — attention within one sequence: each token attends to all the others (including itself).

**Query, Key, Value (Q, K, V)** — three projections of the input in attention. Q "asks", K "responds to the query", V is content. Weights = softmax(QK^T / √d).

**Scaled dot-product attention** — formula: Attention(Q,K,V) = softmax(QK^T / √d_k) V. Dividing by √d_k stabilizes gradients.

**Multi-head attention (MHA)** — parallel attention heads with different Q/K/V projections. Lets the model attend to different aspects.

**MQA (Multi-Query Attention)** — one K and V shared across all heads. Saves memory at inference at a small quality cost.

**GQA (Grouped-Query Attention)** — a compromise between MHA and MQA: groups of heads share K/V. The standard in modern LLMs (Llama 3, Mistral).

**Positional encoding** — encoding token position. Without it, the transformer is invariant to permutation.

**Sinusoidal positional encoding** — original sinusoidal functions from "Attention Is All You Need".

**RoPE (Rotary Position Embedding)** — the modern standard. Encodes position via rotation of Q and K. Extrapolates well to long contexts.

**ALiBi** — a linear bias added to attention weights by position. Cheap, good for extrapolation.

**YaRN** — a method to extend a model's context window by modifying RoPE.

**Causal mask** — a mask forbidding attention to future tokens. Used in decoder-only models (GPT).

**KV-cache** — caching the Key/Value tensors between generated tokens. Saves compute by tens of times during autoregressive generation.

**FlashAttention** — an IO-aware implementation of attention. Minimizes HBM accesses, 2-4x faster than naive softmax(QK^T)V.

**PagedAttention** — managing the KV-cache like virtual memory (pages). The basis of vLLM, multiplies throughput.

**Encoder-only** — a transformer made of encoders only (BERT). Good for classification, NER, embeddings.

**Decoder-only** — a transformer made of decoders only (GPT). The standard for generation.

**Encoder-Decoder** — both components (T5, BART). Good for seq2seq tasks (translation, summarization).

**Context window** — the maximum number of tokens the model can process. 8K, 32K, 128K, 1M+ — growing every year.

---

## 🤖 LLMs and language model training

**LLM (Large Language Model)** — a large language model. Technically — a transformer with billions of parameters trained on a huge text corpus.

**Tokenization** — splitting text into tokens (chunks). The model works with tokens, not words.

**Token** — a unit of processing. Usually 3-4 characters or a sub-word. "understanding" → ["under", "stand", "ing"].

**BPE (Byte-Pair Encoding)** — algorithm for building a vocabulary: iteratively merging the most frequent character pairs. Used in GPT.

**WordPiece** — Google's BPE variant. Used in BERT.

**SentencePiece** — Google's tokenizer; works with raw text without pre-tokenization. Used in Llama, T5.

**tiktoken** — OpenAI's fast BPE tokenizer. Used in GPT models.

**Vocabulary** — the set of all tokens. Usually 30K-200K.

**Pre-training** — training the model on a huge corpus via next-token prediction (or MLM for BERT). The most expensive stage (millions of dollars).

**SFT (Supervised Fine-Tuning)** — fine-tuning on "instruction → answer" pairs. Turns "a model that read the internet" into "a model that answers questions".

**RLHF (Reinforcement Learning from Human Feedback)** — training via human ranking of answers + PPO. Made ChatGPT "polite".

**Reward model** — a model that predicts which answer humans would prefer. A component of the RLHF pipeline.

**PPO (Proximal Policy Optimization)** — the RL algorithm typically used in RLHF.

**DPO (Direct Preference Optimization)** — a modern replacement for RLHF. No reward model needed; trains directly on preferred/rejected pairs. Simpler, cheaper, often better.

**KTO (Kahneman-Tversky Optimization)** — an alternative to DPO that works on binary good/bad answers instead of pairs.

**GRPO** — a group extension of PPO used in DeepSeek-R1 for reasoning models.

**Constitutional AI (CAI)** — Anthropic's approach: use AI feedback guided by a set of principles ("constitution") instead of human feedback.

**RLAIF (RL from AI Feedback)** — RLHF where feedback is provided by another model rather than humans.

**Scaling laws** — empirical laws relating quality to parameters, data, and compute. Chinchilla showed the optimal ratio.

**Chinchilla law** — for compute-optimal training, parameters and tokens should be roughly proportional (~20 tokens per parameter).

**Temperature** — sampling parameter controlling "creativity". T=0 — deterministic, T=1 — standard, T>1 — more randomness.

**Top-k sampling** — sample from the k most likely tokens.

**Top-p (nucleus) sampling** — sample from the smallest set of tokens whose probability sums to ≥ p.

**Greedy decoding** — always pick the most likely token. Deterministic but boring.

**Beam search** — keep top-k hypotheses in parallel. Better for machine translation, worse for free-form generation.

**Speculative decoding** — a small model drafts, a large one verifies. Speeds up inference 2-3x without quality loss.

**Continuous batching** — dynamically combining requests into one batch at the token level. The heart of vLLM.

**Hallucination** — the LLM confidently makes things up. Mitigated by RAG, low temperature, evals, structured outputs.

**Sycophancy** — the model bends to the user's stated opinion. A side effect of RLHF.

**Mode collapse** — after RLHF the model produces uniform answers and loses diversity.

---

## 📚 RAG and retrieval

**RAG (Retrieval-Augmented Generation)** — LLM + search over your documents. The model answers using retrieved context.

**Chunking** — splitting documents into chunks for indexing. From 200 to 2000 tokens, usually with overlap.

**Overlap** — the overlap between adjacent chunks. 10-20% is a compromise between completeness and duplicates.

**Vector database** — a database for storing and searching embedding vectors. Qdrant, Weaviate, pgvector, Pinecone, Milvus, Chroma.

**FAISS** — Meta's library for fast nearest-neighbor search. Powers many vector DBs.

**HNSW** — an approximate nearest-neighbor (ANN) algorithm on graphs. The standard in modern vector DBs.

**ANN (Approximate Nearest Neighbors)** — approximate NN search. Sacrifices accuracy for speed.

**Cosine similarity** — closeness measure for vectors: cos(θ) = (a·b) / (|a|·|b|). The standard for embeddings.

**Recall@k** — fraction of relevant documents in top-k retrieval results.

**MRR (Mean Reciprocal Rank)** — average reciprocal position of the first relevant document.

**NDCG (Normalized Discounted Cumulative Gain)** — a ranking metric that accounts for position and graded relevance.

**BM25** — the classic keyword search algorithm. Good for rare words, weak on synonyms.

**Hybrid search** — combining vector search and BM25. Often +20% quality vs. vector alone.

**RRF (Reciprocal Rank Fusion)** — a simple way to merge rankings from several sources via reciprocal ranks.

**Reranking** — a second pass with a more accurate (but slower) model over top-k. A cross-encoder usually gives +15-25%.

**Cross-encoder** — a model that encodes a (query, doc) pair jointly. More accurate than bi-encoder, but slower.

**Bi-encoder** — query and doc are encoded separately. Faster and indexable. Used for retrieval.

**HyDE (Hypothetical Document Embeddings)** — the LLM generates an "ideal answer" whose embedding is used for retrieval. Improves question retrieval.

**Query rewriting** — rewriting the query with an LLM before search. Helps with short or unclear queries.

**Multi-hop retrieval** — retrieval in several steps: the answer to an intermediate question feeds the next query.

**RAGAS** — an eval framework for RAG: faithfulness, answer relevancy, context precision/recall.

**Self-RAG** — the model decides on its own whether retrieval is needed.

---

## 🛠️ Agents and tool use

**Agent (AI agent)** — an LLM in a "think → act → observe" loop, with access to tools and memory.

**Tool use / function calling** — the LLM returns JSON describing a function call. The host application executes it and returns the result.

**ReAct (Reason + Act)** — a pattern in which the model alternates between reasoning (Thought) and actions (Action). Simple and often effective.

**Toolformer** — self-supervised learning of tool use by an LLM.

**Reflexion** — the agent analyzes its mistakes and stores "lessons" in memory.

**Chain-of-Thought (CoT)** — the model writes out a chain of reasoning before answering. Sharply improves math and logic.

**Tree of Thoughts (ToT)** — parallel exploration of several reasoning chains with backtracking.

**MCP (Model Context Protocol)** — Anthropic's standard for connecting tools and context to an LLM. Already supported by OpenAI, Cursor, many IDEs.

**LangChain** — a framework for building LLM applications. Chains, agents, retrieval.

**LangGraph** — a state-machine framework for agents from the same authors. More flexible than LangChain.

**LlamaIndex** — a framework focused on RAG.

**DSPy** — a framework where prompts are compiled and automatically optimized.

**Multi-agent system** — several LLMs working together. Often overkill, sometimes justified (research, debate).

**CrewAI / AutoGen** — multi-agent frameworks.

**Computer Use** — an agent that drives a computer via screenshots and input emulation. Claude Computer Use, OpenAI Operator.

**Browser agent** — an agent that operates a browser. Browser Use, Playwright + LLM.

---

## 🎨 Generative AI and multimodality

**Generative AI** — models that generate new content (text, images, video, audio).

**Diffusion model** — a model that generates by gradually "denoising" a random starting tensor. The base of Stable Diffusion. See [neural-networks/14-diffusion.md](./neural-networks/14-diffusion.md).

**DDPM (Denoising Diffusion Probabilistic Models)** — the original paper on diffusion models.

**DDIM** — accelerated sampling for diffusion (10-50 steps instead of 1000).

**Latent Diffusion** — diffusion in a VAE latent space. The base of Stable Diffusion: compute-cheap.

**Flow Matching / Rectified Flow** — a modern alternative to diffusion. Used in Flux, Stable Diffusion 3.

**DiT (Diffusion Transformer)** — diffusion on a transformer instead of a U-Net. Used in Sora.

**Classifier-Free Guidance (CFG)** — a technique that amplifies the prompt's influence on generation. Parameter: guidance scale.

**ControlNet** — adding structural control to diffusion (pose, contour, depth map).

**IP-Adapter** — image prompt: use an image as a prompt.

**VLM (Vision-Language Model)** — a model working with text and images. CLIP, BLIP, LLaVA, Qwen-VL.

**CLIP** — a model that learns a joint embedding space for text and images. The base for retrieval and conditional generation.

**LLaVA** — an open-source VLM: vision encoder + projector + LLM.

**Whisper** — OpenAI's open-source ASR model. Supports 100+ languages.

**TTS (Text-to-Speech)** — speech synthesis. ElevenLabs, OpenAI TTS, Coqui.

**Voice cloning** — cloning a voice from a short sample.

---

## 🔧 Fine-tuning and efficiency

**Fine-tuning** — continuing training of a pre-trained model on new data.

**Full fine-tuning** — all parameters are updated. Expensive and memory-hungry.

**PEFT (Parameter-Efficient Fine-Tuning)** — training only a small share of parameters. LoRA, prefix tuning, adapters.

**LoRA (Low-Rank Adaptation)** — adding low-rank "adapters" to weights and training only them. Saves memory by tens of times.

**QLoRA** — LoRA on a quantized (4-bit) model. Lets you fine-tune a 70B model on one 24GB GPU.

**Adapters** — small modules between layers. An alternative to LoRA.

**Prefix tuning** — training "virtual tokens" prepended to the input.

**Prompt tuning** — training the prompt's embeddings without modifying the model.

**Quantization** — switching from fp32/fp16 to int8/int4. Compresses the model 2-8x.

**PTQ (Post-Training Quantization)** — quantize after training. Simple, sometimes loses quality.

**QAT (Quantization-Aware Training)** — account for quantization during training. Higher quality, more expensive.

**GPTQ / AWQ** — 4-bit quantization methods for LLMs. Preserve most of the quality.

**GGUF** — a quantized model format for llama.cpp. Convenient for CPU and Apple Silicon.

**Bitsandbytes** — a library for 8/4-bit quantization in PyTorch.

**Knowledge distillation** — training a small "student" model on the predictions of a large "teacher".

**Pruning** — removing low-importance parameters. Sparsity accelerates inference on specialized hardware.

**MoE (Mixture of Experts)** — for each token, only a subset of "experts" is activated. Mixtral, DeepSeek.

**Speculative decoding** — see the LLM section.

**Continuous batching** — see the LLM section.

---

## ⚙️ MLOps and production

**MLOps** — the infrastructure and processes around ML: tracking, versioning, deployment, monitoring.

**Pipeline** — a chain of steps: data → preprocessing → training → eval → deployment.

**Experiment tracking** — logging parameters, metrics, artifacts. MLflow, Weights & Biases, Neptune.

**Model Registry** — a store of model versions with metadata. MLflow Registry.

**Model versioning** — versioning models with links to code and data.

**Data versioning** — versioning data. DVC, lakeFS, Delta Lake.

**Feature Store** — a unified feature storage with identical logic for train and serve. Feast, Tecton.

**Reproducibility** — the ability to repeat a result given the same data and code. Seed everything.

**Inference** — using a trained model to make predictions.

**Online inference** — real-time prediction per request.

**Batch inference** — mass offline prediction.

**Model serving** — deploying a model as a service. FastAPI, BentoML, Triton, TorchServe.

**Canary deployment** — rolling out a new version on a small fraction of traffic.

**Shadow deployment** — the new model receives real traffic but its answers are not used. Compared with production.

**Champion-Challenger** — a champion model in production, challenger models compete with it.

**Blue-Green deployment** — instant switch between two versions.

**Monitoring** — tracking model health: quality, latency, errors, drift.

**PSI (Population Stability Index)** — a metric for detecting distribution drift.

**KS-test** — the Kolmogorov-Smirnov test for comparing distributions.

**Evidently AI** — an open-source library for ML monitoring.

**Retraining strategy** — a plan for retraining: by schedule / trigger / metric degradation.

**SLA / SLO / SLI** — service-level agreements: targets and measurements.

**Observability** — the ability to understand what is happening inside a system via logs, metrics, and traces.

**OpenTelemetry** — a standard for tracing and metrics.

**Distributed tracing** — tracking a request through a chain of microservices.

---

## 🖥️ Infrastructure and inference

**Docker** — containerization: packaging an app with all its dependencies.

**Kubernetes (K8s)** — a container orchestrator. Manages deployments, scaling, and recovery.

**Helm** — a package manager for Kubernetes.

**Terraform** — Infrastructure as Code: describing infrastructure declaratively.

**CI/CD** — Continuous Integration / Continuous Deployment. Automating tests and deploys. GitHub Actions, GitLab CI.

**GPU (Graphics Processing Unit)** — a massively parallel processor. The standard for training neural networks.

**CUDA** — NVIDIA's platform for GPU computing.

**TPU (Tensor Processing Unit)** — Google's specialized ML chips.

**Mixed precision** — training in fp16/bf16 instead of fp32. 2-3x faster, saves memory.

**Gradient checkpointing** — recompute activations during backward instead of storing them. Saves memory at the cost of time.

**Gradient accumulation** — accumulating gradients over several micro-batches before one optimizer step. Emulates a large batch under memory limits.

**DDP (Distributed Data Parallel)** — the standard way to train in parallel in PyTorch: each GPU holds a copy of the model and gradients are synced.

**FSDP (Fully Sharded Data Parallel)** — the model is sharded across GPUs. Lets you train models that do not fit on one GPU.

**DeepSpeed** — Microsoft's distributed training library. ZeRO optimizations.

**vLLM** — the top LLM inference server. PagedAttention, continuous batching.

**TGI (Text Generation Inference)** — Hugging Face's inference server.

**SGLang** — a modern server with more aggressive optimization.

**TensorRT-LLM** — NVIDIA's accelerated inference.

**llama.cpp** — C++ LLM inference on CPU and any GPU. The standard for on-prem and edge.

**Ollama** — a wrapper over llama.cpp for easy local model running.

**ONNX** — an open model format for framework interop.

**ONNX Runtime** — a runtime for ONNX models.

**Triton Inference Server** — NVIDIA's inference server for any model.

**BentoML / Ray Serve** — Python frameworks for deploying models.

**Edge inference** — inference on device (phone, IoT). CoreML, TFLite, MLX.

---

## 📈 A/B testing and causal inference

**A/B test** — a randomized comparison of two (or more) variants. The gold standard for evaluating changes.

**Control group / Treatment group** — control and treatment groups.

**Hypothesis** — H0 (null) vs. H1 (alternative). We test whether to reject H0.

**p-value** — the probability of observing the data (or something more extreme) under H0. Small p → reject H0.

**Statistical significance** — typically threshold p < 0.05.

**Type I error** — false positive: "found an effect that is not there". Controlled by α.

**Type II error** — false negative: "missed an effect that is there". Controlled by power.

**Power** — 1 - β. The probability of detecting an effect when it exists. Usually targeted at 80%.

**MDE (Minimum Detectable Effect)** — the smallest effect a test can detect at a given power.

**Sample size calculation** — calculating the required sample size.

**Confidence interval** — a range that contains the true value with probability X%.

**Bootstrap** — estimating distributions via resampling with replacement.

**SRM (Sample Ratio Mismatch)** — a discrepancy between the actual split and the expected one. A sign of a bug in the splitter.

**Multiple testing problem** — when many hypotheses are tested, the false-positive rate grows. Treated with Bonferroni / Benjamini-Hochberg corrections.

**CUPED** — a technique that reduces variance in A/B tests via covariates (e.g., a pre-period metric).

**Novelty effect** — a temporary effect from a change's novelty. Skews first-week results.

**Causal inference** — discovering cause-effect relationships from data.

**Confounding** — variables that influence both the treatment and the outcome. Create spurious correlations.

**Propensity score matching** — pairing objects from treatment and control with similar characteristics.

**Difference-in-Differences (DiD)** — comparing changes in treatment vs. control groups before and after.

**Instrumental variables** — variables that affect the outcome only through the treatment. Help with confounding.

**Uplift modeling** — modeling the individual treatment effect. "Who exactly will benefit?"

---

## 🛡️ LLM security

**Prompt injection** — an attack where a user injects instructions into a prompt to bypass system rules.

**Indirect prompt injection** — injection via third-party sources (documents, web pages, emails) that the model reads.

**Jailbreak** — bypassing a model's safety filters with cunning prompts.

**DAN (Do Anything Now)** — the classic jailbreak prompt.

**GCG (Greedy Coordinate Gradient)** — an automated attack on LLMs via gradient optimization.

**Many-shot jailbreak** — an attack using many examples in a long context.

**Data exfiltration** — extracting confidential data from a model via clever queries.

**PII leakage** — leakage of personal data (names, phones, emails).

**Model stealing** — reconstructing a model via mass queries.

**Membership inference** — determining whether a specific example was in the training set.

**Guardrails** — input/output filters around an LLM. NeMo Guardrails, Guardrails AI, Llama Guard.

**Red-teaming** — deliberate attacks on your own system to find vulnerabilities.

**OWASP Top-10 for LLM** — a catalog of common LLM application vulnerabilities.

**Constitutional AI** — see above; Anthropic's alignment-via-principles approach.

**Sandboxing** — running agent tools in an isolated environment.

**Rate limiting** — request-rate caps to defend against abuse.

**Content filtering** — filtering inappropriate content on input/output.

---

## 💼 Careers and roles

**Data Scientist (DS)** — hypotheses, A/B, statistics, business metrics. Less code, more communication.

**Machine Learning Engineer (MLE)** — pipelines, inference, latency, reliability. Closer to backend.

**MLOps / Platform Engineer** — infrastructure for the ML team. Kubernetes, observability, CI/CD for models.

**Research Engineer** — implementing papers, experimenting with architectures. A bridge between research and production.

**Research Scientist** — publishing papers, PhD-level. Top labs: Anthropic, OpenAI, DeepMind, Meta FAIR.

**LLM / GenAI Engineer** — a new role. Prompts, RAG, agents, fine-tuning. The hottest in 2024-2026.

**Applied AI Engineer** — embedding AI features into a product. A hybrid of product + ML + backend.

**AI Safety Researcher** — red-teaming, evaluation, interpretability.

**Data Engineer (DE)** — data pipelines, DWH, ETL. ML is impossible without them.

**Analytics Engineer** — a bridge between DE and DS: data modeling, dbt, metrics.

**T-shape** — broad knowledge plus one deep specialty. The standard pattern for seniors.

**Tech Lead** — the technical leader of a team. Not necessarily a manager.

**Staff Engineer** — a level above senior. Architecture, impact across several teams.

**Principal Engineer** — top-tier IC (Individual Contributor) track. Impact at company / industry scale.

**IC track / Manager track** — two career tracks: individual contributor vs. manager.

---

## 🔗 Additional resources

- [Main repository README](./README.md) — the overall learning map.
- [math-for-ml/](./math-for-ml/README.md) — the math behind every term in this glossary.
- [neural-networks/](./neural-networks/README.md) — a deeper dive into architectures.
- [data-science/](./data-science/README.md) — applied DS and MLOps.
- [llm-engineering/](./llm-engineering/README.md) — the LLM stack in depth.
- [claude-code/](./claude-code/README.md) — working with the developer agent.
- [interview-prep/](./interview-prep/README.md) — interview preparation.

---

> 💡 The glossary is a living document. If you encounter a term that is missing — open an issue or PR. The goal is to cover 95% of the vocabulary that comes up in ML interviews and technical discussions.
