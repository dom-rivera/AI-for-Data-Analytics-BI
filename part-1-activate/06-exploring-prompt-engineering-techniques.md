# Chapter 6 · Exploring Prompt Engineering Techniques

**Part 1 — Activate** · Instructor: Janani Ravi · [← Previous chapter](05-getting-started-with-prompt-engineering.md) · [Back to contents](../README.md) · [Next chapter →](07-case-studies-in-prompt-engineering.md)

> **About this chapter:** This course is mostly hands-on demos in ChatGPT (GPT-3.5), Google Bard, Bing Chat, and the OpenAI Playground (GPT-3.5 Turbo, GPT-4, and legacy models). This chapter keeps the **techniques, example prompts, and observations**. Tool behavior is recorded as it was at the time of recording.

---

## At a glance

- A prompt has **four elements**: **instruction** (the only required one), **context**, **input data**, and **output format**.
- Improve prompts with **role playing, iterative refinement, constraints** (phrased **positively**), and **feedback loops**. More advanced options are **zero-shot, few-shot, chain-of-thought, and augmented knowledge** prompting.
- **Five prompt categories:** open-ended, close-ended, multi-part, scenario-based, and opinion-based.
- **Prompt types by output:** facts and explanations, summarization, classification (including sentiment analysis), extraction, question answering, writing (grammar and tone), ideation and roleplay, and reasoning (mathematical, logical, predictive).
- **Separate instructions from input text** with `###` or `"""`.
- **Always double-check** responses. Models can hallucinate, and even strong models sometimes get reasoning wrong.

---

## 1. Prompt crafting

You already know prompting. To get the **most relevant, coherent** response, though, you need to **design** your prompts so the model has everything it needs.

**Subtleties and nuances matter.** One word can change everything: "Describe the Taj Mahal" vs. "Describe the **history** of the Taj Mahal". The model only gets cues from your query, so **every bit of information counts**.

### The anatomy of a prompt

| Element | What it is | Example from the course |
|---|---|---|
| **Instruction** *(required)* | The core directive: what you want the model to do | "Summarize this text." / "Explain this bit of code." |
| **Context** | Background that helps the model tailor its answer | "Given the fact that I'm going to be working on terabytes of data, should I work with a SQL or NoSQL database?" |
| **Input data** | Data for the model to process (a paragraph, code, CSV records, …) | The text to summarize; the buggy code to debug |
| **Output format / indicator** | The format or tone of the response | Java code, JSON data, "a limerick in the style of William Shakespeare" |

### Techniques to improve prompts

- **Role playing (personas):** Ask the model to act as a librarian, teaching assistant, or comedian. For an abstract explanation, ask a "physicist" or "grammarian". For a simpler one: "*Explain this like you were a high school teacher explaining to high school students.*"
- **Iterative refinement:** Your first prompt is rarely perfect. Start **broad**, then **zoom in** on the direction you want based on the responses.
- **Constraints:** Bound the response, e.g. "*Please use three bullet points to summarize this text.*" Models (especially the one behind ChatGPT) **don't work well with negative constraints**. Say "*Use just three bullet points or fewer*", not "*Do not use more than three bullet points.*"
- **Feedback loops:** Use earlier responses to adjust later prompts.

### More advanced techniques

| Technique | What it involves | Example |
|---|---|---|
| **Zero-shot** | No examples; the model relies on what it learned in training. This is what you usually start with. | "Summarize [text]." / "Recommend some books to me." (with nothing about your taste) |
| **Few-shot** | Give a few examples (**shots**) to guide the response | "Here are some movies that I've liked in the last 3 or 4 years, please recommend some new movies for me to watch." |
| **Chain-of-thought** | Break a complex task into **intermediate reasoning steps** for the model to follow | The instructor finds it very useful for **complex math** and **step-by-step code generation** |
| **Augmented knowledge** | Give the model **relevant facts** to base its response on | — |

### A process for engineering prompts

1. **Start with a reasonable prompt.**
   - Use precise, clear language (ambiguous prompts get very broad responses).
   - Assign **roles or personas** for a particular style (e.g. a fifth-grade teacher, a journalist).
   - Use **constraints** to keep the model on track.
   - Make sure your cues **don't mislead or bias** the model.
2. **Use a feedback loop:** draft → generate and test → **evaluate** against your objective → **refine**. Repeat as needed.
3. **Calibrate and fine-tune:** use few-shot or chain-of-thought prompting, and if you can access the **model's parameters**, tune them.

### Best practices for prompt design

- **Use the latest model.** Newer models are more versatile and less likely to get things wrong. GPT-3.5 is the free version; **GPT-4** is better and less prone to hallucinations.
- **Separate instructions from context** with a delimiter such as `###` or `"""`.
- Be **specific, descriptive, and detailed** about the context, outcome, length, format, and style.
- **Examples help.** The model will mimic an example output quite faithfully.
- **Start with zero-shot.** If that doesn't work, add examples (**few-shot**), then fine-tune.
- Keep descriptions **crisp, clear, and unambiguous**.
- **Say what to do**, not what not to do (positive constraints).
- **For code generation, use leading words:** `import` nudges toward **Python**, and `SELECT` toward **SQL**.

---

## 2. The elements of a prompt in action

**Instruction only** gives general answers. These are fine for **ideation**, but not for decisions:
- "*Please recommend a code editor I can use*" → very general (an **open-ended** prompt).
- "*Please write an email asking for leave*" → a generic email. It's a good starting point, but not tailored.
- "*In what format can I store data?*" → "a world of answers": file formats, databases, even HDF5.
- "*How do I get data from a store?*" → file systems, relational and NoSQL databases, web APIs, message queues, …
- "*Please generate some data for employees*" → ChatGPT picked **JSON** and random fields. If you wanted CSV, you should have said so up front.

**Adding context (+ instruction):**
- "*Our team is planning a project in Python. We need to be able to prototype easily. The IDE should not be platform dependent. Please recommend an IDE.*" → an **actionable** answer: **PyCharm**.
- The same prompt with **GPT-4** in the OpenAI Playground → **Jupyter Notebook** (great for prototyping) *and* PyCharm. The instructor found this more useful; GPT-4 understands nuance better.

**Adding an output format:**
- "*I need to store some structured data using the file system. The data should be in the form of records and should be easily read into a Python or Java program. What format can I use?*" → JSON, XML, protocol buffers, CSV. All fit, but there were many options because the format was still loose.
- A **more specific** format: "*I need to retrieve data from a MySQL database. I need all the fields. The table is called reports. How can I retrieve this data using a SQL query?*" → `SELECT * FROM Reports;` plus an explanation. **Directly usable.**
- **Context + instruction + format:** "*Our office is celebrating learning with a series of sessions with famous educators and technology specialists. Could you please write a tweet celebrating Wellness Week at Skillsoft with the appropriate hashtags?*" → a complete tweet with hashtags.

**Adding constraints (positive vs. negative):**
- Leave request for a half-day medical appointment + "*Do not make the email very long*" → it still works, but the constraint is **negative**.
- Better: "*Since it's a professional email please keep it short and courteous.*" **Ask the model to do something**, not to avoid something. The instructor has found the model does better this way.

**All the elements together:**
- **Test data:**
  - *Context:* employee data for a database table, with fields name, title, department, salary, and years in position.
  - *Input data:* two example records.
  - *Instruction + format + constraint:* "*Please generate 10 records in the CSV format.*"
  - → Exactly what was wanted.
- **A function:**
  - *Context:* summing the elements in a list.
  - *Instruction:* write a function.
  - *Input data:* the signature `compute_sum(input_elements)`.
  - *Output format:* Python.
  - *Constraints:* "*use meaningful variable names and do not use the built-in sum function*".
  - → Exactly what was wanted. The instructor notes "*avoid using the built-in sum function*" would have been a better (positive) way to say it.

**Personas:**
- "*As a programming instructor, please explain the collections API in Java to a beginner learning Java.*" → simple terms, clear explanation, and an example.
- Playground, legacy Completions mode: "*As an AI engineer, please explain what generative AI is to my grandma.*" → a simple explanation.
- Playground, Chat mode, **System** set to "*You are a book reviewer*", then "*Please review … Harry Potter and the Philosopher's Stone*" → a good review analyzing the story and characters.

---

## 3. Five prompt categories

The instructor notes this categorization came from a blog or article she found interesting. It's **not the only way** to categorize prompts.

| Category | What it is | Best for | Examples from the course |
|---|---|---|---|
| **Open-ended** | No specific direction or constraints. Answers are **subjective**. | Ideation, exploration, creativity, brainstorming. *Not* for specific answers. | "*What do you think is a good technology that we can use to build frontend UIs?*" (10 options); "*What are some of the data storage applications I can use?*"; Bard: "*How can I run applications on the cloud?*"; Playground at **temperature 1.11**: "*What are the characteristics of a brave person?*" |
| **Close-ended** | Constraints or guidelines **direct** the answer. Usually **objective**. | Specific information; limiting choices; no exploration | "*What is the data warehouse I can use on the GCP?*" (BigQuery first, all GCP options); "*How do I use event driven compute on AWS?*"; "*How do I create a VM on Azure?*"; "*What countries border India?*" |
| **Multi-part** | Several **interconnected questions** chained in one prompt | Complex issues, deeper thinking, comprehensive answers | "*Suggest some technologies I can use for data visualization and list their strengths and weaknesses*"; "*Could you please highlight the features of Java and Python … compare them based on performance and ease of use?*" (features of each, then a comparison) |
| **Scenario-based** | Describe a **situation** first, then ask for a response in that context | Problem-solving; hypothetical situations | "*I'm hosting a birthday party. They are all between 11 and 13 years old … what should I organize? What food…?*" (tailored ideas, plus a reminder to involve her son in planning); "*I have a lot of raw data … my team does not know how to code. Suggestions for how to preprocess and analyze this data?*" (Excel, SPSS, AutoML, grouped into no-code and low-code tools) |
| **Opinion-based** | Ask for the model's **opinion** on a topic | Exploring the values it expresses; testing your critical thinking; hearing the opposing view | "*What do you think of generative AI? Do you think it will improve our lives?*" (positives *and* concerns); "*What do you think of e-learning? Do you think it improves learning outcomes?*" (advantages *and* challenges) |

**Tip from the demos:** The instructor **renamed each ChatGPT session** after its category (open-ended, close-ended, …) to keep things organized.

---

## 4. Fact-based and explanation-based prompts

**Fact-based prompts** ask for **objective, verifiable** information grounded in established knowledge, not opinions or interpretations. You can check the answer against other sources. They're usually the **easiest** for chatbots to get right.

| Prompt | Result |
|---|---|
| "*Which is the largest state by area in the United States?*" | **Alaska** |
| "*Which state has the largest GDP in the United States?*" | ChatGPT: **California**, with its **September 2021** caveat. Bard: **California**, more confidently (more up-to-date data), and it also **ranked states by GDP and per-capita GDP**. |
| "*What are the largest exports for China?*" | A list of exports with values in billions of dollars |
| "*I need to retrieve data from a REST API. What kind of HTTP request will allow me to do this?*" | **HTTP GET**, with more detail |
| "*My organization is storing data on AWS using S3 buckets. What is the Python library that will allow me to access this data programmatically?*" | **Boto3** |

**Explanation-based prompts** ask for a **detailed explanation**: the context, the rationale, or a step-by-step walkthrough. They are grounded in fact but go deeper, combining facts, theories, and examples.
- "*Could you explain the dictionary data structure in Python?*" → a clear, verifiable explanation.
- "*Could you explain how the limit clause works in SQL?*" → a detailed, step-by-step walkthrough.

### Shaping the "I don't know" answer

You can tell the model **how to respond when it doesn't know**:
- "*What's the top grossing movie in the year 2019?*" → **Avengers: Endgame** (it has data for 2019).
- "*…in the year 2023?*" → the usual apology about September 2021.
- "*What is the top grossing movie in the year 2023? Respond with, 'I'm afraid I do not know this answer' if you actually don't know the answer.*" → exactly that polite line, with no extra explanation.

---

## 5. Summarization prompts

**Summarization prompts** ask for a **condensed version** of information, events, or concepts. They capture the key points in a shorter, digestible form. **Uses:** understanding the core message quickly, simplifying complex ideas, and highlighting important facts.

### Techniques shown

**1. A basic summary.**
- *Prompt:* "*Could you write a concise and comprehensive summary of …*" plus a pasted paragraph from a National Library of Medicine article (the section "Ethics and rules of using text from ChatGPT").
- *Result:* a good summary covering the plagiarism concerns and how two journals responded: **Science** is against using these tools, and **Nature** gave guidance on LLM use.

**2. Use a delimiter.** Put `###` between the instruction and the input text so the model clearly knows which is which.

**3. Be specific about the kind of summary.**
- "*Could you summarize this text using a single sentence?*" `###` [text] → a one-line summary.
- "*…using three bullet points?*" → a **balanced** summary, not too long or short.

**4. Summarize from a link (Bing Chat).** ChatGPT couldn't read links, but Bing could. Bing's summary of the whole section was decent but, in the instructor's view, **missed the main point** (that the section was about using ChatGPT as a writing tool).

**5. Technical text.** "*Could you summarize this in 3 bullet points?*" `###` [C++ docs on variables and memory addresses] → three good bullet points.

**6. Target an audience.**
- Summarize the C++ text **for a 7-year-old**:
  - **ChatGPT:** memory is like "a big, long line of boxes"; variables are things like a score or a color.
  - **Bard:** memory is like **houses**, and addresses are **house numbers**.
- These techniques work across ChatGPT, Bing Chat, and Bard.

**7. Title generation.**
- *Prompt:* generate a title, with `"""` as the delimiter (also acceptable).
- **ChatGPT**, in the same session as the 7-year-old summary, gave a child-friendly title ("*Understanding how computers remember the magic of variables and memory addresses*"). It **carried over the session context**.
- **Bard**, in the same kind of session, **did not** pick up that context and gave adult-oriented titles.

**8. Summarize a conversation.**
- Put a long, multi-paragraph customer–support chat (about a food order arriving cold) **inside `"""`** so the model knows where it starts and ends.
- **GPT-3.5:** brief and to the point. It kept the essence but lost some nuance.
- **GPT-4** in the Playground (**System:** "summarize", **temperature 1.11**): **longer and more nuanced**. That may partly be due to the higher temperature.

*The course description also mentions **extractive** summaries alongside **abstractive** ones. The demos show summaries written in the model's own words.*

---

## 6. Classification prompts

**Classification prompts** ask the model to **categorize or label** items, concepts, or information based on criteria. They range from simple (fruits vs. vegetables) to complex (diseases by symptoms and causes), and are used in research, data analysis, and decision-making.

### Sentiment analysis with zero-shot prompting

"**Zero-shot**" here means the model performs the task **without being specifically trained** for it. (The instructor points out we've been using zero-shot prompts all along.)

| Prompt | Result |
|---|---|
| "*Classify this review*" + a *Top Gun: Maverick* review | **Generally positive**, with an explanation |
| "*Classify this review*" + a negative review | **Negative / critical** |
| "*Classify this review: movie was okay, the actors were decent*" | **Lukewarm / neutral** |

ChatGPT used the three standard sentiment classes (**positive, negative, neutral**) without being told about them.

### Guiding the output

**Specify your own classes.** "*Classify this review as one of: Amazing, Positive, OK, Negative, Horrible*" → **Positive** (not Amazing).

**Few-shot: add an example and an output structure.**
- The prompt includes one example (*Text:* "The movie was decent and worth the money" → *Sentiment:* OK), followed by *Text:* [new review] → *Sentiment:* [left blank].
- **Few-shot prompting** gives the model a small number of example prompts and responses (**shots**) to show it the task.
- **Results:**
  - ChatGPT gave the right labels ("OK", then "Positive"), but **didn't always follow the `Sentiment:` format**. "Sometimes it does, sometimes it doesn't." More shots may help.
  - **Bard** gave the same classifications with **more explanation**, plus a **summary table** you can **export to Google Sheets**.
  - Bard also searched the web and **identified the website** the negative review came from.

### Beyond sentiment: custom categories

**Support tickets for a food-ordering app**, classified as **delivery, product, or support**:

| Ticket | Category | Reasoning |
|---|---|---|
| "*My order came in very late and the food was cold*" | **Delivery** | The order arrived late |
| "*I had ordered burgers and fries, but only received the burger*" | **Product** | More likely the restaurant forgot the fries than the delivery agent |
| "*I tried calling the help desk, but no one responded to my query in time*" | **Support** | The help desk didn't respond |

**Few-shot technology classification** (programming language vs. database):
- Several examples were given first, then: **MongoDB, Fortran, Go, Couchbase**.
- **ChatGPT:** all correct, in the requested format.
- **Bard:** all correct, in a **table** that also included the original examples.

### A hallucination check

A made-up technology, **"NonameDB"**, was added to the list:
- **ChatGPT** correctly said it **doesn't recognize** NonameDB and couldn't categorize it.
- **Bard** searched online and claimed it was an **upcoming database**. The instructor couldn't find any such technology, so this may be a **hallucination**.

> **Lesson:** Generative models can make things up. **Double-check research** against other sources.

---

## 7. Extraction prompts

**Extraction prompts** pull **specific pieces of information** out of text you provide. They're highly focused, and useful for large, complex, hard-to-read documents such as **legal documents**, or for listing kinds of terms used in an article.

**Example 1: Entities from a Wikipedia article (Bill Gates).**
- *Prompt:* "*Identify people, companies, products, places, and general themes from this article*".
- **ChatGPT:** About 50% of the article was **too long** and caused an error. With a **shorter** excerpt it did well:
  - People: Paul Allen, Ray Ozzie, Craig Mundie, …
  - Companies: Microsoft first
  - Products: Altair, MS-DOS, Windows
  - Places: Seattle; Albuquerque (where Microsoft was founded)
  - Themes: entrepreneurship first
- **Bing Chat**, given just the **link**, extracted more places (e.g. Sub-Saharan Africa, India) and, in the instructor's view, **better products** (Windows, Office, Xbox, Surface).
- **Bard**, also with the link, did **better than ChatGPT** and was comparable to Bing. It included the Bill and Melinda Gates Foundation; Windows and Office; and Seattle and Medina.
- Overall, ChatGPT without link parsing came out worst. *(The transcript says "ChatGPT with GPT-5" here, which appears to be a slip for GPT-3.5.)*

**Example 2: Resume parsing.**
- *Prompt:* extract **companies, education, degrees, and skills**, each as a **bullet list**, from a plain-text resume. (She added a second university to vary it.)
- *Result:* neatly bulleted lists, including both universities and both degrees. **Very useful for recruiters.**

**Example 3: Blog keywords.**
- *Prompt:* a Skillsoft blog post on the **skills gap**, plus "*generate only the five most important keywords*". (Without the limit, you'd get a useless list of 20.)
- *Result:* AI and ML, skill gaps, executive leadership, workforce development, …

**Example 4: Hashtags.** The same blog, with a different extraction: "*Extract ten hashtags that can be used to promote this blog on Twitter.*"

**Example 5: Structured specs.** A plain-text product spec from Amazon, extracted into **JSON**: brand, model, RAM, storage, keyboard, and more.

---

## 8. Question-answering prompts

**Question answering** is a type of extraction: the answers are **in a document you provide**, and you ask questions about it.

**A note about peak times:** During **morning US time**, free ChatGPT's servers were overloaded, with slow or no responses. The instructor switched to the **OpenAI Playground with GPT-4**.

### The technique

1. Tell the model to **answer only from the text** you provide.
2. Separate that text with `###`.
3. Then ask your questions.

*If the model starts generating its own questions or a summary right after you paste the text, delete that response and just ask your question.*

**Example 1: Reserve Bank of India regulations** (the RBI is India's central bank, equivalent to the US Fed). Section B.1 on overseas investment by Indian companies was pasted in (GPT-4).
- "*What is the total financial commitment that the Indian party can make for an overseas direct investment?*" → **Not exceeding 400% of the Indian party's net worth.** ✔ Confirmed in the source.
- "*How much time does the Indian party have to report an acquisition to the RBI?*" → **Within 30 days of the transaction.** ✔ Confirmed.

**Example 2: Wi-Fi router troubleshooting (Bing Chat).**
- *Source:* this example comes from Google Cloud's prompt samples page.
- The docs describing each light color were separated by `###`, followed by: "*What should I do to fix my disconnected Wi-Fi? The light on my Google Wi-Fi router is yellow and blinking slowly.*"
- *Result:* **check the Ethernet cable** and that things are turned on. Correct, without reading the docs yourself.

**Example 3: Proving it uses only your text (Instacart IPO).**
- First, GPT-4 confirmed it **knew nothing** about the IPO (its knowledge was as of October 2021). The IPO was set for September 2023.
- Then a WSJ article was pasted with "*Please answer the questions I ask using only this information*":

| Question | Answer from the text |
|---|---|
| Target valuation? | Roughly **8.6 to 9.3 billion** |
| Higher or lower than earlier rounds? | **Lower**; it was previously valued at **39 billion** |
| Current CEO? | **Fidji Simo** |
| Plans for the funds raised? | Shares are sold by **employees and early stakeholders** so they can cash out |

> **Lesson:** Even a model with no knowledge of a topic can answer accurately **from background text you supply**.

---

## 9. Writing prompts: grammar and tone

**Writing prompts** inspire or guide writing. They're a **starting point** that helps generate ideas, focus thoughts, and spark creativity. The instructor often finds it hard to get started on writing, and uses ChatGPT or Bard for a seed.

**Types:**
- **Creative:** describing something that doesn't exist
- **Narrative:** telling a story
- **Expository:** explaining something
- **Persuasive:** convincing the reader of an opinion
- **Journaling, technical writing, and poetry**

### Proofreading

"*Proofread and correct the grammar and spelling mistakes in this email*" (an email with errors such as "in case questions"):
- **Bard** corrected it, **highlighted fixes in bold** (e.g. the misspelled "facilitate"), and **listed all changes**: verb tenses, spelling, more concise sentences, grammar. The instructor liked this best because **it explained the mistakes**.
- **Bing Chat** corrected it well but **didn't explain** anything.

### Generating text and controlling tone

**1. Basic.** "*Write an email requesting an update on the project schedule for the 'Green Trees' project, asking if the task will be completed on time for the next milestone*" → a reasonably good, generic email.

**2. Stern tone (added context).** "*Please make the email stern, since this is a subordinate who's been very lax, needs to buck up, and I'm planning to escalate.*" → strong wording: "I'm disappointed", "please take this seriously".

**3. Gentle tone.** "*Please make the email gentle, since this colleague is just back from bereavement leave and I don't want to put pressure on him but would still like the information.*" → soft and kind, but still asks for the update.

> Same request + **different context** = **very different tone**. This is what prompt engineering is about.

### Other writing examples

**Job posting for Skillsoft.**
- *Prompt details:* an engineer with 5–6 years of experience and full-stack project experience; Java, Python, SQL, NoSQL, JavaScript; a Bachelor's or Master's in Computer Science.
- *Result:* a strong draft. Bard also **added "Bengaluru, India"** as the location, which wasn't in the prompt. It took this from the **location in the instructor's Google account**. Bard uses information it has **about you**, not just your prompt.

**Ad copy** for a cloud security provider that works across all three cloud platforms and uses AI to track threats → copy full of superlatives, plus tips for writing ad copy.

---

## 10. Ideation and roleplay prompts

### Ideation

Before generative AI, you'd ideate with a colleague or friend. Now you can use **ideation prompts**. They tend to be **open-ended** ("blue-sky thinking") and are used for problem-solving, innovation, design, and strategic planning.

**Interview prep (Bing Chat).**
- *As the candidate:* "*I'm preparing for a system design interview. The job role is for building large scale streaming systems at a media company. What are the topics I should cover?*" → a comprehensive topic list **plus references**.
- *As the interviewer:* "*I'm going to be interviewing a candidate for a Python developer role. It's an entry level role, basic Python knowledge. Suggest some questions. The questions should cover concepts as well as coding.*" → Python questions plus links.

**Prompts the instructor suggests trying yourself:**
- **Problem-solving:** "*How can I reduce waste in the manufacturing process?*"
- **Design:** "*Design a public transport system.*"
- **Exploring concepts:** "*What are the different ways I can recycle paper?*"

**Project code names (and temperature).**
- *Prompt:* "*We're in the process of starting prototyping a new project for a music app, custom song recommendations. Could you suggest some code names for this project?*"
- **Bing (Balanced):** Melody, Rhythm, Harmony, Tune. Boring, and code names are usually quirky.
- **Bing (More Creative):** much the same (Melody, Rhythm, Echo, Tune).
- **OpenAI Playground, GPT-4, temperature 1.2:** much more fun, with lots of alliteration (e.g. RhythmSphere, SoundVortex, AuditoryOasis).

> **Tip:** For idea generation, the **OpenAI Playground** lets you control creativity directly with **temperature**.

**Jokes.** "*We are planning on decorating the engineers' floor in our office. Could you come up with some short, pithy jokes involving programming and other technologies?*" (GPT-4) → the instructor laughed out loud at some of them.

### Roleplay

**Roleplay prompting** sets up a scenario where participants take on **roles** and interact based on instructions. You provide **context, objectives, and a few opening lines**, then end with the model's role label (e.g. `Agent:`) so it knows it's its turn.

**1. Customer service (Bing, Creative mode).**
- *Setup:* "*Play the role of a customer service agent at a food delivery company and I will play the role of an irate customer. Please be unfailingly polite and helpful…*"
- It asked for the order number and restaurant. After complaints, it said the driver would arrive **within 15 minutes** and offered a coupon, **SORRY10**. It gave a reasonable answer when pressed for an explanation.

**2. Oversmart teenager (ChatGPT).**
- *Opening:* Adult: "*How was school today?*" → `Teenager:`
- Smart-alecky answers to questions about teachers, favorite subjects, and fun, with **lots of emojis**. The instructor found ChatGPT **very good at roleplay**.

**3. Jargon-loving scientist (ChatGPT).**
- *Opening:* Colleague: "*Did you enjoy your vacation?*" → `Scientist:`
- Jargon-filled answers to simple questions ("*Where did you go?*", "*What are you working on now?*").

---

## 11. Reasoning prompts: mathematical, logical, predictive

**Reasoning prompts** stimulate **critical thinking, problem-solving, and logical analysis**. They're more complex than fact-based prompts: the model must explain its **logic**, weigh evidence, and possibly use examples.
- **Analytical reasoning:** logical analysis, not necessarily math
- **Mathematical reasoning:** math problems with explanations of how they were solved

**Setup:** OpenAI Playground with **GPT-3.5 Turbo** (just a preference; GPT-4 works too). Temperature was **lowered to 1**, because you don't want creativity for reasoning. **Background:** earlier models behind ChatGPT were very bad at math, but newer ones handle middle-school math well.

### Mathematical reasoning

| Problem | GPT-3.5 Turbo (Chat) | text-davinci-002 (legacy) |
|---|---|---|
| 234 + 456 | **690** ✔ | — |
| 1234 − 237 | Correct ✔ | — |
| 1289 × 498 | Correct ✔ | — |
| 4x + 3 = 31 | **x = 7**, with working, without being asked | **x = 7** ✔, but no explanation |
| A pair of simultaneous equations | **a = 3, b = 0** ✔, step by step | **a = 1, b = 2** ✘, no steps |
| 35 shirts bought at Rs. 280, each sold at Rs. 308. Profit %? | Correct, step by step ✔ | **8.28%** ✘ (completely wrong) |
| Sold for Rs. 2,400 at 25% profit. Profit or loss if sold at Rs. 1,800? | **Loss of Rs. 120** ✔, step by step | — |
| Two athletes running the same direction at different speeds. Distance after 10 minutes? | 10 min = 1/6 hour → relative speed → speed-distance formula → **1/3 km** ✔ | — |

- *(The instructor checked the arithmetic with a calculator.)*
- **Old vs. new models:** With older models you had to **ask for intermediate steps**. Newer models **automatically** solve math **step by step**.
- **text-davinci-002** is part of the GPT-3 series, less powerful than GPT-3.5. The text-davinci models are legacy models, tuned more for **natural language** than math. Unless you have a specific use case, you're unlikely to use them.

### Logical reasoning

| Prompt | Result |
|---|---|
| "*Aubrey is my friend and Brett is my friend. Are Brett and Aubrey friends?*" | GPT-3.5: **can't tell** from the information given ✔ |
| "*There are two ducks in front of a duck and two ducks behind the duck. How many ducks are there?*" | GPT-3.5: **three** ✔. **GPT-4: five** ✘, with no explanation. |
| "*A man has 53 socks in a drawer: 21 identical blue, 15 identical black, and 17 identical red. How many must he pull out to be 100% certain of a pair of black socks?*" | GPT-4: **39**, with a very good explanation ✔ |

> One wrong answer doesn't mean GPT-4 is worse at logic than GPT-3.5. It gets complex problems right. But **models won't always get reasoning right**.

### Predictive reasoning

| Prompt | Result |
|---|---|
| "*Mary gets a haircut whenever she goes out shopping during the day. Mary went shopping during the day yesterday. What can you deduce about Mary today?*" | Guarded: Mary **likely got a haircut yesterday**, but nothing can be said about today |
| "*When it gets really hot in Bangalore, it rains. It's really hot in Bangalore today so today evening it's likely to…?*" | **Rain** |

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **Instruction / context / input data / output format** | The four elements of a prompt; only the instruction is required |
| **Persona / role playing** | Asking the model to act as a specific person or role |
| **Positive constraint** | A limit phrased as what *to* do ("use three bullets or fewer") |
| **Delimiter (`###`, `"""`)** | A marker separating your instruction from the input text |
| **Leading words** | Words like `import` or `SELECT` that nudge code generation toward Python or SQL |
| **Open-ended / close-ended prompt** | Subjective and exploratory / directed with an objective answer |
| **Multi-part prompt** | Several connected questions in one prompt |
| **Scenario-based prompt** | Sets a situation first, then asks for a response |
| **Opinion-based prompt** | Asks the model what it thinks |
| **Fact-based / explanation-based prompt** | Asks for verifiable facts / asks for a deeper explanation |
| **Summarization prompt** | Asks for a condensed version of text |
| **Classification prompt** | Asks the model to label or categorize (including sentiment analysis) |
| **Zero-shot / few-shot** | No examples / a few example "shots" to guide the model |
| **Extraction prompt** | Pulls specific information out of supplied text |
| **Question answering** | Answering questions using only supplied text |
| **Writing prompt** | Guides or kick-starts writing (creative, narrative, expository, persuasive, …) |
| **Ideation prompt** | An open-ended prompt for generating ideas |
| **Roleplay prompt** | Sets up roles and opening dialogue for the model to continue |
| **Reasoning prompt** | Asks for mathematical, logical, or predictive reasoning with the logic explained |
| **Hallucination** | The model making up information (e.g. Bard on "NonameDB") |

---

*Source: course transcript "Exploring Prompt Engineering Techniques" (13 videos). Tool behavior is as shown when the course was recorded.*

[← Previous chapter](05-getting-started-with-prompt-engineering.md) · [Back to contents](../README.md) · [Next chapter →](07-case-studies-in-prompt-engineering.md)
