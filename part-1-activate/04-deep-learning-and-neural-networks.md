# Chapter 4 · Deep Learning and Neural Networks

**Part 1 — Activate** · Instructor: Janani Ravi · [← Previous chapter](03-artificial-intelligence-and-machine-learning.md) · [Back to contents](../README.md) · [Next chapter →](05-getting-started-with-prompt-engineering.md)

---

## At a glance

- **Deep learning models** are built from **neural networks**: learning units called **neurons**, arranged in **layers**. They have no single algorithm, only **architectures**.
- Unlike traditional ML, they **extract features automatically** from raw data, need **huge datasets** and **GPUs**, and are **black boxes**.
- A **neuron** computes **Φ(Wx + b)**: a weighted sum plus bias (linear), passed through an **activation function** (non-linear).
- Networks are trained with **gradient descent**: a **forward pass** → compute the **loss** → compute **gradients** → a **backward pass** to update weights and biases → repeat.
- **CNNs** are for images (convolution + pooling). **RNNs** are for sequences and time series (memory / hidden state).
- **NLP** turns words into numbers (one-hot, count vector, TF-IDF, **word embeddings**). **Attention** and **transformers** power today's LLMs.
- **GANs** generate realistic fake data through a zero-sum game. **Reinforcement learning** (not deep learning) learns by trial and error to maximize rewards.

---

## 1. Understanding deep learning

### Traditional ML vs. deep learning

| | Traditional ML models | Deep learning models |
|---|---|---|
| **How they work** | A specific **algorithm** that fits a line, curve, or tree | **Neural networks**: neurons in layers. No specific algorithm, only **architectures** (number of layers, neurons per layer, how they're connected) |
| **Raw data** | Can't train on raw data. Need heavy preprocessing and **manual feature extraction** by the developer. | Often work **directly on raw data** with **automatic feature extraction**, learning to ignore irrelevant features |
| **Data size** | Work well on **smaller datasets** (maybe a few hundred thousand records) | Need **very large datasets** (millions of records) |
| **Compute** | Not very resource-heavy; usually no distributed training | **Computationally intensive**; may need **GPUs** and **distributed training** on a cluster |
| **What the developer controls** | **Hyperparameters**: the model's configurable design settings | The **architecture**: how layers connect, whether every neuron connects to every other, dense or sparse connections |
| **Interpretability** | **White box**: parameters can be examined and understood; easy to explain | **Black box**: parameters are hard to interpret; results may be right without you knowing why |

### What is a neural network?

- Neural networks are computing systems **inspired by the biological neural networks** in animal brains. That's why their learning units are called **neurons** (today often just "units" or "learning units").
- They are also called **ANNs (artificial neural networks)**.
- **"Deep"** refers to the use of **multiple layers**, sometimes hundreds.

### How data flows through layers

Each layer extracts slightly different information. **Earlier layers** learn fine details, and **later layers** combine them into more complex representations.

> **Example: recognizing a puppy in an image**
> Layer 1: pixel-level information → Layer 2: **edges** → Layer 3: **corners** → Layer 4: **objects** → Layer 5: puts it all together → **"puppy"**

- Neurons are **interconnected**, and the output of one layer is the input to the next. These connections work like **synapses** in the brain.
- **How** neurons connect (e.g. every neuron to every neuron in the next layer) is a design and architecture choice.
- Each neuron **receives signals** from neurons in the previous layer, **transforms** them, and **passes** its output signal on to neurons in the next layer.
- The input data makes up the signals traveling from the first layer to the last. The **output of the last layer is the model's prediction**.

---

## 2. Understanding neurons

A neuron is simple: it's a **mathematical function** made of two parts, a **linear** function and a **non-linear** function.

**Step by step:**
1. The neuron receives several inputs, **X₁, X₂, …, Xₙ**, from neurons in the previous layer.
2. Each input connection has a **weight (W)** showing how **important** that connection is. More important connections get higher weights.
3. The neuron computes the weighted inputs and adds a **bias (b)**: **Wx + b**. This **linear** part learns **linear relationships** in the data.
4. The result goes through an **activation function, Φ (phi)**. This is usually **non-linear** and learns **non-linear relationships**.

> **What a single neuron computes:** **Φ(Wᵢ·Xᵢ + bᵢ)**, the activation function applied to the weighted sum of inputs.

| Part | Set by | Changed during training? |
|---|---|---|
| **Weights (W)** and **biases (b)** | Learned from data | **Yes**: they are the **model parameters**, adjusted to improve performance |
| **Activation function (Φ)** | The network designer | No: it's part of the design |

The math of one neuron seems trivial, but thousands of neurons with many interconnections produce "almost magical" results.

---

## 3. Training a neural network

**Model parameters** are the **weights and biases** of every connection. Real-world networks can have **millions** of them. As data flows through the layers, these parameters transform it into the final prediction.

**The goal of training:** find parameter values that **minimize the loss**, meaning the gap between the model's predictions and the actual values. Smaller loss = better predictions.

### Gradient descent (the intuition)

- Picture a 3D surface: two model parameters on the x and y axes, and the **loss** on the z axis. (Real networks have millions or billions of parameters. Two are shown to keep it simple.)
- Every combination of parameter values gives a loss, so you get a landscape of high and low points.
- Parameters start **random**, so you begin anywhere on the slope.
- **Gradient descent** "**walks down the slope**" toward the parameter values with the **lowest loss**.
- The direction comes from **gradients**: the **partial derivatives of the loss with respect to each model parameter**. You don't need the math, only the intuition.

### The training loop

1. **Initialize** all weights and biases randomly.
2. **Forward pass:** Pass the training data through the model to get predictions (inaccurate at first).
3. **Compute the loss**, the difference between predicted and actual values. *(The course writes "loss = prediction − actual" only to show it's a difference, not a literal subtraction.)*
4. **Compute the gradients** from the loss.
5. **Backward pass:** Use the gradients to **update the parameters**, from the **last layer back to the first**.
6. **Repeat** with the updated parameters until training is complete.

---

## 4. Convolutional neural networks (CNNs): for images

### Why not use a dense network for images?

A **dense neural network** connects every neuron to every neuron in the layers before and after it.
- **Parameter explosion:** With thousands of neurons per layer and tens or hundreds of layers, there are millions of parameters. With complex data like images, there are too many to train well.
- **Loss of spatial information:**
  - Images are **2D grids of pixels**: one intensity value per pixel for **grayscale**, or **RGB** (red, green, blue) values for **color**.
  - Dense networks work on **one-dimensional** data, so the image must be **flattened**, which loses its spatial structure.

**CNNs** are deep learning models specialized for **grid-like data such as images**. They use **convolutional and pooling layers** to capture local patterns hierarchically. Put simply, they're very good at **recognizing patterns in images**.

### Inspired by the visual cortex

- Your brain doesn't process an image all at once. **Local receptors** each sense only a **limited region**.
- Their information is passed to other layers in the brain and **pieced together**. This is **hierarchical feature extraction**: high-level neurons combine features found by low-level neurons.
- CNNs **mimic this**.

### The two kinds of layers

**1. Convolutional layer: extracts features**
- Plays the role of the local receptors.
- Has a **local receptive field** called a **kernel** or **filter**: a small grid of numbers. These numbers are **model parameters**, learned during training.
- The kernel **slides over the image**. At each position, its values are multiplied by the pixel values beneath it, producing one value of the **convolved feature**, also called the **feature map**.
- Different kernels extract different features: **horizontal or vertical edges, sharpening, blurring**, and more.

**2. Pooling layer: simplifies (downsamples)**
- Feature maps are very dense. Pooling **reduces their spatial size** while keeping the important information.
- **Purpose:**
  - Lower the computational cost.
  - Make the network **robust to where an object appears and how big it is**. A kitten in the top-left or top-right corner is still a kitten (**location invariance**).
- A pooling filter slides over the input and aggregates:
  - **Max pooling** takes the **maximum** value.
  - **Average pooling** takes the **average** value.

**Typical CNN architecture:** alternating **convolution + pooling** blocks → a few **dense, fully connected layers** → the final prediction (e.g. classification or object detection).

---

## 5. Recurrent neural networks (RNNs): for sequences

RNNs are designed for **sequential data** with **time-related dependencies**, such as **time series** and **natural language**. Dense networks and CNNs can't capture these.

### Feed-forward vs. recurrent

| | Feed-forward networks (dense, CNN) | Recurrent networks |
|---|---|---|
| **Data flow** | Forward only, from the first layer to the last | Output from one time step is **fed back** in at the next |
| **Input** | The **whole input at once** | Fed in **one step at a time** |
| **Best for** | **Independent** records. *Example:* one home's attributes have nothing to do with another's in a price model. | **Dependent** sequences. *Example:* a stock's price at each tick depends on the ticks before it. |

### The recurrent neuron

- A feed-forward neuron outputs **Y = activation(Wx + b)**.
- A **recurrent neuron** at time *t* processes the current input **X(t)** **plus** its own previous output **Y(t−1)**. This is how it picks up time-related information.
- In practice, it keeps a **hidden state** that updates from the new input and the previous hidden state. This hidden state is its **memory**. **More memory = more information captured.**
- **LSTM (long short-term memory)** cells use a **logic-gate structure** to **forget unimportant old memories** and **store important new ones**.

### Memory cells and unrolling through time

- A **layer** of recurrent neurons is called a **memory cell**, because it has memory.
- An RNN is built by **unrolling** the memory cell **through time**, with one unrolled layer per element in the input sequence.
  - At t = 1, input X(1) (the first word, or the first stock tick) → output Y(1), and hidden state h(1) is updated.
  - At t = 2, input X(2) plus h(1) → and so on.
  - *Example:* A 10-element sequence → the RNN has **10 unrolled layers**.
- **Uses:** time series (stock prices) and **natural language**, where word order matters.
- **Limitation:** Simple RNN cells don't have enough memory for **very long sequences**. That's why variations like **LSTM** were developed: they handle long sentences, paragraphs, or stock data over days and months instead of hours.

---

## 6. Natural language processing (NLP)

**NLP** is the field of AI focused on the interaction between computers and human language: enabling computers to **understand, interpret, generate, and respond** to it.

| Component | Goal |
|---|---|
| **NLU (natural language understanding)** | Extract meaning from text or speech and turn it into a **structured representation** a machine can use |
| **NLG (natural language generation)** | Turn **structured data** into human-readable text or speech |

**Common NLP tasks:**
- **Text understanding:** **sentiment analysis** (emotional tone), **text classification** (labels or categories), **text summarization**
- **Speech recognition:** speech → text (Siri, Alexa, transcription, voice control)
- **Machine translation:** e.g. Google Translate, translation on social media
- **Language generation:** chatbot responses, content generation, automatic report writing

NLP models are often built with **RNNs**, because text is sequential. Newer architectures such as **transformers** can also process sequences.

### Turning words into numbers

Neural networks only understand numbers, so text must be **encoded**. *Example sentence:* "It is a beautiful day today" (six words).

| Technique | How it works | Limitation / note |
|---|---|---|
| **One-hot encoding** | Each sentence is an array the size of the whole dictionary: **1** if a word is present, **0** if not | Ignores how often a word appears |
| **Count-vector encoding** | Same array, but each element holds the **count** of that word in the sentence | — |
| **TF-IDF** (term frequency–inverse document frequency) | Gives each word a score: **up-weights** words frequent in a sentence, **down-weights** words common across the whole corpus (like *and, the, then*) | An improvement over the two above; good for simple NLP |
| **Word embeddings** | A neural network trained on a large corpus learns numbers that capture **meaning**. Similar words get similar values (e.g. *dog, cat*, and other animals sit close together). | Used for **advanced** NLP |

### How an RNN handles text

Each encoded word is fed in **one time step at a time**. The words so far are used to **predict the next word**. This helps with autocompletion, fill-in-the-blank, translation, and more.

| RNN type | Input → output | Example task |
|---|---|---|
| **One-to-many** | A single vector → a sequence | **Text generation**: "Cricket" → "is" → "very" → … (each new word is fed back in) |
| **Many-to-one** | A sequence → a single value | **Sentiment analysis** of a sentence |
| **Many-to-many (equal length)** | A sequence → a same-length sequence | **Parts-of-speech tagging**, one tag per word |
| **Sequence-to-sequence (unequal length)** | A sequence → a different-length sequence | **Language translation** |

---

## 7. Attention-based models and transformers

**Transformers** were introduced in **2017** in ***Attention Is All You Need*** by **Vaswani et al.** They revolutionized NLP and are now used for ML tasks **beyond NLP** too. **All of today's LLMs** trace back to them.

| Concept | What it does |
|---|---|
| **Attention** | Lets the network **focus on specific parts of the input** while ignoring others |
| **Self-attention** | The core innovation: weighs the importance of different parts of the input sequence, capturing **long-range dependencies** |
| **Multi-head attention** | Several attention heads **in parallel**, each capturing different relationships, which improves learning and generalization |

### The translation example ("I ate a yummy meal" → German)

- **Without attention:** The model captures the **whole input in one representation** and translates from that, producing output **one word at a time** (each new word uses the full input plus the words generated so far) until an **end-of-sentence token**.
- **With attention:**
  - When generating *Ich*, focus on **"I"**.
  - When generating the German word for "yummy", focus on **"yummy"**.
  - Some output words need attention on **several** input words.
- Using the whole input **plus** attention gives better output than one single representation.

### Large language models (as described in this course)

- Models like the **GPT series** (ChatGPT) and **PaLM 2** (Google Bard) all use attention in some form.
- LLMs **predict the next word** from the words before it.
- They are "large" because they have **billions of parameters** and are trained on **billions of records**.
- The course mentions a parameter figure for GPT-4 here (175 billion) that **differs** from the figure in [Chapter 2](02-introduction-to-gpt-models.md) (an undisclosed number, estimated at around 1.7 trillion). Both are recorded as each course stated them.

---

## 8. Generative adversarial networks (GANs)

### Generative AI recap

- **Generative AI** produces **new, original** content (text, images, music) based on patterns in existing data.
- New samples **resemble** the training data but **don't exist in it**.
- It's usually powered by very large **foundation models** trained on huge datasets. **LLMs** are generative AI for language.
- It can perform out-of-the-box tasks like question answering, summarization, and classification.

### GANs

- Introduced in **2014** by **Ian Goodfellow et al.**
- One of the **original** generative models. Not nearly as powerful as today's models, but "**where it all started**".
- **Generative:** it generates data, usually **images**.
- **Adversarial:** it's made of **two neural networks competing** in a **zero-sum game**. As one gets better, the other gets worse.

| Component | Role | Analogy |
|---|---|---|
| **Generator** | Takes **random noise** as input and produces realistic-looking **fake data** | A forger or artist reproducing originals |
| **Discriminator** | A simple **classification model** that tells **real** data (from a database) from **fake** data (from the generator) | An art critic |

**How training goes:**
1. **Start:** The generator's fakes are poor, so the discriminator easily spots them.
2. Each time a fake is caught, the generator is **heavily penalized** and improves.
3. As the generator gets better, the discriminator's accuracy **falls**.
4. **End:** The discriminator **can't tell real from fake**. The generator can now produce realistic data of the type it was trained on.

---

## 9. Reinforcement learning

**Reinforcement learning** is **not** a deep learning technique. It's a **separate subfield of ML**, where an **agent** learns to make decisions by interacting with an **environment**, aiming to **maximize cumulative rewards** through **trial and error**. *Like life:* you try things, see the results, and adjust.

| Term | Meaning | Hill-climbing robot example |
|---|---|---|
| **Agent** | The learner and decision-maker | The robot |
| **Environment** | Everything the agent interacts with and learns from; it gives feedback | The hill and its terrain |
| **State (Sₜ)** | The current situation, with all the information needed to decide (continuous or discrete) | Where the robot is now |
| **Action (Aₜ)** | One of the possible choices at each time step; it changes the state to **Sₜ₊₁** | Step left, right, forward, backward, or sideways |
| **Reward** | Feedback for each action: large, small, or **negative** (a punishment) | Climbing higher = reward; falling into a pit = punishment |
| **Policy** | How the agent makes decisions. It is **not predefined**; it **evolves** as the agent learns the best way to maximize expected cumulative reward. | — |

- The aim is the **total (cumulative) reward**, not the reward at a single step.
- Highly rewarded actions tend to be **repeated**.
- RL runs as a **feedback loop**: action → reward → adjust → repeat.

### Exploration vs. exploitation (the critical challenge)

| Strategy | What it means | Trade-off |
|---|---|---|
| **Exploration** | Try actions the agent hasn't tried much, to learn more about the environment and find better options | Can lead to worse results |
| **Exploitation** | Choose actions already known to give the highest expected reward | Uses current knowledge, but may miss better options |

The agent must explore enough to gather valuable information, while exploiting what it knows to maximize rewards.

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **Deep learning** | ML using neural networks with multiple layers |
| **Neuron / unit** | The learning unit: computes Φ(Wx + b) |
| **Weights & biases** | The model parameters learned during training |
| **Activation function (Φ)** | A usually non-linear function applied to the weighted sum; part of the network design |
| **Hyperparameters** | Configurable design settings of traditional ML models |
| **White box / black box** | Interpretable model / hard-to-interpret model |
| **Loss** | How far predictions are from the actual values |
| **Gradient descent** | The optimization that "walks down" the loss surface to minimize loss |
| **Gradients** | Partial derivatives of the loss with respect to each parameter |
| **Forward / backward pass** | Getting predictions / updating parameters from the last layer back to the first |
| **Dense network** | Every neuron connected to every neuron in adjacent layers |
| **CNN** | Convolutional neural network for grid-like data such as images |
| **Kernel / filter** | The small sliding grid in a convolutional layer that extracts features |
| **Feature map** | The convolved feature produced by sliding a kernel over an image |
| **Pooling (max / average)** | Downsampling feature maps by taking the max or average |
| **RNN** | Recurrent neural network for sequential, time-dependent data |
| **Hidden state** | The memory a recurrent neuron carries between time steps |
| **LSTM** | Long short-term memory cell: an RNN cell with more memory for longer sequences |
| **NLU / NLG** | Natural language understanding / generation |
| **One-hot / count vector / TF-IDF** | Simple ways to turn words into numbers |
| **Word embeddings** | Learned numeric representations that capture word meaning |
| **Attention / self-attention / multi-head attention** | Mechanisms that let a model focus on the most relevant parts of its input |
| **GAN** | Generator vs. discriminator in a zero-sum game |
| **Reinforcement learning** | An agent learning by trial and error to maximize cumulative reward |
| **Exploration vs. exploitation** | Trying new actions vs. using known best actions |

---

*Source: course transcript "Deep Learning and Neural Networks" (11 videos).*

[← Previous chapter](03-artificial-intelligence-and-machine-learning.md) · [Back to contents](../README.md) · [Next chapter →](05-getting-started-with-prompt-engineering.md)
