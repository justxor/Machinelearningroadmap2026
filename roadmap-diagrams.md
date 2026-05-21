# 🗺️ Roadmap diagrams

Visual map of the whole repository. All diagrams use [Mermaid](https://mermaid.js.org/) — GitHub renders them natively.

If you only have 30 seconds, look at **Diagram 1** — it shows the entire learning path on one page.

---

## 1. Repository map: how the courses fit together

```mermaid
flowchart TD
    Start([👋 You are here]) --> Math[📐 math-for-ml<br/>linear algebra, calc, prob]
    Start --> DS[📊 data-science<br/>EDA, A/B, MLOps]

    Math --> NN[🧠 neural-networks<br/>MLP → CNN → Transformer]
    DS --> NN

    NN --> LLM[🤖 llm-engineering<br/>RAG, agents, fine-tune]
    NN --> CV[👁️ computer-vision<br/>detection, ViT, VLM]

    LLM --> Labs[🧪 practice-labs<br/>25 hands-on labs]
    CV --> Labs
    DS --> Labs

    Labs --> Interview[🎤 interview-prep<br/>system design, coding]
    Interview --> Job([💼 Job offer])

    Claude[⚡ claude-code<br/>AI dev agent] -.boost any course.-> NN
    Claude -.boost any course.-> LLM
    Claude -.boost any course.-> CV

    classDef start fill:#22c55e,stroke:#15803d,color:#fff
    classDef finish fill:#3b82f6,stroke:#1d4ed8,color:#fff
    classDef base fill:#fbbf24,stroke:#b45309,color:#000
    classDef advanced fill:#a78bfa,stroke:#6d28d9,color:#fff
    classDef boost fill:#f472b6,stroke:#be185d,color:#fff

    class Start start
    class Job finish
    class Math,DS base
    class NN,LLM,CV,Labs,Interview advanced
    class Claude boost
```

---

## 2. Pick a track (decision tree)

```mermaid
flowchart TD
    Q1{What is your goal?} --> A[Build LLM products<br/>RAG, agents, chatbots]
    Q1 --> B[Classical applied ML<br/>tabular, A/B, forecasts]
    Q1 --> C[Computer Vision<br/>detection, video, OCR]
    Q1 --> D[Research / papers<br/>novel architectures]

    A --> A1[math-for-ml light<br/>→ neural-networks 1–9<br/>→ llm-engineering full<br/>→ labs 11–16]
    B --> B1[data-science full<br/>→ neural-networks 1–5<br/>→ llm-engineering 1–10<br/>→ labs 01–05, 17–20]
    C --> C1[math-for-ml<br/>→ neural-networks full<br/>→ computer-vision full<br/>→ labs 06–10]
    D --> D1[math-for-ml full<br/>→ neural-networks full<br/>→ papers + reimplementations<br/>→ PhD or research role]

    A1 --> Done([4–6 months])
    B1 --> Done2([6–9 months])
    C1 --> Done3([6–9 months])
    D1 --> Done4([9–12+ months])

    classDef q fill:#fbbf24,stroke:#b45309
    classDef track fill:#3b82f6,stroke:#1d4ed8,color:#fff
    classDef path fill:#e5e7eb,stroke:#9ca3af
    classDef finish fill:#22c55e,stroke:#15803d,color:#fff
    class Q1 q
    class A,B,C,D track
    class A1,B1,C1,D1 path
    class Done,Done2,Done3,Done4 finish
```

---

## 3. The neural-networks course at a glance

```mermaid
flowchart LR
    subgraph B1["Block 1 · Fundamentals"]
        L1[01 Perceptron] --> L2[02 MLP + backprop]
        L2 --> L3[03 Activations + init]
        L3 --> L4[04 Regularization]
        L4 --> L5[05 Optimizers]
    end

    subgraph B2["Block 2 · Architectures"]
        L6[06 CNN]
        L7[07 RNN/LSTM]
        L8[08 Attention]
        L9[09 Transformer]
        L6 --> L7 --> L8 --> L9
    end

    subgraph B3["Block 3 · Application"]
        L10[10 Embeddings + tokenization]
        L11[11 Fine-tuning]
        L12[12 Production]
        L10 --> L11 --> L12
    end

    subgraph B4["Block 4 · Advanced"]
        L13[13 ViT + multimodal]
        L14[14 Diffusion]
        L15[15 RLHF / DPO]
        L16[16 GNN]
        L17[17 Self-supervised]
        L18[18 Distributed training]
    end

    L5 --> L6
    L9 --> L10
    L12 --> L13
    L13 --> L14 --> L15 --> L16 --> L17 --> L18
```

---

## 4. LLM application stack (llm-engineering map)

```mermaid
flowchart TB
    User([👤 User]) --> App[App / UI<br/>FastAPI, Streamlit]

    App --> Router{Router}

    Router -->|simple Q| LLM[LLM provider<br/>OpenAI · Anthropic · local]
    Router -->|needs docs| RAG[RAG pipeline]
    Router -->|needs tools| Agent[Agent loop<br/>ReAct · planning]

    RAG --> Embed[Embedding model]
    Embed --> VDB[(Vector DB<br/>Qdrant · pgvector)]
    RAG --> BM25[(BM25 / keyword)]
    VDB --> Rerank[Reranker]
    BM25 --> Rerank
    Rerank --> LLM

    Agent --> Tools[Tools<br/>search · code · DB · MCP]
    Tools --> LLM

    LLM --> Evals[📏 Evals<br/>offline + online]
    LLM --> Monitor[📈 Monitoring<br/>cost · latency · quality]
    LLM --> User

    classDef user fill:#22c55e,stroke:#15803d,color:#fff
    classDef infra fill:#fbbf24,stroke:#b45309
    classDef model fill:#a78bfa,stroke:#6d28d9,color:#fff
    classDef store fill:#3b82f6,stroke:#1d4ed8,color:#fff
    classDef obs fill:#f472b6,stroke:#be185d,color:#fff
    class User user
    class App,Router,Tools infra
    class LLM,Embed,Rerank,Agent,RAG model
    class VDB,BM25 store
    class Evals,Monitor obs
```

---

## 5. RAG sequence: a single user query, step by step

```mermaid
sequenceDiagram
    autonumber
    participant U as User
    participant App as App
    participant Q as Query rewriter
    participant V as Vector DB
    participant B as BM25
    participant R as Reranker
    participant L as LLM
    participant E as Eval logger

    U->>App: question
    App->>Q: rewrite + expand
    Q->>V: dense search
    Q->>B: keyword search
    V-->>R: top-50 dense
    B-->>R: top-50 sparse
    R->>R: cross-encoder rerank
    R-->>App: top-5 chunks
    App->>L: prompt + chunks
    L-->>App: answer + citations
    App->>E: log query, chunks, answer
    App-->>U: final answer
```

---

## 6. Computer-vision production pipeline

```mermaid
flowchart LR
    A[📷 Raw images / video] --> B[Annotation<br/>CVAT · Roboflow]
    B --> C[Aug pipeline<br/>albumentations]
    C --> D[Train<br/>PyTorch + timm/ultralytics]
    D --> E[Eval<br/>mAP · IoU · FiftyOne]
    E -->|good| F[Export<br/>ONNX · TensorRT]
    E -->|bad| C
    F --> G{Deploy target}
    G -->|cloud| H[Triton + FastAPI]
    G -->|edge| I[CoreML · TFLite · Jetson]
    H --> J[📈 Monitoring<br/>drift · latency]
    I --> J
    J -->|drift| B

    classDef data fill:#fbbf24,stroke:#b45309
    classDef train fill:#a78bfa,stroke:#6d28d9,color:#fff
    classDef deploy fill:#3b82f6,stroke:#1d4ed8,color:#fff
    classDef obs fill:#f472b6,stroke:#be185d,color:#fff
    class A,B,C data
    class D,E,F train
    class G,H,I deploy
    class J obs
```

---

## 7. MLOps lifecycle (data-science → production)

```mermaid
flowchart LR
    subgraph Loop["♻️ Continuous loop"]
        direction LR
        Data[📦 Data<br/>collect · clean · version] --> Train[🏋️ Train<br/>experiment · track]
        Train --> Eval[📏 Eval<br/>metrics · slices]
        Eval --> Reg[📚 Model Registry]
        Reg --> Deploy[🚀 Deploy<br/>shadow · canary · A/B]
        Deploy --> Mon[📈 Monitor<br/>quality · drift · cost]
        Mon -->|drift / decay| Data
        Mon -->|stable| Deploy
    end
```

---

## 8. Career path

```mermaid
flowchart TD
    Start([New to ML]) --> Jr[🟢 Junior ML / DS<br/>1 year]
    Jr --> Mid[🟡 Middle ML / DS<br/>2–4 years]

    Mid --> Branch{Choose track}

    Branch --> ICTrack[Individual Contributor]
    Branch --> MgrTrack[People Manager]

    ICTrack --> Sr[🔴 Senior<br/>4–7 years]
    Sr --> Staff[⭐ Staff Engineer<br/>7–10 years]
    Staff --> Principal[👑 Principal / Distinguished]

    MgrTrack --> EM[Engineering Manager]
    EM --> Director[Director of ML]
    Director --> VP[VP / Head of AI]

    Sr -.also possible.-> Specialist[🔬 Domain specialist<br/>CV · NLP · MLOps · Research]

    classDef start fill:#22c55e,stroke:#15803d,color:#fff
    classDef ic fill:#3b82f6,stroke:#1d4ed8,color:#fff
    classDef mgr fill:#f472b6,stroke:#be185d,color:#fff
    classDef spec fill:#a78bfa,stroke:#6d28d9,color:#fff
    class Start start
    class Jr,Mid,Sr,Staff,Principal ic
    class EM,Director,VP mgr
    class Specialist spec
```

---

## 9. Weekly study cadence

```mermaid
gantt
    title One learning week
    dateFormat  YYYY-MM-DD
    section Theory
    New lesson (read + code along)     :a1, 2026-01-05, 2d
    section Practice
    Rewrite from scratch + exercises   :a2, after a1, 2d
    One lab from practice-labs         :a3, after a2, 1d
    section Reflect
    Weekly retrospective               :a4, after a3, 1d
    Rest (genuinely)                   :a5, after a4, 1d
```

---

## 10. Anti-patterns vs healthy patterns

```mermaid
flowchart LR
    subgraph Bad["🚫 Anti-patterns"]
        B1[Watch tutorials<br/>without coding]
        B2[Switch tracks<br/>every 2 weeks]
        B3[Track hours<br/>not artifacts]
        B4[Skip exercises<br/>"I get it already"]
        B5[Notebook-only<br/>no tests, no repo]
    end

    subgraph Good["✅ Healthy patterns"]
        G1[Code every lesson<br/>line by line]
        G2[Pick ONE track<br/>for 6+ weeks]
        G3[3 real projects<br/>on GitHub]
        G4[All exercises<br/>before next lesson]
        G5[Structured repo<br/>README + tests + report]
    end

    B1 --> G1
    B2 --> G2
    B3 --> G3
    B4 --> G4
    B5 --> G5

    classDef bad fill:#fca5a5,stroke:#991b1b
    classDef good fill:#86efac,stroke:#166534
    class B1,B2,B3,B4,B5 bad
    class G1,G2,G3,G4,G5 good
```

---

[← Back to main README](./README.md)
