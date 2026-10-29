# Chapter 1 · An Introduction to Generative AI

**Part 1 — Activate** · Instructor: Janani Ravi · [← Back to contents](../README.md) · [Next chapter →](02-introduction-to-gpt-models.md)

---

## At a glance

- **Generative AI** creates new content (text, images, audio, video) that resembles its training data but isn't an exact copy.
- **Discriminative models** do something different: they classify or label existing data.
- Generative models are **probabilistic**. The same input can give a different output each time.
- The input to a generative model is usually a **prompt**, a user request for a certain kind of content. Writing prompts well is called **prompt engineering**.
- The field goes back decades, from rule-based systems like **ELIZA** (1960s) to the **transformer** (2017) that powers today's large language models.
- Generative AI brings real **risks**: harmful content, intellectual property issues, privacy leaks, bias, hallucinations, and **deepfakes**. There are concrete ways to reduce them.

---

## 1. What is generative AI?

AI and machine learning have been researched for decades. But AI only really came into its own in the last 10–15 years, once big data technologies made it possible to process massive datasets.

**Generative AI** is a class of AI techniques and models built to produce content that is both **novel and coherent**.

- These models are usually trained on **massive datasets**, mostly data from the internet that has been pre-processed and cleaned.
- They learn the **patterns and structures** in that data and reproduce them at the output.
- The output resembles or extends the training data. It's similar, but not identical.

> **Example from the course:** A model trained to generate cat images will produce cats that look like the ones it saw in training, but they may not match any original image exactly.

A **machine learning model** is a mathematical representation that tries to capture the relationships and entities that exist in the real world.

**Why the recent buzz?** Interest and research go back to the 1950s and picked up in the last ten years or so. The excitement jumped with models like OpenAI's ChatGPT and Google's Bard, because simple interfaces made it possible to create high-quality text, graphics, and video in seconds.

### Generative vs. discriminative models

| | Discriminative models | Generative models |
|---|---|---|
| **Goal** | Find the *decision boundary* that separates classes, then classify the input | Learn the *probability distribution* of the data, then sample from it to create new data |
| **Training data** | Many observations, **each with a label** | Many observations of the kind of thing to generate; **labels not needed** (usually unsupervised learning). The data must be massive. |
| **Output** | A probability score for each category. The highest one is the prediction. | New content similar to, but not the same as, the training data |
| **Behavior** | **Deterministic**: same model + same input = same output (e.g. classification, regression) | **Probabilistic**: includes a random element, so the same input can give different outputs |
| **Complexity** | Simpler | Harder and more complex, because they must model richer relationships in the data |

**Discriminative example (handwritten digits):** The model is trained on images of digits, each labeled with the correct digit. It learns what each digit looks like. Given a new, unlabeled image, it outputs a probability for each digit. The one with the highest score (say, 8) is the prediction.

**Generative example (cats):** The model learns what makes up a cat: whiskers, nose, ears, postures. After training, it takes an input, which could be a latent noise variable, some text, or anything else. It uses that input and what it learned to generate new cat images.

> This probabilistic nature is why ChatGPT or Bard give *similar but not identical* answers when you ask the same question twice.

---

## 2. Content generation using generative models

**Generation starts with a prompt.** This can be text, an image, a video, or another kind of input.

- **Why it's so popular now:** Generating content only takes a query in **natural language**.
- **Earlier**, you had to use an API or write code to interact with a generative model, which wasn't accessible to everyone.
- Natural-language prompting has **democratized** generative AI.

### How these models handle content

- Today's generative models **combine several AI algorithms and techniques**. They aren't a single modality.
- **Text:** Natural language processing turns raw letters, punctuation, and words into sentences, parts of speech, entities, and actions. Text is represented as **vectors** using encoding techniques.
- **Images:** These are turned into visual elements, also expressed as vectors.
- Behind the scenes, the models are **complex neural network architectures** that focus on the relevant parts of your input to generate a response.

**Garbage in, garbage out.** Generative models train on real-world data, so they can absorb and encode **biases, racism, deception**, and other problems in that data.

### A short path to today

- **1960s:** Programmatic content generation began with **rule-based (expert) systems** that used explicitly written rules. These could only go so far.
- **Neural networks** (designed to mimic the human brain) learn the rules from patterns in data. The first ones existed in the **1950s**, but they were held back by limited computing power and small datasets.
- **Early 2000s:** Big data technologies such as **MapReduce and Hadoop** made it possible to process huge datasets in parallel across clusters. Together with **GPUs**, this made neural networks practical for generating content.

### Popular tools covered in the course

- **ChatGPT:** an AI chatbot launched by **OpenAI in November 2022**
- **Google Bard:** Google's conversational agent, powered by a different model
- **DALL-E:** an OpenAI model that generates images from text descriptions

**ChatGPT vs. Google Bard (as described in the course):**

| | ChatGPT | Google Bard |
|---|---|---|
| **Access** | chat.openai.com | bard.google.com |
| **Cost** | Mostly free. A paid plan (~$20/month) gives premium server access and **GPT-4**. | Completely free |
| **Account** | Sign up with an email or social media account | Requires a Google account (Gmail or corporate) |
| **Underlying model** | **GPT** (Generative Pre-trained Transformer) | **PaLM 2** (Pathways Language Model) |
| **Current info** | Free version answers based on an **information cut-off date** | Tends to be more up to date, using real-time Google Search info |
| **Image analysis** | Paid version only (GPT-4) | Included in the free version |

The instructor's advice: responses to the same query will differ, so it's good practice to **use both**. Which is "better" depends on your use case.

**Interface vs. model:** In everyday speech we call ChatGPT and DALL-E "models", but strictly speaking they are **interfaces** to the underlying models.
- ChatGPT is a chatbot built on a **text-to-text** model, GPT.
- DALL-E is the interface to a **text-to-image** model.
- In both cases, the underlying model is a mathematical construct trained on massive amounts of data.

### Large language models (LLMs)

The models behind ChatGPT and Bard are **large language models**.

- They take natural-language input and generate text **one word at a time**, predicting the next word from what has already been generated.
- They are called "large" for two reasons:
  1. They have **billions of parameters** to train. More parameters can capture more complex relationships, but they take longer to train and need more data.
  2. They are trained on a **huge corpus** of billions of records.

**The breakthrough: the transformer.**
- Introduced in **2017** in the paper ***Attention Is All You Need***.
- Transformers are **sequence-to-sequence** models. They take an input sequence and produce an output sequence. Natural language is a sequence of words, and both input and output can be of any length.
- Their key innovation is **attention**, which lets the network focus on the most relevant parts of the input when producing output.
- There is a direct line from the transformer to today's language models.

---

## 3. Prompt engineering

**Prompt engineering** is the process of structuring text so a generative AI model can interpret and understand it. It's a skill to get the most relevant, coherent, and meaningful response.

- It's mainly used with **text-to-text** models, though prompts also guide text-to-image and text-to-audio models.
- It works because of the model's ability for **in-context learning**. The model learns from the instructions in your prompt and from the back-and-forth conversation.
- A **prompt** is just natural-language text describing the task, essentially a question to the model.
- **Why "engineering"?** Generative AI is still early. Models may not give exactly what you want, and they can **hallucinate** (make up facts).

**Example prompts from the course:**
- "Please explain Einstein's theory of relativity in simple terms, as though to a fifth grader."
- "Write code in Python to compute the average of numbers in a list."
- "Write a poem about how programming is fun; the poem should be short and humorous."

### Why prompting matters

- It guides the model toward **relevant, coherent** output by including context and details.
- Deeper prompts improve the **quality and diversity** of output, instead of canned responses.
- Real-world data is biased. Good prompts can give you **more control**, improve **interpretability**, and even **reduce bias**.
- They help limit **hallucinations** by steering the model to cite the right references.
- You can state your **goal** in the prompt so the model knows what a good outcome looks like.
- Good prompts improve **safety** and help defend against **prompt hacking**.

**Uses inside organizations:**
- Tuning an e-commerce chatbot to answer customer queries
- Helping a law firm's lawyers generate contract specifications
- Handling common technical support questions so they don't reach human agents

### Challenges

- Getting the required result **on the first try**
- Knowing **where to start** and how to structure the prompt
- **Mitigating bias** in the output
- Getting **diversity and creativity** instead of narrow answers
- **Interpretability**: understanding the reasoning behind a response
- Balancing **precision and creativity**: fact-based answers with some flair

### Security vulnerabilities

- **Prompt injection:** An attacker manipulates the prompt to produce malicious or harmful output.
- **Sensitive information exposure:** A model trained on company data might leak sensitive information to the wrong people.
- **Jailbreaking:** An attacker gains unauthorized access to the model's internal state and parameters, so its responses can no longer be trusted.
- **Bias and misinformation:** Models can perpetuate biases and produce unlawful or misleading information.

> A generative AI model has **no concept of right and wrong**, even when it seems like it does.

### Techniques

**Every word matters.** "Describe the Taj Mahal" and "Describe the history of the Taj Mahal" give very different responses. Be **clear, concise, detailed, and specific**, and break complex requests into smaller parts.

**Anatomy of a prompt:**

| Component | What it does | Example |
|---|---|---|
| **Instruction** | The core directive: what the model should do | "Summarize the following text" |
| **Context** | Background that shapes the answer | "I'm 25 years old, just starting off my career. How do I invest the money I have saved?" |
| **Input data** | Specific information for the model to process | A paragraph, a set of numbers, or a single word |
| **Output format** | How you want the result | CSV or JSON |

**Basic techniques:**
- **Role playing:** Ask the model to act as a specific entity, like a scientist or a math tutor, for tailored answers.
- **Iterative refinement:** Start broad, then refine based on how the model responds.
- **Constraints:** Models respond better to **positive constraints**. Say "Please use Python", not "Do not use Java".
- **Use the outputs:** Let each response inform your next prompt.

**Advanced techniques:**
- **Zero-shot prompting:** Give the model a task it hasn't seen in training, with no examples. This tests how well it generalizes.
- **Few-shot prompting / in-context learning:** Give a few examples ("shots") to guide the response. Use this if zero-shot results are poor.
- **Chain-of-thought prompting:** Guide the model through a series of reasoning steps for complex tasks.
- **Augmented / generated knowledge prompting:** Provide a knowledge base or script for the model to use when answering.

---

## 4. Evolution of generative AI (to the early 2010s)

Generative AI "caught fire" in **2023**, after ChatGPT's launch in November 2022. But some form of it has existed for decades. The instructor notes this is a selection of milestones, not a complete history.

| When | Milestone | Why it matters |
|---|---|---|
| **1957** | **Noam Chomsky**'s work on syntactic structures and **generative grammar** | Its rules for generating valid language structures became a foundation for early AI researchers trying to mimic human language |
| **Mid-1960s** | **ELIZA**, by MIT professor **Joseph Weizenbaum** | Considered the first-generation chatbot (see below) |
| **1968** | **SHRDLU**, by **Terry Winograd** | Users manipulated and reasoned about blocks in a virtual "block world" using English. Called the first multimodal AI, but it wasn't truly multimodal because it was text-only. |
| **Early 1980s** | The game **Rogue** | Pioneered **procedural content generation**: random algorithms created dungeons, items, and enemies. A precursor to modern generative techniques. |
| — | **Bayesian networks** | Model probabilistic **cause-and-effect** relationships between variables, helping produce more coherent, context-relevant content |
| **Late 1980s** | **RNNs** and **CNNs** | RNNs (recurrent neural networks) suit sequential data like time series and language. CNNs (convolutional neural networks) suit 2D image data. |
| *Through the early 2000s* | Paper: ***A Neural Probabilistic Language Model*** | Used neural networks (particularly feedforward networks) to model language. Improved language modeling, text generation, and machine translation. |
| **2009** | **ImageNet**, by **Fei-Fei Li** | A huge labeled image database. It led to the ImageNet Large Scale Visual Recognition Challenge, which spurred deep learning and CNNs. Winning architectures became a foundation for generative models. |
| **Early 2010s** | Apple's **Siri** | Popularized conversational AI and brought virtual assistants into the mainstream |
| **2012** | **AlexNet** (a CNN) | Applied deep learning to image classification, using deep layers, ReLU activation, dropout, regularization, and GPU acceleration. Kickstarted the **deep learning revolution**. |
| **2013** | **Word2vec** | A **word embedding** technique that maps words into dense vectors based on their meaning, helping models understand and generate relevant text |

**More about ELIZA:**
- It simulated a **Rogerian psychotherapist**, who listens empathetically and reflects the patient's feelings back.
- It was **rule-based**. It didn't understand language. It matched keywords like "I feel" or "I am" against predefined patterns and gave programmed responses.
- *Example:* "I'm feeling sad" might get "Tell me more about why you're feeling sad."
- It showed the potential of text-based human-computer conversation and paved the way for later NLP work.

---

## 5. Recent advances (about 2012–2018)

These advances paved the way for ChatGPT, Bard, and DALL-E.

### Variational autoencoders (VAEs)

- First conceptualized around **2013–2014**. One of the original generative models.
- They learn the distribution of the input data in a **lower-dimensional latent space**.
- **Two parts:**
  - The **encoder** compresses the input into the latent space and outputs that space's **mean and standard deviation**.
  - The **decoder** takes a sample from the latent space and tries to **reconstruct the original input**.
- **Training goal:** Reconstruct the input at the output. This isn't trivial, because the architecture is constrained.
- **Generating new data:** Pick a sample from the latent space's probability distribution and feed it to the decoder.

### Generative adversarial networks (GANs)

- Proposed in **2014** by **Ian Goodfellow** and other researchers.
- Made of **two neural networks that compete** during training in a **zero-sum game**: as one improves, the other gets worse.

| Component | Role | Analogy |
|---|---|---|
| **Generator (G)** | Takes **latent noise** (typically Gaussian noise) as input and produces fake data good enough to fool the discriminator | Art forger |
| **Discriminator (D)** | A simple **classification model** that decides whether data is real (from a real database) or fake (from the generator) | Art critic |

**How training works:**
1. At first the generator's fakes are obvious, so the discriminator's job is easy.
2. The discriminator **heavily penalizes** implausible fakes, and this feedback pushes the generator to improve.
3. Training ends when the discriminator **can no longer tell real from fake**.

GANs work very well with **images**.

### Attention and transformers

- Transformers are **sequence-to-sequence** models, and their key innovation is **attention**.
- **Attention** lets the network focus on specific parts of the input while ignoring others. Not every part of a long sentence is equally important.

**Translation example (English → German, "I ate a yummy meal"):**
- **Without attention:** The model looks at the whole sentence at once to produce the translation.
- Output is generated **one word at a time**, using the words already generated plus the input.
- **With attention:** To predict the first German word, *ich*, the model focuses on "I". To translate "yummy", it focuses on "yummy". Some words need attention across **several** input words.
- Shifting attention to different parts of the input at different steps gives a **better translation**. (The original transformer was a translation model.)

### From transformers to today's tools

| Year | Release |
|---|---|
| **2017** | Transformer architecture introduced |
| **2018** | OpenAI's **first GPT**. GPT models are **pre-trained** on huge amounts of text, then **fine-tuned** for specific tasks. |
| **2021** | OpenAI's **DALL-E**: photorealistic images from text |
| **2022** | **Stable Diffusion** (by Stability AI): images from text prompts, AI art, sketches, image editing |
| **2022** | **Midjourney**: a diffusion neural network that creates images from noise |

---

## 6. Applications of generative AI

| Area | What generative AI can do |
|---|---|
| **Image generation** | Text-to-image; turning sketches or text into realistic images (semantic image-to-image translation); filling missing or damaged parts of photos; raising resolution without pixelation (e.g. medical imaging, surveillance); editing color, lighting, style, and objects |
| **Software and coding** | Generating code from requirements; intelligent code completion in IDEs (e.g. **GitHub Copilot**); natural-language interfaces for coding; generating test cases; refactoring legacy code; detecting and suggesting fixes for bugs |
| **Video creation** | Automating editing (assembling clips, animations, effects); restyling video to match a reference; predicting future frames; enhancing or upscaling low-quality footage; building 3D models (e.g. using autoregressive models and GANs) |
| **Audio generation** | **Text-to-speech (TTS)** for voice assistants, audiobooks, and accessibility; composing music; **speech-to-speech (STS)** for voiceovers, dubbing, and character voices in games and film; sound effects and ambient audio |
| **Text generation** | Blog posts, marketing copy, social media posts; translation; powering chatbots; summarizing research papers, news, and emails; summarizing complex datasets into reports in **business intelligence and data analysis** |
| **Conversational agents** | Better language understanding; human-like, personalized replies; handling open-ended questions that older chatbots struggled with; learning user preferences from past conversations |
| **Organizational collaboration** | Splitting meeting recordings into titled sections with markers and streamlining note-taking; drafting job descriptions and marketing copy; automating repetitive tasks in word processors and email |
| **Enterprise search** | Securely analyzing contracts, research reports, and other documents for faster retrieval; highlighting key sections; categorizing and organizing documents automatically |

---

## 7. Risks of generative AI

| Risk | What it means |
|---|---|
| **Harmful content** | Realistic fake news and deepfakes; content produced at scale with little human effort; AI can't make ethical judgments; bad actors can use it to manipulate opinion, spread misinformation, or carry out psychological warfare |
| **Intellectual property** | Training data often lacks clear attribution, so outputs may infringe existing IP (especially in finance and pharmaceuticals). Open debates: should AI-generated work get copyright? Is it fair to train on others' work without paying them? |
| **Data privacy** | Training data may contain **personally identifiable information (PII)** that the model could reveal. Removing personal data is much harder than with a search engine. Organizations must comply with privacy laws. |
| **Confidential data disclosure** | Wider access can lead to accidental leaks, e.g. patient medical records or a pharma company's product strategy, with legal and trust consequences |
| **Reinforcing bias** | Models absorb sexist, racist, or ableist bias from online data. Organizations using a model may have no control over that bias. Real-world data lacks diversity, so models can amplify prejudice. |
| **Workforce morale** | AI is speeding up tasks done by knowledge workers (writing, coding, content, summarizing, analysis). This can displace workers and cause uncertainty and anxiety as roles change. |
| **Attribution and authenticity** | Training data may come from poorly governed or doubtful sources. Models can **hallucinate**, and false information can spread further, so outputs can't always be trusted. |
| **Explainability** | You can see a response but not *why* it was generated. Models may find **correlations rather than causation**, which limits how far you can trust them. |

### Reducing the risks (when building your own models)

- Use **diverse and representative** training data.
- Keep **reviewing and testing outputs for bias**, and catch it early.
- **Transparently disclose** your training data and algorithms to build trust.
- Keep **assessing data quality**, and stop fake content from entering training data.
- **Get consent** before generating content from other people's work.
- **Know your model's capabilities and limitations**, and communicate them clearly to users.

---

## 8. Ethical considerations

The course groups them into four areas:

**1. Accuracy and communicating uncertainty**
- Train on diverse, accurate data to balance accuracy, precision, and recall.
- Because models are probabilistic, communicate training sources, explain AI decisions, and point out uncertainty.
- Set limits to prevent excessive automation, and keep **human oversight** in critical decisions.

**2. Safety and bias mitigation**
- Run regular **bias, explainability, and robustness** evaluations.
- Analyze and clean training data, and protect PII in line with privacy laws.
- Do **security assessments** as you would for software, including for **prompt injection**.

**3. Honesty and data provenance**
- Respect where training data comes from, and get **consent** where required.
- Make sure training data is diverse and free of obvious bias.
- Be **transparent** about what you know of the model's biases and limitations.
- Use data ethically and comply with both company policy and privacy laws.

**4. Empowerment and human-centric AI**
- Present AI as an **assistant**, especially where trust is critical (finance, healthcare).
- Combine **human judgment** with AI insights for crucial decisions.
- Make AI outputs accessible to all users, and treat content contributors and data labelers fairly.
- Acknowledge the **energy and water** used to train LLMs, and try to shrink models without losing accuracy.

### Tips from Harvard Business Review (2023)

- Train on **zero-party data** (data customers share proactively) or **first-party data** (data the organization collects directly). Strong **data provenance** keeps models accurate, original, and trusted.
- Relying on **third-party** data makes reliability hard to ensure. Stale data makes **hallucinations** more likely.
- Review training data and remove biased, toxic, and false elements.
- Keep **humans in the loop**: AI can't understand emotional or business context. Use AI to **augment** people, not replace them.
- Continuously **monitor and test** outputs for accuracy, bias, and hallucinations.
- **Get feedback and iterate**, listening to employees, trusted advisors, and affected communities.

---

## 9. Deepfake AI

A **deepfake** is AI used to create convincing image, audio, and video **hoaxes**: content that looks real but isn't, usually meant to mislead. The term covers both the AI system and the fake content.
- The word combines **deep learning** (neural networks) + **fake**.
- *Example:* A celebrity appearing to endorse a product they never endorsed.

### Types of deepfakes

| Type | Description |
|---|---|
| **Face swap** | One person's face replaced with another's in a video (one of the most common) |
| **Lip syncing** | Lips altered to match new or changed audio, so someone appears to say something they never said |
| **Voice cloning** | AI copies a person's vocal patterns to make audio of them saying anything |
| **Expression manipulation** | Facial expressions or body language changed in existing video (used in film effects, but can be misused) |
| **Synthetic people** | Entirely fake people, e.g. virtual influencers or fake personas |
| **Scene generation / alteration** | Changing backgrounds or weather, or creating fictional locations |

**How they're made:** Usually with a **GAN**. The generator creates the fake, and the discriminator judges how real it looks and penalizes obvious fakes, so the output keeps getting more realistic.
- For a **photo**, the GAN may study photos of the target from different angles.
- For a **video**, it may analyze the target's behavior, movement, and speech patterns.

### Uses

- **Benign:** art; entertainment (films and games cloning or adjusting actors' voices); satire and parody
- **Harmful:** reputational damage; **false evidence** in legal cases; **fraud** (impersonation to obtain bank or card details); swaying public opinion with fake videos of politicians; moving a company's **stock price** with a fake CEO video

### How to spot deepfakes

**Video:**
- Unusual movement or awkward facial positioning
- Unnatural facial or body movement
- Unnatural coloring or inconsistent, uneven audio
- Looks odd when you zoom in or out
- People who don't blink

**Text and email:**
- Misspellings or unnatural sentences
- A suspicious sender address, or one that is very close to a trusted one
- Phrasing that doesn't match the sender's personality
- Messages that don't make sense coming from that sender

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **Generative AI** | AI that creates novel, coherent content resembling its training data |
| **Discriminative model** | A model that classifies or labels existing data by learning decision boundaries |
| **Probabilistic vs. deterministic** | Probabilistic models can give different outputs for the same input; deterministic models always give the same output |
| **Prompt** | A natural-language request describing the task for the model |
| **Prompt engineering** | Structuring prompts so a model gives the most relevant, coherent response |
| **In-context learning** | A model learning from instructions and examples within the prompt or conversation |
| **Hallucination** | A model confidently producing false or made-up information |
| **LLM** | Large language model: billions of parameters, trained on huge text corpora, predicts the next word |
| **Transformer** | The 2017 sequence-to-sequence neural network architecture built on attention |
| **Attention** | A mechanism that lets a network focus on the most relevant parts of its input |
| **VAE** | Variational autoencoder: an encoder–decoder model that generates data by sampling a latent space |
| **GAN** | Generative adversarial network: a generator and discriminator competing in a zero-sum game |
| **PII** | Personally identifiable information |
| **Prompt injection / jailbreaking** | Attacks that manipulate prompts or gain unauthorized access to a model's internals |
| **Zero-party / first-party data** | Data customers share proactively / data an organization collects directly |
| **Deepfake** | AI-generated fake image, audio, or video meant to look real |

---

*Source: course transcript "An Introduction to Generative AI" (11 videos). Product details such as names, prices, and features are given as they were described in the course.*

[← Back to contents](../README.md) · [Next chapter →](02-introduction-to-gpt-models.md)
