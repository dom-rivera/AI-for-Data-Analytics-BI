# Chapter 2 · An Introduction to GPT Models

**Part 1 — Activate** · Instructor: Janani Ravi · [← Previous chapter](01-introduction-to-generative-ai.md) · [Back to contents](../README.md) · [Next chapter →](03-artificial-intelligence-and-machine-learning.md)

---

## At a glance

- **GPT = Generative Pre-trained Transformer.** It's a *series* of large language models from OpenAI, not a single model.
- **ChatGPT** is the *chatbot application*. GPT is the *model* behind it.
- GPT models are **foundation models**: trained on broad data at scale, then adapted to many tasks.
- They are built on the **transformer** (2017, *Attention Is All You Need*), whose key idea is **self-attention**.
- GPTs are **decoder-only** transformers, trained to **predict the next word**.
- To make them useful, models are **aligned** through **supervised fine-tuning (SFT)**, **reinforcement learning from human feedback (RLHF)**, and **in-context learning** (prompting).
- **Prompt engineering** improves your *prompts*. **Prompt tuning** trains a small "soft prompt" to adapt the *model* to a task.

---

## 1. What is GPT?

**ChatGPT** is an AI chatbot developed by OpenAI. The name often refers to the whole system: the application, the model behind it, and the user interface. The model behind ChatGPT has been trained and fine-tuned for **conversation**. It's optimized for human-like chat responses and stays coherent over long contexts.

### Quick refresher: generative vs. discriminative

- **Traditional (discriminative) models** learn the boundary between classes, or predict a target variable from features.
- **Generative models** learn the underlying distribution of the data, then use it to create new samples that are similar to, but not the same as, the training data.

### What each letter in GPT means

| Letter | Meaning |
|---|---|
| **G — Generative** | It can generate coherent, relevant text from a prompt. Used for writing help, content creation, summarization, and conversational agents. |
| **P — Pre-trained** | It's first trained on a very large body of text from the web, then fine-tuned for specific tasks. This gives it wide knowledge of language, styles, and information. |
| **T — Transformer** | The neural network architecture it uses. Transformers rely on **self-attention** to weigh the importance of different words, which helps them understand context and nuance. |

- **GPT is a series**, not a single model: GPT, GPT-2, GPT-3, and later versions. Each one grew in size and capability.
- It's used for text generation, translation, summarization, and more.
- Other companies and research groups build similar models, though they may not use the GPT name.
- GPTs are a type of **large language model (LLM)** and a prominent framework for generative AI.

### Large language models (LLMs)

- They handle many language tasks: text generation, semantic analysis, summarization, text extraction, and more.
- They show **task flexibility**: they can do many language tasks *without task-specific training*.
- They are **large** in two ways:
  - **Parameters:** billions (or even trillions) of weights, adjusted during training to capture the subtleties of language
  - **Training data:** billions of records covering literature, websites, and scientific articles

The breakthrough came with the **transformer**, introduced in the **2017** paper ***Attention Is All You Need***. Today's GPT models are essentially all transformers.

### Three categories of transformer models

| Type | How it's pre-trained | Natural uses |
|---|---|---|
| **Auto-encoding** | Input tokens are corrupted, and the model reconstructs the original sentence | Sentence or token classification |
| **Autoregressive** | Predict the next token, given all previous tokens | **Text generation**. **GPT is autoregressive.** |
| **Sequence-to-sequence** | Takes an input sequence and produces an output sequence | Translation, summarization, question answering |

All of them use **attention** to focus on the right parts of the input.

---

## 2. Foundation models and the GPT-n series

### GPT vs. ChatGPT

| | GPT | ChatGPT |
|---|---|---|
| **What it is** | A type of LLM, and a whole **series** (GPT-1, 2, 3, 4 and beyond) | A **chatbot** developed by OpenAI, powered by a GPT model |
| **Training** | Pre-trained on large-scale data; can be fine-tuned or used generally | Uses a GPT variant with extra training for conversation, including **RLHF**, safeguards, and modifications for interactive use (in mostly undisclosed ways) |
| **Role** | The "brain" | The interface: a chat-optimized UI plus extra **content filters** |

The name "ChatGPT" = **Chat**bot (the interface) + **GPT** (the model).

### The GPT-n series

- The "n" is the **version number**.
- All versions share the same foundation: **generative**, built on the **pre-trained transformer** architecture (using **self-attention**), and trained on **large-scale data**.
- Each version grew much larger in parameters, giving better performance. Better architecture and training also improved **generalization**, reducing the need for task-specific data.

| Model | Released | Parameters | Training data | Notes |
|---|---|---|---|---|
| **GPT-1** | 2018 | 117 million | ~4.5 GB: **BookCorpus** (~7,000 unpublished books) | Mainly a **proof of concept** that transformers work for language tasks (translation, Q&A, summarization). Used pre-training + supervised fine-tuning. **Flaws:** repetitive text, couldn't reason in conversation, couldn't track long-term context. |
| **GPT-2** | 2019 | 1.5 billion | 40 GB: **WebText** (8 million documents from 45 million webpages upvoted on Reddit) | Similar architecture with a few changes. Much more coherent over longer passages. Capable of **zero-shot learning**. Used **pre-training only**, no fine-tuning. **Flaw:** struggled with complex reasoning and context. |
| **GPT-3** | 2020 (the course says June 2020) | 175 billion | 45 TB: **Common Crawl**, WebText, English Wikipedia, two book corpora | Massive scale-up, same core architecture. Made available through an **API**. Could write code and create art, with little or no task-specific training. Three variants: **Babbage, Curie, DaVinci**. **Flaw:** often biased, inaccurate, or inappropriate responses. |
| **Codex** | July 2021 | — | Fine-tuned on code from GitHub | A task-specific GPT-3 variant for **programming** |
| **Instruction-tuned GPT-3** | March 2022 | — | — | First GPT-3 fine-tuned for **following instructions**. Built on further with RLHF. |
| **GPT-3.5** | — | 175 billion | — | Iterative improvements on GPT-3. A variant powered **ChatGPT at launch (November 2022)**. |
| **GPT-4** | March 14, 2023 | Undisclosed (estimated ~1.7 trillion; also given as 1.75 trillion in the course) | Undisclosed (no peer-reviewed paper, citing competition) | **Multimodal** (text and images). Tuned with RLHF. Uses **mixture of experts**: splitting a large model into smaller submodels to improve training. Available through ChatGPT's premium version and OpenAI's API. Aims to address bias, ethics, and accuracy. |

### Foundation models (overview)

**Foundation models** are AI models trained on **broad data at scale** so they can be adapted to a wide range of downstream tasks, even ones they weren't explicitly trained for.
- They embody **transfer learning**: knowledge from pre-training carries over to new but related tasks.
- All GPT-n models are foundation models.
- **Others mentioned:**
  - Google's **PaLM** (Pathways Language Model), comparable to GPT-3
  - Meta's **LLaMA** (Large Language Model Meta AI)

**Multimodal AI** can understand, process, and generate information across several data types, not just text: images, video, audio, and more.

---

## 3. Attention

Natural language is **sequential**: word order carries meaning, and a single word can flip it.

> "This is the worst restaurant by far" vs. "This is **not** the worst restaurant by far."

### How RNNs handled language (before transformers)

In the early 2010s, the best language models used **recurrent neural networks (RNNs)**.
- They take input **one timestep at a time**, feeding each output back in as the next input. This captures time dependencies.
- **Translation example ("I ate a yummy meal" → "Ich habe eine leckere Mahlzeit gegessen"):**
  1. The input is tokenized, vectorized, and fed in word by word.
  2. The whole input is captured as a **single vector representation**.
  3. Output is generated word by word. Each new word uses the full input plus all words predicted so far.

**RNN drawbacks:**
1. **Long sequences:** One representation for the whole input works for short text but breaks down for long text. Special memory cells such as **LSTM** (long short-term memory) and **GRU** (gated recurrent unit) help, but still do poorly on very long sequences.
2. **No parallelism:** Processing is sequential, so training can't be parallelized. RNNs are hard to train and slow to converge.

### What attention does

**Attention** lets the network **focus on specific parts of the input while ignoring others**. It computes interactions between *all pairs of positions*, so it captures **long-range dependencies** regardless of how far apart words are.

**In the translation example:**
- To predict *Ich*, focus on "I".
- To translate "yummy", focus on "yummy".
- To predict *gegessen*, focus on several words: "I", "ate", and "meal".

It doesn't have to be one-to-one, and the relevant words change at each step. Translation models with attention work **orders of magnitude better**, and attention improves all NLP tasks, not just translation.

### Self-attention

Attention existed before transformers, but transformers introduced it in a new way: **self-attention**. For every word in a sentence, the model computes scores for how much focus to put on **every other word** when representing the current word. This is what made transformers groundbreaking.

---

## 4. The transformer architecture

The transformer was introduced by **Vaswani et al.** in **2017**. It:
- Relies **only on attention**, with **no recurrent or convolutional layers**
- Uses **self-attention**, so each word is contextualized by every other word in the sequence, regardless of distance
- Processes whole sequences **in parallel**, unlike RNNs, making it faster and suited to large datasets

### High-level structure: encoder + decoder

- The **encoder** creates an abstract, highly contextualized representation of the input.
- The **decoder** uses that representation to generate the output (e.g. "I am a manager" → "Je suis directeur").

Depending on the task, you can use both parts or just one:

| Setup | Used by |
|---|---|
| **Encoder + decoder** | Sequence-to-sequence tasks like translation (the original 2017 transformer) |
| **Encoder only** | Auto-encoding models (good at extracting information for classification and regression) |
| **Decoder only** | Autoregressive models (text generation). **This is GPT.** |

### Building blocks (as walked through in the course)

**1. Input embedding + positional encoding** (in both encoder and decoder)
- Models only understand numbers, so text becomes vectors.
- **Word embeddings** are dense vectors that capture a word's **meaning** and its relationships to other words. They start random and are **learned during training**. With enough data, related words like *woman, queen, girl* cluster together.
- **Positional encoding** adds each word's **position** in the sequence, including relative position (which comes first and how far apart words are). Transformers don't process words in order, so this is what makes **parallel processing** possible.
- The two vectors have the same dimension and are **added together** into one vector per word. The model can still separate the two kinds of information. All word vectors are stacked into a matrix and fed in.

**2. Multi-head attention** (the core layer)
- It's a correlation and contextualization mechanism: each word interacts with the others to build a matrix representing the meaning of the whole input.
- Four broad steps:
  1. **Create queries, keys, and values.** Each word's embedding goes through **three separate dense networks**. Their parameters are learned during training to make attention work as well as possible.
  2. **Split into multiple heads.** Queries, keys, and values are divided into chunks, one per attention head (the number of heads is configurable). Each head sees part of every word, so it can attend to the sequence for **different reasons**.
  3. **Attention in each head:**
     - **Queries** represent the data whose relevance to other data we're measuring.
     - **Keys** are what queries are compared against.
     - **Query · Key (dot product)** gives an **attention matrix**: for each word, the relative importance of every other word.
     - That matrix is **multiplied by the values** (the actual data to aggregate). The output is the same size as the input.
  4. **Combine the heads' outputs** into one abstract representation that captures the nuances and dependencies in the text.

**3. Add & norm** (in both encoder and decoder)
- **Skip connections** feed earlier data back in, so the output doesn't drift from the original input.
- **Normalization** scales outputs into a smaller range. This stabilizes training, makes it less sensitive to hyperparameters and starting weights, and often speeds up convergence.

**4. Feed forward**
- A projection that reshapes the attention output into a form useful for the next stage (the decoder).

**Decoder-specific blocks**
- **Multi-head attention (encoder–decoder):** The **keys and values come from the encoder**, and the **query comes from the decoder**. This lets each decoder position attend to all of the input.
- **Masked multi-head attention:** During training the decoder can see the whole output sequence, which would let it "cheat" by looking at future words. A **mask** hides everything after the current position: to predict word *n+1*, it can only see words up to *n*.
  - In **decoder-only text generators**, all not-yet-processed tokens are masked.
  - In models like **BERT**, masking is **random**, so attention can use tokens on both sides.
  - Masking lets all positions train **in parallel**, a major improvement over RNNs.
- At the very end come **Linear** and **Softmax** layers, which produce **output probabilities**.

---

## 5. Inside the GPT model

GPT uses a transformer with self-attention, pre-trained to **predict the next word**, then fine-tuned on smaller task-specific datasets.

**Encoder vs. decoder roles:**
- **Encoders** extract information from input and map it to continuous representations of meaning and context.
- **Decoders** generate text step by step, predicting the next word using attention on previously generated words and on the input.
- **GPT is decoder-only**, because its job is text generation.

### Four key concepts behind GPT

1. **Decoder-only architecture**
2. **Unsupervised (self-supervised) pre-training** on unlabeled text
3. **Supervised fine-tuning** on a smaller labeled dataset for a specific task
4. **Task-specific input transformation:** formatting the input text to fit the task. The GPT authors chose to format tasks *textually* instead of adding task-specific components to the model.

### GPT-1's architecture (as shown in the course)

Text & position embedding → masked multi-head self-attention → layer norm → feed forward → layer norm → outputs to **text prediction** and **task classifier**.
- **Text & position embed** produces **learned word embeddings** (meaning) and **learned positional encodings** (order), combined into one vector per word.
- **Masked multi-head self-attention** combines every word with every other word to learn their relationships.
- **Normalization** keeps values in a reasonable range for better training.
- The decoder is **several stacked blocks**, not one.

### How GPT generates text

GPT is trained on the **language modeling objective**: predict the next word given all previous words. The model learns the **probabilities of word sequences**.
- Each generated word is **fed back into the input** to predict the next one, and so on. In principle this can produce very long sequences.

### Pre-training vs. fine-tuning

| Stage | What happens | Result |
|---|---|---|
| **Pre-training** | An untrained LLM learns from a huge corpus of **unlabeled** text by predicting the next word | An LLM that **understands text**: broad knowledge, but not useful for a specific task on its own |
| **Supervised fine-tuning** | Further training on a **labeled**, task-specific dataset (e.g. lots of code) | An LLM adapted to a task (e.g. **one that generates code**) |

**Self-supervised learning:** Pre-training is often called "unsupervised", but it's really **self-supervised**. Labels are created programmatically from the data itself. *Example:* mask the last word of a sentence and train the model to predict it.

| Learning type | Labels |
|---|---|
| Supervised | Labels provided |
| Unsupervised | No labels at all |
| Self-supervised | Labels **generated programmatically** from the data |

**Why fine-tune?** The model must be **aligned with what the user wants**: classification, answering questions, and so on. SFT uses curated prompts with expected responses, effectively a labeled dataset, and adjusts the model's weights to predict those outputs.

**In-context learning:** GPTs are powerful in-context learners. Context given in the prompt helps them respond better. Task-specific input transformation can mean formatting training data for tasks like question answering or text similarity.

---

## 6. Understanding foundation models

**Foundation models** are pre-trained on vast data (often from the internet) using **self-supervision at scale**, then adapted to many downstream tasks.

**Characteristics:**
- **Pre-trained on massive, diverse datasets** with significant computing resources
- **General, not specialized.** Traditional models do one task, like image classification. A foundation model can translate, answer questions, write creatively, and more.
- **Adaptable** to specific tasks and domains through **prompting and fine-tuning**, with minimal extra training
- **Large** in both parameters and training data, which drives their power
- **Self-supervised**: they learn to predict or fill in parts of the data (the next word, a masked blank)
- **Often multimodal**: text, numbers, code, images, video, speech, structured data, and machine signals
- Usable for **both generative and discriminative tasks**: they can be tuned for regression or classification, or generate text, images, video, audio, and speech

**Example:** ChatGPT uses a GPT foundation model (3.5 or 4), further fine-tuned to follow instructions using **SFT** and **RLHF**. Thanks to this extra tuning, ChatGPT had **higher accuracy, less toxic sentiment, and better alignment with user needs** than the foundation models alone.

### Emergence

**Emergence** is when complex, often unexpected abilities appear as a model's scale or complexity grows.
- *Example:* A model trained only to predict the next word turns out to answer questions, classify, and summarize.
- These abilities are **not directly predictable** from the system's individual parts. New behaviors can appear in larger models that weren't visible in smaller ones.
- *Example (GPT-3):* writing fiction, composing music, and generating code, without being explicitly trained for them.
- **Upside:** highly capable, versatile systems. **Downside:** behavior is harder to predict and control, raising questions of reliability and ethics.

---

## 7. Model alignment

A foundation model is broad and general, so you usually can't use it directly for a specific application. *Example:* a customer support chatbot built on a raw foundation model may not be as polite as you want.

**Model alignment** is making a model's behavior, decisions, and outputs match **human values, intentions, ethical principles**, and any task-specific goals.

| Type | Meaning |
|---|---|
| **Goal alignment** | The model's objectives match its intended use: it understands and properly answers user requests (answering questions, generating text, helping with decisions) |
| **Value alignment** | Outputs reflect human values and ethics, avoiding harmful, biased, or offensive content. This is hard because values differ across cultures, people, and contexts. |

On its own, a pre-trained LLM tends to give **repetitive, not very helpful** results, even though the knowledge is in there.

### Steps in building an LLM

1. **Pre-training** (self-supervised; creates the foundation model)
2. **Alignment**, in three steps:
   1. **Supervised fine-tuning (SFT)**
   2. **Reinforcement learning from human feedback (RLHF)**
   3. **In-context learning** (examples or instructions in your prompt when using the model; this is where prompt engineering comes in)

### Step 1: Supervised fine-tuning (SFT)

**How it works:**
1. Start with a pre-trained foundation model.
2. **Humans curate** a dataset of high-quality example responses showing the correct output for given inputs.
3. Fine-tune the model, adjusting its weights to predict those responses.

- It's "supervised" because it uses traditional supervised learning on labeled examples.
- The model learns to **replicate the style** of the examples.
- It's best where it's clear what a correct output looks like.
- It's similar to pre-training (same next-word objective). The difference is **curated, high-quality data**.

**Examples from the course:**
- **A dataset from a Meta research paper:**
  - Prompt: a poem to help remember the first 10 elements of the periodic table → the expected poem
  - Prompt: a request to be roasted with swearing → the model should **decline**
- **Explaining to a child:** "Explain reinforcement learning to a 6-year-old" → a simple analogy
- **Customer service:**
  - User: "I can't log into my account. What should I do?"
  - Pre-trained model (blunt): "Try resetting your password using the 'Forget password' option."
  - After SFT with polite examples: "I'm sorry to hear you're having trouble logging in…", followed by a gentle suggestion to try the password reset

**SFT vs. generic fine-tuning:**
- **Generic fine-tuning** teaches a model to solve a specific task. It becomes more of a specialist and may **lose general abilities**.
- **SFT** teaches a correct *style, behavior, or kind of response*, so the model **keeps its general problem-solving ability**.

### Step 2: Reinforcement learning from human feedback (RLHF)

SFT shows the model what kind of response is wanted, and its style and tone. But it doesn't tell the model **how good or bad** a given response is. RLHF fills that gap.

**Reinforcement learning basics:** An **agent** learns to make decisions by interacting with an **environment**, aiming to **maximize cumulative rewards** through trial and error.

| Term | General meaning | In an LLM |
|---|---|---|
| **Agent** | The learner and decision-maker (like a robot exploring unfamiliar terrain) | The model |
| **Environment** | Everything the agent interacts with and learns from | The users interacting with the model |
| **State (Sₜ)** | The current context at time *t* | The conversation so far |
| **Action (Aₜ)** | The agent's decision, which changes the environment | The text the model generates |
| **Reward (Rₜ)** | Feedback on the action: large, small, or negative (a penalty) | A thumbs up (reward) or thumbs down (penalty) |

The agent updates its internal **policy** to earn more reward over time. The LLM learns to produce responses that collect more "thumbs up".

**How RLHF works:**
1. **Human labelers rank** possible responses to prompts (best, second best, terrible, …) across a reasonably large dataset.
2. A **reward model** is trained on these human evaluations to score each prompt–response pair (e.g. 1, 4, 5, or 10 points).
3. The base model is **fine-tuned with a reinforcement learning algorithm** using those rewards, in an iterative feedback loop.

The algorithm commonly used is **proximal policy optimization (PPO)**.
- It adjusts the model's parameters to maximize the rewards predicted by the reward model.
- It optimizes the model's **policy** (how it makes decisions).
- "**Proximal**" means each update stays in a **small region close to the previous version**, changing the model only slightly each time.

**Example:** For "Explain reinforcement learning to a 6-year-old", labelers rank four reasonable answers (e.g. D > C > A > B). The model is rewarded based on which one it picks, and PPO pushes it toward the higher-ranked style.

---

## 8. Prompt engineering vs. prompt tuning

**Prompt engineering** is structuring text so a generative model can interpret it, to get the best response from a model that has already been pre-trained, fine-tuned, and aligned.

**Example prompts:**
- Explain Einstein's theory of relativity in simple terms to a 5th grader.
- Write code in Python to compute the average of numbers in a list.
- Write a short, humorous poem about how programming is fun.

### Why prompting matters

- It gets output that is **immediately useful**, and improves **quality and diversity**.
  - *Instructor's tip:* When generating fictitious names, she explicitly asks for names from different countries.
- It gives **more control**, better **interpretability**, and helps **reduce bias** inherited from training data.
- It helps limit **hallucinations** by asking the model to **cite correct sources**.
- It lets you experiment with different data types and ways of presenting data.
- **Goal setting** in the prompt shows what "good" looks like. *Example:* "I'm looking for a three-sentence overview of how black holes work so that I can understand this intuitively" (this removes jargon).
- It improves **safety** and helps defend against **prompt hacking**.

### Challenges

- Getting the result **on the first try** (often needs back-and-forth)
- Knowing **where to start** on complex problems
- **Bias**, especially implicit bias you may not notice
- Responses that are **boring or narrow**. *Example:* when choosing technology for a software solution, give plenty of context.
- **Interpretability**: models work well, but you often don't know why, which is a problem when answers are wrong or half-baked
- Balancing **precision and creativity**: stick to facts, but present them vividly

**Every word matters:** "Describe the Taj Mahal" vs. "Describe the history of the Taj Mahal".

### Anatomy of a prompt

| Component | Description | Example from the course |
|---|---|---|
| **Instruction** *(required)* | The core directive | "Extract keywords from this text." / "Summarize this newspaper article." |
| **Context** | Background that frames the response | "Considering that I have just a week's vacation, do you think it makes sense to [go to] Europe?" |
| **Input data** | The data to process (paragraph, numbers, a word) | The text you want summarized |
| **Output format** | The form of the response | A list of student names in **JSON** |

### Techniques

**Basic:**
- **Role playing:** "As a mathematician, please explain the intuition behind the Black-Scholes formula."
- **Iterative refinement:** Start broad, then narrow it down.
- **Adding constraints:** e.g. "Use simple language, don't use jargon." **Positive constraints work better**: "Do use simple language", not "Do not use complex language".
- **Use the model's outputs** to shape your next prompt.

**Advanced:**
- **Zero-shot:** A task with no examples, testing generalization.
- **Few-shot:** A few examples to guide the model. *Example:* "These are the kinds of books I like to read. Please recommend some other books like these to me."
- **Chain-of-thought:** Guide the model through intermediate reasoning steps.
- **Generated / augmented knowledge:** The model first generates relevant facts, then completes the prompt, giving higher-quality answers.

### Prompt tuning

| | Prompt engineering | Prompt tuning |
|---|---|---|
| **Goal** | Get the best response by **crafting better prompts** | **Improve the model** for a specific task |
| **How** | Refine the wording and structure of prompts | Train a small set of extra parameters, a **soft prompt**, on a task-specific dataset |
| **Changes the model?** | No | Doesn't alter the underlying pre-trained model. May tune a subset of parameters tied to the prompt. |
| **Cost** | — | **Far less resource-intensive** than full fine-tuning |

Prompt tuning can involve adding keywords, phrases, or structured instructions the model learned to respond to. It adapts a large model to a task with few extra parameters while keeping the base model flexible.

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **GPT** | Generative Pre-trained Transformer: OpenAI's series of decoder-only LLMs |
| **ChatGPT** | OpenAI's chatbot (interface + filters) powered by a conversation-tuned GPT variant |
| **Foundation model** | A model trained on broad data at scale, adaptable to many downstream tasks |
| **Transfer learning** | Reusing knowledge from pre-training for a different but related task |
| **Autoregressive** | Predicts the next token from all previous tokens (GPT) |
| **Self-attention** | Each word gets weighted scores for every other word in the same sequence |
| **Query / Key / Value** | Three learned representations of each word used to compute attention |
| **Multi-head attention** | Attention split across several heads, each attending for different reasons |
| **Positional encoding** | A vector that tells the model where each word sits in the sequence |
| **Masking** | Hiding future tokens during training so the decoder can't "cheat" |
| **Self-supervised learning** | Training with labels generated programmatically from the data |
| **Emergence** | Unexpected abilities appearing as model scale grows |
| **Model alignment** | Making a model's outputs match human goals and values |
| **SFT** | Supervised fine-tuning on curated, human-written example responses |
| **RLHF** | Reinforcement learning from human feedback, using a reward model built from human rankings |
| **PPO** | Proximal policy optimization: the RL algorithm often used in RLHF; makes small, bounded updates |
| **Mixture of experts** | Dividing a large model into smaller submodels to improve training (used by GPT-4, per the course) |
| **Prompt tuning / soft prompt** | Training a small set of extra parameters to adapt a model to a task without changing the base model |

---

*Source: course transcript "An Introduction to GPT Models" (12 videos). Model details, dates, and figures are given as stated in the course.*

[← Previous chapter](01-introduction-to-generative-ai.md) · [Back to contents](../README.md) · [Next chapter →](03-artificial-intelligence-and-machine-learning.md)
