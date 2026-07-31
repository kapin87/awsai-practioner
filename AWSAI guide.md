# AWS Certified AI Practitioner (AIF-C01)

## How to use this document

Read this in three passes:

1. **Section A** — what's changed and what to unlearn. Do this first, or you'll revise confidently in the wrong direction.
2. **Sections B–F** — the five domains, in exam weighting order.
3. **Sections G–I** — mapping table, scenarios with answers, and a final checklist.

Topics marked **🆕** are in the current syllabus but were absent from the original notes.

\---

## Exam facts at a glance

|Item|Detail|
|-|-|
|Exam code|AIF-C01|
|Level|Foundational|
|Questions|65 total — 50 scored, 15 unscored trial items|
|Time|90 minutes|
|Passing score|700 out of 100–1,000 (scaled, compensatory)|
|Cost|USD 100|
|Validity|3 years|
|Delivery|Pearson VUE test centre or online proctored|
|Question types|Multiple choice, multiple response, ordering, matching|

**Compensatory scoring** means you don't need to pass each domain — only the exam overall. Practically: don't panic-optimise a weak 14% domain at the expense of the 28% one.

### Domain weightings

|Domain|Topic|Weight|
|-|-|-|
|1|Fundamentals of AI and ML|20%|
|2|Fundamentals of GenAI|24%|
|3|Applications of Foundation Models|28%|
|4|Guidelines for Responsible AI|14%|
|5|Security, Compliance and Governance for AI Solutions|14%|

Domains 2 and 3 together are **52%** of the exam. Classical ML — the algorithm tables, the hyperparameter definitions — sits inside a 20% slice, and even there it's tested conceptually. This is the single biggest calibration error in most self-made study guides: they over-invest in the ML theory that's comfortable and familiar, and under-invest in generative AI and foundation models, which is where half the marks live.

\---

# Section A — Accuracy audit and what changed from previous version

## A1. Corrections to carry forward

These are places where the original notes are now wrong or misleading, not just incomplete.

|Item in the original notes|Status|What to know instead|
|-|-|-|
|**Amazon GuardDuty** listed under Security|❌ Explicitly **out of scope**|AWS names it in the out-of-scope appendix, alongside Security Hub, WAF, Cognito, Detective and Shield. Threat detection as a *concept* is in scope; GuardDuty as an answer option is a distractor.|
|**Amazon Forecast** = time-series prediction|⚠️ Stale|Forecast has been closed to new customers since July 2024 and is not on the in-scope service list. Time-series forecasting now points to **SageMaker AI / SageMaker Canvas**.|
|**Amazon Mechanical Turk** as a labelling service|⚠️ Not in scope|It's a real service and the concept of crowdsourced human labelling is fine to know, but it isn't on the in-scope list. For labelling, the exam wants **SageMaker Ground Truth**; for human review of predictions, **Amazon A2I**.|
|**"Amazon SageMaker"**|🔄 Renamed|The ML platform is now **Amazon SageMaker AI**. The newer umbrella "Amazon SageMaker" refers to the unified data-and-AI platform. Answer options use the new naming.|
|**Amazon Q Business / Q Developer** as separate services|🔄 Consolidated|The in-scope list simply says **Amazon Q**. The two use cases still exist; treat them as capabilities rather than distinct exam services.|
|**SageMaker Role Manager / Model Dashboard** as key governance features|⚠️ Over-weighted|The objectives name **Model Cards**, **Clarify**, **Model Monitor** and **Bedrock Model Evaluations**. Role Manager is not named anywhere in the current guide.|
|Deep hyperparameter tuning content|⚠️ Over-weighted|"Performing hyperparameter tuning or model optimisation" is listed by AWS as an **out-of-scope job task**. Know what learning rate, epoch and batch size *mean*; don't study tuning strategy.|
|**Amazon MemoryDB** as a vector store|❌ Removed|Dropped from the in-scope list in the April 2026 revision.|

## A2. What the April 2026 revision added 🆕

The guide grew a whole agentic layer. If your material predates this, it is missing:

* **Agentic AI as a first-class term** — now sits alongside AI, ML, deep learning and GenAI in the basic definitions objective.
* **Model Context Protocol (MCP)** — how agents connect to external tools and systems.
* **Multi-agent patterns** — orchestration, communication, memory management, tool use.
* **Amazon Bedrock AgentCore** — including **AgentCore Identity** and **Policy in AgentCore**, which appear in the *security* domain, not just the build domain.
* **Strands Agents** and **Kiro** — added to the in-scope Developer Tools list.
* **Amazon Nova** and **AWS Transform** — added to in-scope Machine Learning services.
* **Amazon Quick** — replaced QuickSight on the in-scope Analytics list.
* **Token-based pricing** as its own objective, with cost and latency implications.
* **Context engineering** as a named concept distinct from prompt engineering.
* **Model distillation** and **prompt caching** as customisation and cost levers.
* **Bedrock Prompt Management** for prompt versioning.
* **LLM-as-a-judge** as an evaluation method.
* **Hallucination detection and grounding** — moved into Domain 5 (security), which is a genuinely counter-intuitive placement worth remembering.
* **Traditional ML vs foundation model** as an explicit selection decision.
* **Asynchronous** and **serverless** inference added to the inference-types list.

\---

# Section B — Domain 1: Fundamentals of AI and ML (20%)

## B1. The nested-doll model

The classic hierarchy still holds, with agentic AI as a newer outer wrapper around how models are *used* rather than how they're built:

```
Artificial Intelligence
 └── Machine Learning
      └── Deep Learning
           └── Generative AI
                └── Agentic AI  (models that plan, call tools, and act)
```

**Analogy.** Think of a bank's operations floor. Traditional ML is the credit scorecard — narrow, auditable, one job. Deep learning is the fraud engine that spots patterns nobody wrote rules for. Generative AI is the analyst who drafts the client letter. Agentic AI is the analyst who also books the meeting, pulls the CRM record and files the note — same brain, but with hands and a to-do list.

## B2. Learning paradigms

|Paradigm|Data it needs|Question it answers|Typical use|
|-|-|-|-|
|Supervised|Labelled|"What is this / how much?"|Churn prediction, credit default, spam|
|Unsupervised|Unlabelled|"What natural groupings exist?"|Customer segmentation, anomaly detection|
|Semi-supervised|Small labelled + large unlabelled|Same as supervised, cheaper|Any domain where labelling is expensive|
|Reinforcement|Reward signal from an environment|"What action should I take next?"|Robotics, game playing, sequential decisions|
|**Self-supervised** 🆕|Raw data, labels derived from the data itself|"Predict the missing piece"|How foundation models are pre-trained|

Self-supervised learning is worth adding because it's the honest answer to "how was the LLM trained without labels?" — the text supplies its own labels by masking or next-token prediction.

## B3. Inference types 🆕

This was missing entirely and is directly named in the objectives.

|Type|Shape of the workload|Rough mental picture|
|-|-|-|
|**Real-time**|Persistent endpoint, low latency, steady traffic|A teller window that stays open|
|**Batch**|Large volume, no latency requirement, scheduled|Overnight statement run|
|**Asynchronous**|Large payloads or long processing, queued, near-real-time|Drop it in the in-tray, collect later|
|**Serverless**|Intermittent or unpredictable traffic, scales to zero|A window that opens only when someone walks up|

Exam signal: *"unpredictable, spiky traffic and we don't want to pay for idle"* → serverless inference. *"Millions of records, results needed by morning"* → batch. *"Large documents, processing takes minutes"* → asynchronous.

## B4. Data types 🆕

Structured vs unstructured, labelled vs unlabelled, tabular, time-series, image, text, audio. Simple but frequently the hinge of a question: an answer that requires labelled data is wrong if the scenario says the data is unlabelled.

## B5. When AI/ML is the wrong answer 🆕

AWS explicitly tests the negative case. ML is a poor fit when:

* The rule is deterministic and known — a tax calculation doesn't need a model.
* You need a **guaranteed, exact outcome**, not a probabilistic one.
* The cost of building and maintaining the model exceeds the value.
* There isn't enough representative data.
* Full explainability is legally mandated and only a black-box model would perform.

## B6. Traditional ML vs foundation models 🆕

A new objective. The decision rule:

|Choose traditional ML when|Choose a foundation model when|
|-|-|
|You need explainability for regulators|The task is language, image or content generation|
|The task is narrow and well-defined|The task is broad, varied or open-ended|
|You have good labelled data|You have little or no labelled data|
|Latency and cost per prediction must be minimal|Time to market matters more than per-call cost|
|The output must be a stable, auditable number|The output is text, summary or conversation|

## B7. ML lifecycle and MLOps 🆕

Pipeline stages: **data collection → EDA → pre-processing → feature engineering → training → tuning → evaluation → deployment → monitoring → retraining.**

MLOps is DevOps applied to models, with one extra headache: the code can stay identical while the world underneath it changes. That's **model drift** (the relationship between inputs and outputs shifts) and **data drift** (the input distribution shifts). Hence monitoring and retraining are lifecycle stages, not afterthoughts.

Supporting services: **SageMaker Data Wrangler** (prep), **Feature Store** (reusable features), **Model Monitor** (drift and quality in production), **SageMaker Pipelines** (orchestration), **Model Registry** (versioning).

## B8. Evaluation metrics

**Classification** — accuracy, precision, recall, F1, AUC-ROC.

The distinction that gets tested:

* **Precision** — of everything I flagged, how much was right? Optimise when **false positives are costly** (blocking legitimate transactions).
* **Recall** — of everything I should have caught, how much did I catch? Optimise when **false negatives are costly** (missing a fraud case or a disease).
* **F1** — the balance of the two; the default when classes are imbalanced.
* **AUC-ROC** — how well the model separates classes across all thresholds.

**Regression** — MAE, MSE, RMSE. RMSE punishes large errors hardest.

**Business metrics** 🆕 — cost per user, development cost, customer feedback, ROI. AWS deliberately tests that a technically excellent model with no business return is a failed project.

Still true, and still worth repeating: **accuracy alone is meaningless on imbalanced data.** A model that predicts "not fraud" every time is 99.9% accurate and completely useless.

\---

# Section C — Domain 2: Fundamentals of GenAI (24%)

## C1. Core vocabulary

|Term|Plain meaning|
|-|-|
|Token|The chunk of text a model actually processes — roughly ¾ of a word in English|
|Chunking 🆕|Splitting source documents into retrievable pieces before embedding them|
|Embedding|A numeric vector capturing meaning, so similarity becomes measurable distance|
|Vector|The stored form of that embedding|
|Context window|The total tokens a model can hold in view at once — prompt plus response|
|Transformer|The architecture behind modern LLMs; attention lets it weigh all tokens against each other|
|Diffusion model 🆕|Generates images by iteratively denoising random noise|
|Multi-modal model 🆕|Accepts and/or produces more than one modality — text, image, audio, video|

**Analogy for embeddings.** Think of a filing system where documents are placed on a map by meaning rather than alphabetically. "Mortgage arrears" and "loan delinquency" land next to each other even though they share no words. Retrieval becomes "who are my nearest neighbours?"

## C2. The foundation model lifecycle

```
Data selection → Model selection → Pre-training → Fine-tuning
      → Evaluation → Deployment → Feedback (→ loop back)
```

Note that this is a distinct lifecycle from the ML pipeline in Domain 1. Questions sometimes test whether you can tell them apart.

## C3. Token-based pricing 🆕

You pay for **input tokens plus output tokens**. Consequences the exam cares about:

* Long prompts and long documents in context are a direct, recurring cost — this is a real argument for RAG over stuffing everything into the prompt.
* Verbose outputs cost money; setting max output length is a cost control.
* **Prompt caching** reuses a repeated prompt prefix across calls, cutting both cost and latency.
* **Provisioned throughput** buys reserved capacity at a fixed rate — right for predictable high volume, wasteful for spiky workloads. On-demand is the reverse.
* Smaller models cost less per token and respond faster; **model distillation** is how you get a small model to imitate a large one's behaviour on a narrow task.

## C4. Context engineering 🆕

Prompt engineering is how you word the instruction. **Context engineering is what you put in the window and in what order** — retrieved documents, conversation history, tool outputs, system instructions.

**Analogy.** Prompt engineering is asking a good question. Context engineering is deciding which files to put on the desk before you ask it, in what order, and which ones to remove because they're stale.

Why it matters: context windows are finite and cost money, models attend unevenly across long contexts, and irrelevant context actively degrades answers.

## C5. Agentic AI 🆕

An **agent** is a foundation model given a goal, a set of tools, and the ability to loop: reason → act → observe → repeat, until the goal is met.

|Concept|What it is|
|-|-|
|Tool use|The model calls APIs or functions rather than answering from memory|
|**Model Context Protocol (MCP)**|An open standard for connecting agents to external tools and data sources — one integration contract instead of bespoke glue per system|
|Memory management|Short-term (this session) and long-term (across sessions) state|
|Orchestration|Breaking a goal into steps and sequencing them|
|Multi-agent patterns|Specialist agents coordinated by a supervisor/router, or collaborating peers|

**Analogy.** A single agent is one capable contractor. A multi-agent system is a builder, a sparky and a plumber with a site manager sequencing them. MCP is the standardised plug socket they all use, so nobody has to rewire the house per trade.

## C6. Advantages and limitations

**Strengths** — adaptability across tasks, conversational interaction, content generation, fast time to value, low barrier to entry.

**Weaknesses** — hallucination, non-determinism (same prompt, different answer), limited interpretability, factual staleness, cost at scale, prompt-injection exposure.

**Business value metrics** 🆕 — ROI, conversion rate, efficiency gains, average revenue per user, customer lifetime value, cross-domain performance.

## C7. AWS building blocks for GenAI

|Service|What it's for|
|-|-|
|**Amazon Bedrock**|Managed, serverless access to foundation models from multiple providers via one API. Adds Knowledge Bases (RAG), Agents, Guardrails, Model Evaluation, Prompt Management, Flows, custom model import.|
|**Amazon Bedrock AgentCore** 🆕|Runtime and supporting services for deploying agents at production scale — identity, memory, gateway, observability, sandboxed tool execution.|
|**Amazon Nova** 🆕|AWS's own foundation model family (text/multimodal understanding plus image and video generation).|
|**Amazon SageMaker AI**|Full-lifecycle ML platform: build, train, tune, deploy, monitor.|
|**SageMaker JumpStart**|Model hub of pre-trained and open-source models with one-click deploy and fine-tune.|
|**Amazon Q**|AWS's generative assistant — enterprise knowledge Q\&A over company data, and developer/coding assistance.|
|**Kiro** 🆕|Agentic IDE for spec-driven development.|
|**Strands Agents** 🆕|Open-source SDK for building agents in code.|
|**Amazon Quick** 🆕|AWS's BI and analytics workspace (the evolution of QuickSight), with generative capabilities.|
|**AWS Transform** 🆕|Agentic service for modernising legacy workloads.|
|**PartyRock**|No-code Bedrock playground — useful for experimentation, dropped from the current objective wording.|

**The Bedrock vs SageMaker AI line.** Bedrock = consume and customise someone else's foundation model, no infrastructure. SageMaker AI = build, train and operate your own models, full control. If a scenario says "no ML expertise" or "no infrastructure to manage" → Bedrock. If it says "custom model on proprietary data with full control of training" → SageMaker AI.

\---

# Section D — Domain 3: Applications of Foundation Models (28%)

The heaviest domain. Give it the most time.

## D1. Choosing a model

Selection criteria: cost, modality, latency, language coverage, model size and complexity, customisation options, input/output length limits, and **prompt caching support** 🆕.

## D2. Inference parameters

|Parameter|Effect|When to move it|
|-|-|-|
|**Temperature**|Randomness. Low = deterministic and repetitive; high = varied and creative|Lower it for factual, compliance or extraction tasks|
|**Top-K**|Sample only from the K most likely next tokens|Blunt cap on the candidate pool|
|**Top-P (nucleus)**|Sample from the smallest set of tokens whose probabilities sum to P|More adaptive than Top-K|
|**Max tokens / response length**|Caps output size|Cost and latency control|
|**Stop sequences**|Ends generation on a trigger string|Structured output, formatting control|

Note: none of these change the model's *knowledge* — they change how it samples. Lowering temperature reduces creative drift but does **not** make a model factually correct about things it never learned. That's what grounding is for.

## D3. The customisation ladder — cheapest to most expensive

```
Prompt engineering        (no training, instant, cheapest)
      ↓
RAG                       (no training; adds retrieval infrastructure)
      ↓
Fine-tuning               (training on labelled examples; moderate cost)
      ↓
Continued pre-training    (further training on large unlabelled domain data)
      ↓
Pre-training from scratch (millions of dollars; almost never the answer)
```

Two shortcuts that sit alongside this ladder 🆕:

* **Model distillation** — train a smaller, cheaper model to reproduce a larger model's outputs on your task. Cost and latency win, scope narrows.
* **In-context learning** — few-shot examples in the prompt. Zero training cost, limited by context window.

**The single most common exam decision:** the model doesn't know current or proprietary facts → **RAG**. The model doesn't know your *style, format, tone or domain vocabulary* → **fine-tuning**. Get that distinction wrong and you'll lose several marks.

## D4. RAG

```
User question
   → Embed the question
   → Search the vector store for nearest chunks
   → Inject retrieved chunks into the prompt as context
   → Model generates a grounded answer (ideally with citations)
```

Benefits: current information without retraining, fewer hallucinations, source citation, respects existing document permissions, far cheaper than fine-tuning.

On AWS: **Amazon Bedrock Knowledge Bases** is the managed implementation — it handles chunking, embedding, storage and retrieval.

**Vector store options in scope:** Amazon OpenSearch Service, Amazon Aurora (PostgreSQL with pgvector), Amazon RDS for PostgreSQL, Amazon Neptune, Amazon DocumentDB. *MemoryDB was removed from the in-scope list in April 2026.*

**Kendra vs Knowledge Bases** — Kendra is enterprise intelligent search that returns documents and passages; Bedrock Knowledge Bases wires retrieval into an FM to generate an answer. Both can serve enterprise Q\&A; the phrasing of the desired output usually decides it.

## D5. Prompt engineering

**Constructs:** instruction, context, input data, output indicator, negative prompts (what *not* to do), latent space.

**Techniques:**

|Technique|Description|
|-|-|
|Zero-shot|Instruction only, no examples|
|Single-shot|One example|
|Few-shot|Several examples establishing pattern and format|
|Chain-of-thought|Ask for stepwise reasoning — helps on multi-step logic|
|Role prompting|Assign a persona to shape tone and framing|
|Prompt templates|Parameterised, reusable prompts for consistency at scale|

**Risks — a named objective, and often under-revised:**

|Risk|What it means|
|-|-|
|**Prompt injection**|Malicious instructions hidden in user input or retrieved content hijack the model|
|**Jailbreaking**|Crafted prompts that bypass safety guardrails|
|**Prompt leaking / exposure**|The model reveals its system prompt or confidential context|
|**Poisoning**|Corrupted training or retrieval data steers behaviour|
|**Hijacking**|Redirecting the model away from its intended task|

**Bedrock Prompt Management** 🆕 — version, test, compare and deploy prompts as managed artefacts, rather than hard-coding them in application source.

## D6. Training and fine-tuning

* **Pre-training** — build general capability from massive unlabelled corpora (self-supervised).
* **Continued pre-training** — more unlabelled data, domain-specific, to shift vocabulary and domain fluency.
* **Fine-tuning** — labelled prompt/response pairs to shape behaviour on a task.
* **Instruction tuning** — fine-tuning specifically on instruction-following examples.
* **Transfer learning** — reuse learned representations for an adjacent task.
* **RLHF** — humans rank outputs; those preferences train a reward model that aligns the FM.

**Data preparation for fine-tuning** — curation, governance, sufficient volume, accurate labelling, representativeness and balance. Garbage in, expensively fine-tuned garbage out.

## D7. Evaluating foundation models

|Metric|Best suited to|What it measures|
|-|-|-|
|**ROUGE**|Summarisation|Overlap with reference text, recall-oriented|
|**BLEU**|Translation|Overlap with reference text, precision-oriented|
|**BERTScore**|Semantic similarity|Meaning-level match via embeddings, not exact wording|
|**Perplexity**|Language modelling|How "surprised" the model is by the text|
|**LLM-as-a-judge** 🆕|Open-ended generation|A strong model scores outputs against a rubric|
|**Human-in-the-loop evaluation**|Anything subjective or high-stakes|Human judgement, still the gold standard|

**Amazon Bedrock Model Evaluation** supports both automatic metrics and human evaluation workflows, including LLM-as-a-judge.

**Evaluating applications, not just models** 🆕 — a new objective. A RAG system can fail on retrieval quality even with a perfect model; an agent can fail on tool selection or step sequencing. Evaluate the pipeline end-to-end.

**Business alignment metrics** 🆕 — task completion rate, user satisfaction, cost per interaction, productivity gain, engagement.

\---

# Section E — Domain 4: Guidelines for Responsible AI (14%)

## E1. The dimensions AWS names

Bias · fairness · inclusivity · robustness · safety · veracity · explainability · transparency · privacy · governance · controllability.

## E2. Bias and variance

||Meaning|Symptom|
|-|-|-|
|**High bias → underfitting**|Model too simple to capture the pattern|Poor on training *and* test data|
|**High variance → overfitting**|Model memorised the training data|Excellent on training, poor on new data|

**Analogy.** Underfitting is a graduate who learned one rule and applies it to everything. Overfitting is one who memorised last year's exam paper word-for-word and is lost when the questions change.

Also know **dataset bias** — unrepresentative training data producing systematically worse outcomes for particular demographic groups. Mitigations: balanced and diverse datasets, curated sources, subgroup analysis, label-quality audits, human review.

## E3. Transparency vs explainability

* **Explainability** — can you explain *why this particular prediction* came out this way?
* **Transparency** — is it clear *how the system works and where it's being used*?

They are not the same, and the exam tests the distinction. There is a real **trade-off**: the most interpretable models (linear regression, decision trees) are often less accurate than the least interpretable (deep networks, LLMs). In a regulated context, interpretability may legitimately outrank raw accuracy.

## E4. AWS tools

|Tool|Purpose|
|-|-|
|**Amazon Bedrock Guardrails**|Content filters, denied topics, word filters, PII detection and redaction, and **contextual grounding checks** that flag responses unsupported by source material|
|**SageMaker Clarify**|Bias detection pre- and post-training, plus feature-attribution explainability|
|**SageMaker Model Monitor**|Ongoing monitoring for data quality, drift and bias in production|
|**SageMaker Model Cards**|Documented model purpose, assumptions, risks, intended use, performance|
|**Amazon A2I**|Routes low-confidence or high-stakes predictions to human reviewers|
|**AWS AI Service Cards** 🆕|AWS-published documentation of intended use, limitations and responsible-AI design for its own AI services|

## E5. Legal and ethical risk

Intellectual property infringement in generated output, biased outcomes and discrimination exposure, hallucinated claims presented as fact, loss of customer trust, end-user harm, and privacy breach through training or prompt data. Also named: **environmental and sustainability considerations** when choosing a model — a smaller model that meets the requirement is the responsible choice as well as the cheap one.

## E6. Human-centred design for explainable AI 🆕

User-feedback mechanisms, transparency about when AI is involved in a decision, clear escalation paths to a human, and interfaces that communicate confidence and uncertainty honestly.

\---

# Section F — Domain 5: Security, Compliance and Governance (14%)

## F1. Securing AI systems

|Service|Role|
|-|-|
|**IAM**|Identity, roles, policies, least privilege|
|**AWS KMS**|Encryption key management|
|**Amazon Macie**|Discovers and classifies sensitive data in S3|
|**AWS PrivateLink / VPC endpoints**|Keeps traffic to AWS services off the public internet|
|**AWS Secrets Manager**|Credential and secret storage with rotation|
|**Amazon Bedrock Guardrails**|Runtime input/output safety controls|
|**AgentCore Identity / Policy in AgentCore** 🆕|Identity and authorisation for agents acting on a user's behalf|

**The shared responsibility model** applies here as everywhere: AWS secures the cloud infrastructure and managed service; you secure your data, access control, prompts and outputs.

## F2. AI-specific security concerns 🆕

Beyond conventional cloud security, the current objectives name:

* **Prompt injection** — treat retrieved content and user input as untrusted.
* **Data leakage prevention** — stopping confidential data escaping through prompts or responses.
* **Output filtering and validation** — checking what comes out, not just what goes in.
* **Toxicity** — harmful or offensive generated content.
* **Audit trail and logging for AI interactions** — recording prompts and responses for review.
* **Encryption at rest and in transit** — the baseline.

## F3. Hallucination detection and grounding 🆕

Notably placed in the *security* domain, not the generative AI one:

* **RAG grounding** — anchor answers in retrieved source material.
* **Contextual grounding checks** (Bedrock Guardrails) — automatically flag responses not supported by the provided context.
* **Output validation** — programmatic checks against schemas, rules or known facts.
* **Confidence scoring** — surface uncertainty rather than hiding it.
* **Human review** — A2I for anything consequential.
* **Lower temperature** and **domain-specific data** — supporting levers, not solutions on their own.

## F4. Governance and compliance

|Service|Role|
|-|-|
|**AWS CloudTrail**|API-level audit log — who did what, when|
|**Amazon CloudWatch**|Metrics, logs, alarms|
|**AWS Config**|Resource configuration tracking and compliance rules|
|**Amazon Inspector**|Vulnerability scanning for workloads|
|**AWS Audit Manager**|Automates evidence collection for audits|
|**AWS Artifact**|On-demand access to AWS compliance reports (SOC, ISO, PCI)|
|**AWS Trusted Advisor**|Best-practice checks across cost, security, performance|
|**AWS Well-Architected Tool**|Structured workload review|

**Standards named in the guide:** ISO, SOC, and algorithm accountability laws.

**Generative AI Security Scoping Matrix** 🆕 — AWS's framework for deciding how much security ownership you carry, from Scope 1 (consumer app) through Scope 2 (enterprise app), Scope 3 (building on a pre-trained model via API), Scope 4 (fine-tuned model) to Scope 5 (self-trained model). The further right you go, the more of the security burden is yours.

**Data governance strategies:** data lifecycle, lineage, cataloguing, residency, retention, logging, monitoring.

## F5. Cost management

**AWS Budgets** (set thresholds and alerts) and **AWS Cost Explorer** (analyse spend). Practical levers for AI workloads: right-size the model, cache prompts, cap output length, choose serverless inference for spiky traffic and provisioned throughput only for predictable high volume, and prefer RAG over fine-tuning where it solves the problem.

\---

# Section G — Signal-to-service mapping

Updated, with the stale entries corrected.

|Phrase in the question|Service|
|-|-|
|Access multiple foundation models, no infrastructure|Amazon Bedrock|
|Build, train and deploy custom ML models|Amazon SageMaker AI|
|Pre-built and open-source model hub|SageMaker JumpStart|
|Deploy and operate agents at scale|Amazon Bedrock AgentCore|
|Managed RAG over company documents|Amazon Bedrock Knowledge Bases|
|Enterprise search across company content|Amazon Kendra|
|Assistant over enterprise data, or coding help|Amazon Q|
|Label a training dataset|SageMaker Ground Truth|
|Human review of low-confidence predictions|Amazon A2I|
|Detect bias and explain predictions|SageMaker Clarify|
|Document a model's purpose, risks and intended use|SageMaker Model Cards|
|Monitor a deployed model for drift|SageMaker Model Monitor|
|Block harmful content, redact PII, check grounding|Amazon Bedrock Guardrails|
|Compare foundation models on a task|Amazon Bedrock Model Evaluation|
|Version and manage prompts|Amazon Bedrock Prompt Management|
|Sentiment, entities, key phrases, PII in text|Amazon Comprehend|
|Image and video analysis|Amazon Rekognition|
|OCR — text and tables from scanned documents|Amazon Textract|
|Speech to text|Amazon Transcribe|
|Text to speech|Amazon Polly|
|Language translation|Amazon Translate|
|Conversational bot with intents and slots|Amazon Lex|
|Personalised recommendations|Amazon Personalize|
|Time-series forecasting|SageMaker AI / SageMaker Canvas *(not Forecast — closed to new customers)*|
|Store embeddings for vector search|Amazon OpenSearch Service, Aurora/RDS PostgreSQL, Neptune, DocumentDB|
|Find sensitive data in S3|Amazon Macie|
|Scan workloads for vulnerabilities|Amazon Inspector|
|Audit API activity|AWS CloudTrail|
|Track resource configuration compliance|AWS Config|
|Collect audit evidence|AWS Audit Manager|
|Download AWS compliance reports|AWS Artifact|
|Connect an agent to external tools|Model Context Protocol (MCP)|
|Build agents in code|Strands Agents|
|Agentic IDE|Kiro|
|AWS's own foundation models|Amazon Nova|

\---

# Section H — Scenario practice

Cover the answers and work through them cold. The original set is reworded here, with new scenarios covering the added syllabus.

**1.** A wealth manager wants an internal assistant that answers adviser questions using only the firm's own product and policy documents, with citations. Nothing may be sent for model retraining.

**2.** A hospital requires clinicians to review AI predictions whenever model confidence falls below a threshold.

**3.** A retailer must produce a labelled dataset from two million product photographs.

**4.** A marketing team wants AI-generated product copy using foundation models, with no infrastructure to manage and no ML engineers on staff.

**5.** A support team wants to know whether inbound reviews are positive or negative, at scale.

**6.** Finance needs line items and tables extracted from scanned supplier invoices.

**7.** A security team needs to scan EC2 workloads for known software vulnerabilities.

**8.** A data scientist must formally document a model's intended use, assumptions, risks and known limitations for an internal risk committee.

**9.** A chatbot occasionally states policy terms that don't appear anywhere in the source documents. The team needs this detected automatically before responses reach customers.

**10.** An application sends the same 4,000-token system prompt on every call, and the monthly bill is climbing.

**11.** The model's answers are factually fine but the tone and document format are wrong for the firm's house style. Retrieval is already working well.

**12.** An agent needs to query a CRM, a ticketing system and an internal wiki without a bespoke integration written for each one.

**13.** Traffic to an inference endpoint is unpredictable — sometimes hundreds of requests an hour, sometimes none for days. The team wants to stop paying for idle capacity.

**14.** A compliance officer needs an immutable record of who invoked which model and when.

**15.** A team must decide between a small fine-tuned classifier and a large foundation model for a credit decisioning step that regulators will audit.

\---

### Answers

1. **Amazon Bedrock Knowledge Bases** (RAG on Bedrock). Kendra is defensible if the requirement were document retrieval rather than a generated, cited answer.
2. **Amazon A2I** — human review triggered by low confidence.
3. **SageMaker Ground Truth** — managed data labelling.
4. **Amazon Bedrock** — managed foundation models, serverless.
5. **Amazon Comprehend** — sentiment analysis.
6. **Amazon Textract** — text and table extraction from scanned documents.
7. **Amazon Inspector**. *(GuardDuty is a distractor and is out of scope.)*
8. **SageMaker Model Cards**.
9. **Amazon Bedrock Guardrails**, specifically the contextual grounding check.
10. **Prompt caching** — reuse the cached prefix; also review output length caps.
11. **Fine-tuning**. RAG fixes knowledge gaps; fine-tuning fixes style, format and behaviour.
12. **Model Context Protocol (MCP)** — one standard interface instead of per-system glue.
13. **Serverless inference** — scales to zero, no charge for idle.
14. **AWS CloudTrail**.
15. **The traditional ML model.** Explainability and auditability requirements outweigh the FM's flexibility — this is exactly the new "traditional ML vs FM" objective.

\---

# Section I — Final checklist

Work through this the day before. If any line makes you hesitate, that's your revision list.

**Fundamentals**

* \[ ] Distinguish AI, ML, deep learning, generative AI and agentic AI
* \[ ] Match supervised / unsupervised / reinforcement / self-supervised to a scenario
* \[ ] Choose between batch, real-time, asynchronous and serverless inference
* \[ ] Explain when AI/ML is the *wrong* tool
* \[ ] Decide traditional ML vs foundation model, and justify it
* \[ ] Pick precision vs recall vs F1 for a given cost of error
* \[ ] Name the ML pipeline stages and the AWS service at each

**Generative AI**

* \[ ] Define token, chunking, embedding, vector, context window
* \[ ] Explain token-based pricing and three ways to reduce cost
* \[ ] Distinguish prompt engineering from context engineering
* \[ ] Explain what an agent is, and what MCP does
* \[ ] State the Bedrock vs SageMaker AI decision rule in one sentence

**Foundation models**

* \[ ] Order the customisation ladder by cost
* \[ ] Decide RAG vs fine-tuning from the symptom described
* \[ ] Describe temperature, Top-K, Top-P and their effects
* \[ ] List the in-scope vector stores
* \[ ] Name the prompt-engineering risks, including prompt injection
* \[ ] Match ROUGE, BLEU, BERTScore and LLM-as-a-judge to the right task

**Responsible AI**

* \[ ] Distinguish transparency from explainability
* \[ ] Distinguish overfitting from underfitting
* \[ ] Say what Guardrails, Clarify, Model Monitor, Model Cards and A2I each do
* \[ ] Name three legal risks of generative AI

**Security and governance**

* \[ ] Apply the shared responsibility model to an AI workload
* \[ ] Name four grounding or hallucination-detection techniques
* \[ ] Match CloudTrail, Config, Inspector, Audit Manager, Artifact and Macie to their purpose
* \[ ] Explain the Generative AI Security Scoping Matrix at a high level
* \[ ] Know which security services are explicitly **out** of scope

\---

# Closing note

The exam rewards judgement over recall. Most questions present a plausible business situation with three defensible answers and one *best* one, and the differentiator is usually a single constraint buried in the wording — "no infrastructure to manage", "must be auditable", "unpredictable traffic", "cannot leave our account", "no ML expertise on the team".

So the productive drill isn't reciting what each service does. It's reading a scenario and asking: *what constraint is doing the work here?* Get that habit in place and the service naturally falls out of it.

Good luck.

\---

*Sources: official AWS Certified AI Practitioner (AIF-C01) exam guide, version 1.1, published 30 April 2026, including its published change history and in-scope/out-of-scope service appendices.*

