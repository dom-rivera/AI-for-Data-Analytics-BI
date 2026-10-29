# Chapter 5 · Getting Started with Prompt Engineering

**Part 1 — Activate** · Instructor: Janani Ravi · [← Previous chapter](04-deep-learning-and-neural-networks.md) · [Back to contents](../README.md) · [Next chapter →](06-exploring-prompt-engineering-techniques.md)

> **About this chapter:** Much of this course is hands-on demos of ChatGPT, Google Bard, Bing Chat, and Perplexity AI. This chapter captures the **lessons and observations** from those demos. Tool features, models, prices, and limits are recorded **as described at the time the course was recorded**. The instructor stresses that these tools change quickly. The course also notes that you aren't expected to create accounts on these platforms; the principles apply to any corporate conversational AI chatbot.

---

## At a glance

- **Prompt engineering** is designing, refining, and optimizing prompts so a generative AI model gives the output you want.
- The **prompt is all the model has** to go on, so context, constraints, and clarity matter.
- Chatbots remember context **within a session**, but **not across sessions**.
- LLM output is **stochastic (probabilistic)**: the same prompt can give different answers.
- **Temperature** controls randomness: **higher = more creative**, **lower = more precise**.
- The course compares four tools: **ChatGPT, Google Bard, Bing Chat, and Perplexity AI**. Each has different strengths, so it's useful to have more than one in your toolkit.
- **Don't share sensitive data** with these tools, and **always verify** their answers.

---

## 1. Introducing prompt engineering

**A bit of history:** In the late 1990s, Google Search made crafting search queries a skill. Search later improved so simple terms were enough. Natural-language queries brought a similar revolution when **ChatGPT was released on November 30, 2022**. You could talk to a knowledgeable chatbot in plain language, and this gave rise to **prompt engineering**.

- A **prompt** is the natural-language query you give a chatbot. It's a question or instruction describing the task: give information, ideate, summarize, and so on.
- **Prompt engineering** is structuring text so a generative AI model can interpret it: **designing, refining, and optimizing** prompts.
- **An analogy:** When you ask a friend or colleague for information, you set the context first. The same applies to AI models.

**Generative AI** means ML models that produce **new, previously unseen content** (images, music, text) based on patterns learned from data.

### Text-to-text models and in-context learning

- Prompt engineering is mainly used with **text-to-text** models: text in, text out (a sequence of words in, a sequence of words out).
- Well-designed prompts let the model use **in-context learning**: it learns from the information in your prompt (why you need something, your scenario, your constraints, the form you want) and tailors its response.
- For **text-to-image** or **text-to-audio** models, the prompt defines the kind of image or music you want.

### Example prompts and what makes them work

| Type | Example | Why it's well crafted |
|---|---|---|
| **Explanation** | "Please explain Einstein's theory of relativity in simple terms to a 5th grader." | Asks for an explanation *and* sets the level (simple, for a 5th grader) |
| **Code generation** | "Write code in Python to compute the average of numbers in a list." | Clearly defines the task **and the programming language**. Models understand many human *and* programming languages, so say which one. |
| **Creative** | "Write a poem about how programming is fun - should be short and humorous." | Rich context: the topic, the angle (*fun*, not a drudge), the length, and the tone |

*Note: The transcript says "the more ambiguous your task is, the better the response" at this point. From the example that follows, the point being made is that a **clearly defined** task gets a better response.*

### Why good prompts matter

- **The prompt is the model's only guide.** Getting it right avoids follow-up questions.
- It improves the **quality and diversity** of output, with less bias and more creativity.
- It gives you **more control**, better **interpretability**, and **less bias**. Models mimic their training data, so they can be biased.
- It helps reduce **hallucinations**: when a model gives a wrong answer but firmly believes it's correct and can't move away from it.
- Tell the model what **good and bad outcomes** look like, so it knows its goal.
- It improves **safety** against **prompt hacking**, where users send prompts to produce unwanted behavior.

---

## 2. Business use cases, challenges, and safety

### Three business examples

| Setting | How prompt engineering and generative AI help |
|---|---|
| **E-commerce customer service** | Human-staffed customer service is expensive, and many issues (wrong products, delivery problems, refunds, exchanges) are simple. Tune a model on company data to act as a **polite, helpful customer service agent**. |
| **Law firms** | A model trained on the firm's documents (law, contracts, case files) can **draft legal documents and contracts**, give **predictive analysis of case outcomes**, **summarize case law** for research, and offer insights based on **precedents**. |
| **Technical support desks** | **Auto-respond** to common queries for faster resolution, **summarize documentation or logs** for troubleshooting, and **suggest solutions** based on patterns in past tickets. |

### Challenges

- **Getting it right the first try** is hard, especially for complex requests. Chatbots track the **whole conversation** as context, so follow-ups help.
- **Knowing where to start.** Simple queries ("What's the capital of Canada?", "Fun things for a birthday party?") are easy. For complex research, the model is influenced by earlier questions, so **starting in the wrong place can lead you down the wrong track**, and it's hard to get back.
- **Mitigating bias.** Models are only as good as their training data, and real-world data contains subtle and overt biases. Factor this into your prompts.
- **Diversity and creativity.** Use **open-ended**, varied prompts that don't steer the model. **Iterate and refine** to get a broad range of results.
- **Understanding the reasoning** behind a response, so you can improve it.
- **Precision vs. creativity.** Lean toward **precision** for factual research, and toward **creativity** for poems and idea generation.

### Security concerns

- **Prompt injection / manipulation:** Models are tools that can be driven toward good or harm. People use prompts to produce harmful outputs.
- **Leaking sensitive information:** A model trained on company data, without the right restrictions and security settings, could expose (for example) legal-team-only information to operations or customer service teams.
- **Jailbreaking:** Using prompts to gain unauthorized access to the model's internal state, or to extract, modify, or use a model outside its intended or licensed environment, by **bypassing its restrictions**.
- **Perpetuating bias:** These models train on the requests and responses they receive. Using them to spread bias or unlawful or misleading information feeds back into training and can make the model **worse over time**.

### Where to practice (as presented in the course)

| Tool | Developer | Notes from the course |
|---|---|---|
| **ChatGPT** | OpenAI | Launched November 2022. The **fastest app to reach 100 million** users. |
| **Google Bard** | Google | Google's experimental conversational AI. Trained on a different model, so responses often differ from ChatGPT. Launched **February 2023**. |
| **Bing Chat** | Microsoft | Integrates OpenAI's **GPT-4**. Launched **February 2023**. |
| **OpenAI Playground** | OpenAI | A **paid**, web-based playground (with some free starting credits) exposing the models' APIs to developers and researchers. Lets you tune parameters such as **randomness, response length, creativity, and diversity**. Not for day-to-day use; it's for understanding and customizing models. |

---

## 3. Understanding generative AI and LLMs (non-technical)

- **Discriminative models** classify records or predict numbers. They differentiate between existing records.
- **Generative models** create **entirely new** text, images, or media that resemble what they've seen but aren't identical.

**Why "large"?** Generative models have **billions of parameters**, and parameters converge to their final values during training. Scale as given in the course:

| Model | Parameters |
|---|---|
| **GPT-2** | 1.5 billion |
| **GPT-3** | 175 billion |
| **GPT-4** | Said to be **1.7 trillion** |

They are trained on huge datasets (think: all the text available on the internet). They can do many tasks out of the box: question answering, summarization, explanation, classification, code generation, data generation, code debugging, and more.

**A model** is just a **mathematical representation** of everything it learned from its training data.

### Application vs. model

| Application (interface) | Underlying model | Type |
|---|---|---|
| **ChatGPT** | **GPT** (generative pre-trained transformer) | Text-to-text |
| **DALL-E** | A text-to-image model | Text-to-image |

It's fine to call ChatGPT and DALL-E "models" in conversation, but strictly they are **applications built on models**. "ChatGPT" = **Chatbot** (the interface) + **GPT** (the brains).

### How a large language model works (intuition)

- It reads your query as a **sequence of words**, where order carries meaning.
- It generates output **one word at a time**, using what came before to **predict the next word**. Think of it as a **massive auto-completion mechanism**.
- There's no clear threshold for "large". Once models reach billions of parameters and train on billions of records, they're considered LLMs.
- LLMs are **neural networks** (deep learning). Other types include **CNNs** for images and **RNNs** for sequential data.
- **The breakthrough (around 2016–2017):** the **transformer**, a sequence-to-sequence architecture that uses **attention** to focus on the most important parts of the input. Before it, language models were rather primitive.
- ChatGPT's interface is **optimized for dialogue** and includes **content filters**.

---

## 4. Prompt engineering use cases by role

**Who can use prompt engineering? Everyone with a task to accomplish.**

| Role | How prompt engineering helps |
|---|---|
| **Software engineers** | Generate code (e.g. read a file and filter records for active members), often usable as-is for simple cases; **explain** unfamiliar code; **debug** by pasting in problem code; **optimize** performance; **migrate** code between languages (Java → Python, Python → Go, …) |
| **Managers and tech leads** | Generate custom **reports and summaries**; feed in data and inputs to support **decisions**; help with **troubleshooting and debugging** |
| **Marketing professionals** | Ideas for **social media posts and campaigns**; **SEO keywords** for blog posts; **ad copy** and creatives; **targeted, personalized marketing emails**. The value is a **starting point** you then refine with your own "secret sauce". |
| **Sales professionals** | **Prospecting and lead generation** ideas; **presentations and proposals**; personalized **follow-up messages**; **sales scripts**; content for **brochures and collateral**; **competitor analysis** and sales insights |
| **HR professionals** | **Candidate screening** (extract keywords and skills from resumes); **onboarding and training** materials (building on existing ones); **survey templates** for morale; personalized **employee recognition** messages |

---

## 5. ChatGPT

### Getting set up (as shown in the course)

- Go to **chat.openai.com** → **Log in** or **Sign up**. You can sign up with an email address, or with a **Google, Microsoft, or Apple** account.
- You'll be asked for your name and **date of birth** (to verify you're not underage), and to **verify a phone number**. One phone number can be linked to **at most two** ChatGPT accounts.
- A **puzzle** checks that you're human.

**ChatGPT's own tips when you start:**
- It can answer questions, help write code, brainstorm, and more.
- **Don't share sensitive or confidential information.** What you type may be used to train the model, which is a real concern inside organizations.
- **Check your facts.** It can give inaccurate answers.

### The interface

- A **text box** at the bottom for prompts.
- **Sessions:** A session is a back-and-forth conversation on one topic. ChatGPT **remembers context within a session**. Sessions appear in the left sidebar (which can be collapsed), where you can **rename** them.
- **Free plan:** runs on **GPT-3.5**. You can chat as much as you like, unless the servers are busy (common during the US daytime). The course says the model has **175 billion parameters**. *(The transcript says "GPT-5" here, which appears to be a slip for GPT-3.5.)*
- **ChatGPT Plus (~$20/month):** access to **GPT-4**, which is more powerful and nuanced, trained on newer data, gives longer and more accurate answers, and is less prone to hallucination. You also get **priority access** to servers.
- **Custom instructions:** tell ChatGPT about yourself (your situation, work, interests) and **how it should respond** (tone, short or long answers, what to call you).
- **Settings:** **theme** (System, Dark, Light); **data controls** (chat history and training on/off, shared links, export data, delete account).
  - *The instructor's practice:* She leaves chat history on, never shares information proprietary to her organization, and deletes chats she no longer needs.

### Lessons from the ChatGPT demos

**1. Open-ended prompts get broad answers. Specific prompts get specific answers.**
- *"Best programming language for beginners?"* → a long, comprehensive list (Python first, then JavaScript, Java, C#, Swift, Go, …), ending with "it depends on your goals".
- *"…if I'm planning to work with data?"* → more specific: **Python**, with a mention of **R**.
- *"…if I'm planning to build a server-side backend?"* → different recommendations. ChatGPT picked up on the new use case.

**2. Output is stochastic.** You may not get the same answer the instructor got. LLM output is **probabilistic, not deterministic**. It's not like 2 + 3 always giving 5. Structure, phrasing, and some content can differ.

**3. Context lives inside a session.**
- In the *same* session, the data question got "Python". In a **new chat**, the same question got a broad overview (SQL, Julia, Scala, MATLAB, SAS, …), because the earlier context was gone.
- **New York example:** After asking about things to do in New York, the follow-ups "*Do you have suggestions for good places to eat?*" and "*How will I commute within the city?*" were answered **specifically for New York**, even though New York wasn't mentioned again.
- The same "good places to eat?" question in a **new chat** gave a scattered, **US-centric** answer (New York, San Francisco, Chicago, delivery apps). The instructor links the US focus to the training data.

**4. Knowledge cut-off.** Asked about **Nvidia's latest earnings** and the **2023 US heatwave**, free ChatGPT (GPT-3.5) apologized: it has no real-time data and can't discuss events after **September 2021**, because its training data ends there. It's **not good for current events**.

---

## 6. Google Bard

### Background (as told in the course)

- ChatGPT's popularity caught Google off guard. In **December 2022**, Google executives declared a **"code red"**, fearing the impact on Search and Microsoft's partnership with OpenAI.
- The **transformer** technology behind ChatGPT originated at Google (a 2017 paper). Google had the technology but hadn't released a chatbot.
- **Bard launched in February 2023** (announced **February 6, 2023**), one day before Microsoft announced Bing's ChatGPT integration.
- **Models:**
  - Bard was first powered by a lightweight version of **LaMDA** (Language Model for Dialogue Applications, launched 2021). It had glitches and factual errors, and Google got criticism.
  - Bard is now powered by **PaLM 2** (Pathways Language Model version 2). It's trained on **100+ languages** and domains such as math, science, programming, and literature, using a **curated dataset** that filters out spam, hate speech, and other low-quality or harmful text.
  - PaLM 2 uses **Pathways Learning**, which combines information from multiple sources coherently. It's Google's own proprietary model, architecturally different from GPT, though **both are transformer-based**, and they were trained on different data.
- **Access:** **bard.google.com**, with a **Google account required**. It once had a waiting list; it's now freely available.

### The interface

- A text box with a **microphone** for spoken prompts.
- **Sessions** with memory, shown in the left sidebar.
- Clearly labeled as an **Experiment**: it can be wrong, so verify with other sources.
- **Warning:** **Human reviewers may process** your conversations, so **don't enter sensitive info**.
- Settings at the time had only a **dark/light theme**, with no custom instructions like ChatGPT.

### Features and observations from the demos

| Feature | What the course showed |
|---|---|
| **More succinct, directed answers** | "*I've never coded before. What is the best programming language for me to learn?*" → a clear opinion: **Python**, with reasons. (The added context "never coded before" may have helped.) The instructor's personal experience is that Bard is **less chatty** than ChatGPT. |
| **Helpful links** | Bard offers more links for follow-up, which she sees as the influence of Search |
| **Feedback buttons** | Good response / Bad response (ChatGPT has similar options) |
| **Modify response** *(not in ChatGPT)* | **Shorter, Longer, Simpler, More casual, More professional**. "Simpler" kept the content but used easier words and explained terms like "versatile". |
| **Google it** | Jump to related **Google searches** if you're not satisfied |
| **View other drafts** | Bard may generate **multiple drafts** (e.g. 3). You can pick one or regenerate. Most useful for technical subjects. |
| **Images with sources** | "*Which database should I use?*" → database types, each with an **image and a link** to where it came from. Citing sources is a hard problem for chatbots, and this is an important step forward. |
| **Writing emails** | "*I need to write an email apologizing for missing a deadline*" → a well-written draft plus tips. Adding context ("had to work on a higher priority project") tailored it. **More professional** (e.g. for a VP) and **More casual** (for a friend) rewrote the tone, and Bard **listed what it changed** (formal language, no contractions, active voice, …). Always **proofread**. |
| **Current events** | Answered about the **2023 US heatwave** and **Nvidia's latest earnings** (released 15–20 days before recording), an advantage over free ChatGPT |
| **Summarizing links** | Summarized a Steve Jobs biography from **britannica.com** from its link. Free ChatGPT said it **couldn't access external websites** (but could give a biography from its training data). |

**Takeaway:** ChatGPT and Bard use different models and data, so they often give **different responses**. If one doesn't help, try the other. **Diversity in your toolkit** helps.

---

## 7. Bing Chat

### Background (as told in the course)

- Bard was announced **February 6, 2023**, and **Bing Chat launched February 7, 2023**.
- Microsoft was an early investor in OpenAI and invested roughly **10 billion** more after ChatGPT's release, gaining access to OpenAI's models.
- **Bing Chat runs on GPT-4**, which you'd otherwise pay for in ChatGPT. On Bing it's **free**.
- **GPT-4 vs. GPT-3.5:** described as more reliable, creative, and collaborative; better with nuanced instructions; and able to handle a **much larger context**, so it can process longer text in one request.
- **Access:** **bing.com → Chat**. You can use it **without logging in** for a limited number of responses (**5 per conversation**), then sign in with a **Microsoft account**.
- **Extras over ChatGPT (at the time):** **recent events**, **cited references**, and the ability to work with **images**.
- It also uses **sessions**. Click **New topic** to start one.

### Conversation styles and temperature

Bing (in Preview at the time) let you **choose a conversation style**:

| Style | Temperature | Best for |
|---|---|---|
| **More Creative** (purple) | **Higher** | Ideation: picnic or party ideas, poems. More varied, but possibly **less accurate**. |
| **More Balanced** (blue) | **Middle** | **Most common use cases**: some creativity, pros and cons |
| **More Precise** (green) | **Lower** | **Facts**, **math and logical reasoning**, **code**, SQL queries, fact-based **current data** |

**What is temperature?** A **hyperparameter that controls the randomness and creativity** of generated text.
- A generative model produces text **one word at a time**, choosing the next word from **probabilities** over all possible next words.
- **Higher temperature:** it also picks **lower-probability words**, so output is more random and creative.
- **Lower temperature:** probabilities are "**sharpened**", so it picks the **higher-probability** words, giving more deterministic, less creative output.

### Observations from the demos

**References everywhere (Balanced mode).**
- "*If I'm a beginner programmer, what programming language should I start with?*" → a greeting, a succinct answer (Python first, then C++, Java, …), and **superscript reference numbers** linking to sources (including a Codecademy blog post that directly answered the question).
- Neural networks are often **black boxes**, so **attribution is hard**. The instructor mentions lawsuits from content creators seeking attribution and payment. Bing's references are "not perfect yet" but "an amazing start".
- Bing also **suggests follow-up questions** (e.g. "How long does it take to learn programming?", "Which language is most in demand for jobs?").

**Precise mode:**
- "*Third president of the USA?*" → **Thomas Jefferson** (1801–1809), with 4 sources (mostly Wikipedia) and an image.
- "*Current Prime Minister of India?*" → **Narendra Modi**, citing pmindia.gov.in.
- **Math:** "*Two trains are 5 km apart, travelling at 50 km/h and 100 km/h toward each other. How long until they meet?*" → it reasoned **step by step**: relative speed is the sum, 150 km/h, and 5 km ÷ 150 km/h = **2 minutes**. Earlier models struggled to show their working and often got math wrong.
- **Latest data:** Microsoft's latest earnings (results from June 30).
- **Code:** "*Write Python code to sum all numbers in a list*" → a short function using Python's **built-in `sum`**. (The first try produced no response. Chatbots sometimes fail, so just try again.)

**Creative mode:**
- **Same fact question** (third president) → still correct, but richer: a Founding Father, a principal author of the Declaration of Independence, came after George Washington and John Adams, and **died on July 4th, the same day as his friend and rival John Adams**.
- **Same code question** → a function that **loops** through the list to add the numbers (no built-in `sum`), with a comment on every line and a longer explanation. Nice, but overdone for a simple task.
- **Poem:** "*Write a poem extolling the virtues of Python as a programming language*". Creative mode shines here. Precise mode would use fewer kinds of words.

**Link summaries:** Bing could summarize the britannica.com Steve Jobs article from its link, unlike free ChatGPT.

**Summary of Bing vs. ChatGPT (at the time):** recent news and events, summarizing links, working with images, and a more powerful model (GPT-4) **for free**.

---

## 8. Perplexity AI

### What it is (as described in the course)

- An **AI chat-based conversational search engine** that answers questions using LLMs.
- Microsoft and Google aren't the only players, but they have the money and computing power to train LLMs. Perplexity is one of the "other horses in this race".
- Built on the **same technology as ChatGPT**: by default it uses **GPT-3.5** (the free ChatGPT model), but it's trained specifically as a chatbot and may give better results in some cases.
- **Design philosophy:** ChatGPT is a traditional chatbot (plug-ins can be installed). Perplexity is built **more like a search engine**: it searches the web **in real time**, gives **suggestions and sources**, and provides **up-to-date** information.
- **Layout:** like Google Search, with a central "Ask anything" box.
- **Sign in:** with Google, Apple, or email.

### Plans and limits (at the time of recording)

| | Free | Pro (~$20/month or $200/year) |
|---|---|---|
| **Default model** | GPT-3.5 | Can upgrade to **GPT-4** or **Claude 2** |
| **Copilot** (runs on GPT-4) | About **5 queries every four hours** | **300+ per day** |
| **File upload** | Available (up to **25 MB**, **3 uploads per day**) | Unlimited |

- **Claude 2** is described in the course as an LLM chatbot by **Anthropic** (an AI research company in San Francisco), said to be strong in **coding and math**.
- **For comparison:** GPT-4 on paid ChatGPT was limited to **25 prompts every three hours**. These limits exist because there aren't yet enough servers running these models.

### Features and observations

- **Search results built into answers:** a **Quick Search** strip of links plus a natural-language answer with **numbered references** (e.g. reference 3 led to a Codecademy article on easy languages to learn).
- **Copilot** considered **8 sources** versus about 5–6 in regular mode, giving a more comprehensive and specific answer.
- **Follow-up suggestions** ("Related"), similar to Bing Chat.

**Focus modes:**

| Focus | What it searches |
|---|---|
| **All** | The entire internet |
| **Academic** | Academic papers |
| **Writing** | Generates text or chats **without searching the web** (pure generation) |
| **Wolfram\|Alpha** | Wolfram Alpha's computational knowledge engine |
| **YouTube** | Answers in **video** form |
| **Reddit** | Reddit |

- **YouTube focus:** "*Good resources for learning cooking?*" → well-known cooking channels plus a text summary. A follow-up on essential cooking tools linked each tool to a video.
- **Academic focus:** "*Applications of generative AI*" → sources from **arXiv**, **Semantic Scholar**, and the **National Library of Medicine** (e.g. a paper on generative AI in medical imaging; *Business (mis)Use Cases of Generative AI* on arXiv). It's more focused than Google Search and adds a natural-language summary.

**PDF Q&A:** The instructor uploaded a short story PDF that ChatGPT had generated for her, *The Wise Old Tree and the Curious Squirrel*.
- "*Who is Sammy?*" → correct (a curious young squirrel), with extra context from the document.
- A vague follow-up, "*Who does he learn the secret of happiness from?*", was understood thanks to the session context, with a reference pointing to the PDF.
- "*What is the secret of happiness based on this story?*" → a correct answer.
- **Real-world use:** parsing complex **contracts** and asking questions about them. At the time, ChatGPT couldn't do PDF Q&A directly.

---

## 9. Quick comparison (as of the course recording)

| | ChatGPT (free) | Google Bard | Bing Chat | Perplexity AI (free) |
|---|---|---|---|---|
| **Maker** | OpenAI | Google | Microsoft | Perplexity |
| **Model** | GPT-3.5 (GPT-4 on Plus) | PaLM 2 (earlier LaMDA) | GPT-4 | GPT-3.5 (GPT-4 via Copilot) |
| **Account** | Email / Google / Microsoft / Apple + phone | Google account | Optional at first (5 responses per conversation), then Microsoft account | Google / Apple / email |
| **Current events** | No (cut-off Sept 2021) | Yes | Yes | Yes (real-time web search) |
| **Cites sources** | No | Links and image sources | Yes, numbered references | Yes, numbered references + quick search |
| **Reads links** | No | Yes | Yes | — |
| **Special features** | Custom instructions, data controls | Modify response, drafts, Google it, voice input | Creative / Balanced / Precise styles, follow-up suggestions | Focus modes, Copilot, PDF upload, follow-up suggestions |

---

## Practical tips from this course

- **Give context and constraints:** your level, your use case, the format, the tone.
- **Use sessions on purpose.** Keep related questions in one session, and **start a new chat** for a new topic. **Name** important sessions.
- **Follow-up questions work** within a session, even without repeating context.
- **Match the mode to the task:** precise for facts, math, and code; creative for ideas and poems; balanced for most things.
- **Use more than one tool**, because they differ.
- **Never paste sensitive or proprietary data**, and **always verify and proofread**.
- If a chatbot gives no response, **just try again**.
- These tools **change quickly**. What's true today may not be true tomorrow.

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **Prompt** | A natural-language question or instruction describing the task |
| **Prompt engineering** | Designing, refining, and optimizing prompts to get the desired output |
| **Text-to-text model** | A model that takes text in and produces text out |
| **In-context learning** | A model learning from context provided in your prompt or session |
| **Session** | A back-and-forth conversation the chatbot remembers; context doesn't carry to new sessions |
| **Stochastic / probabilistic output** | The same prompt may produce different responses |
| **Hallucination** | A model giving a wrong answer while firmly believing it's correct |
| **Prompt hacking / injection** | Using prompts to produce unwanted or harmful behavior |
| **Jailbreaking** | Bypassing a model's restrictions to access or misuse it |
| **Knowledge cut-off** | The date after which a model has no training data (Sept 2021 for free ChatGPT, per the course) |
| **Temperature** | A hyperparameter controlling randomness and creativity: higher = more creative, lower = more precise |
| **Copilot (Perplexity)** | Perplexity's GPT-4-powered mode, which searches more sources |
| **Focus mode (Perplexity)** | Restricts search to a source type: All, Academic, Writing, Wolfram\|Alpha, YouTube, Reddit |

---

*Source: course transcript "Getting Started with Prompt Engineering" (15 videos). All product details are as described when the course was recorded and may have changed since.*

[← Previous chapter](04-deep-learning-and-neural-networks.md) · [Back to contents](../README.md) · [Next chapter →](06-exploring-prompt-engineering-techniques.md)
