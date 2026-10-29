# Chapter 7 · Case Studies in Prompt Engineering

**Part 1 — Activate** · Instructor: Janani Ravi · [← Previous chapter](06-exploring-prompt-engineering-techniques.md) · [Back to contents](../README.md)

> **About this chapter:** This course is a set of hands-on case studies in ChatGPT (GPT-3.5), Google Bard, and the OpenAI Playground. This chapter captures the **prompting patterns, examples, and lessons**. Tool behavior is recorded as it was at the time of recording. The instructor's standing caveat: **always double-check generated code and answers.**

---

## At a glance

- **Data generation prompts** create realistic fake (synthetic) data in any format, with the fields, counts, statistics, and constraints you specify.
- **Code generation prompts** can be plain English, **code comments**, or **starter code** (e.g. a function signature) that the model completes.
- Generative AI can also **write SQL**, **convert code** between languages, **explain code**, **debug code**, and **write code from documentation** you supply.
- **Zero-shot** = no examples. **Few-shot** = a few examples ("shots") that teach the task and format.
- **Chain-of-thought** = spell out the steps you want, or simply add "*Let's think step by step*".
- **Augmented (generated) knowledge** = give the model information it didn't have, such as your organization's rules, so it can act on it.
- **Prompt engineering is not an exact science.** Output is probabilistic, so tweak and retry.

---

## 1. Generating data with prompts

Fake data is useful for scenarios, demos, development, and testing. Making it by hand (or with Excel formulas) is tedious, especially when you need many attributes. Here, "data generation" means **data in the form of records**, in any format.

**Setup:** the OpenAI Playground with GPT-3.5. The **maximum length** was raised to **533 tokens** to allow longer outputs. The instructor switches between tools to show the techniques **work the same across platforms**.

### Examples

**1. Names for a fictitious scenario.**
- *Prompt:* "*I need some names for men, women, companies, and designations for my fictitious scenario. Please can you come up with five examples of each kind of name?*" (no format given)
- *Result:* five of each (e.g. the company "Quantum Solutions").
- *Refinement for an international audience:* "*Can you make these names more diverse? The individuals are from different countries of origin.*" → names from Pakistan, Mexico, India, Saudi Arabia, China, Colombia, and more.

**2. Bank loan customers (JSON).**
- *Prompt:* 20 records of bank customers who applied for a loan, each with name, age, gender (male, female, or other), income, designation, years with the bank, and loan amount, in **JSON**.
- *Result:* the records matched, but the output **stopped partway** because the maximum token length was too small.

**3. Restaurant reviews with a set mix.**
- *Prompt:* 10 sentences reviewing a **fine-dining** restaurant: **6 positive, 2 negative, 2 neutral**.
- *Result:* exactly that order: reviews 1–6 positive, 7–8 negative, 9–10 neutral ("meh").

**4. Data with statistical characteristics.**
- *Prompt:* height and weight data for a **linear regression** problem. Students aged 10–12, **average height 140 cm**, **average weight 38 kg**. Name, height, and weight for 20 students, in **CSV**.
- *Result:* values distributed around 140 cm and 38 kg, true to the spec.
- *Refinement:* first *and* last names for each student.

**5. Data for a relational database.**
- *Prompt:* two tables, **employees** and **departments**, with fields listed. *Constraint:* every employee must belong to a department, but a department need not have employees.
- *Result:* exactly as specified. (In this run every department happened to have employees, which was allowed but not required.)

The course summary adds that you can request data **in any format, even embedded within SQL queries**, for easy insertion into SQL tables.

---

## 2. Generating code: descriptive and comment prompts

Generative AI tools are very good at **straightforward code**. For **advanced use cases or obscure technologies** with few examples on the web, they may not do as well. As code gets more complex, be **more cautious** about using it.

### Plain-English prompts

| Prompt | What ChatGPT gave |
|---|---|
| "*What's the code that I can use in Python to open and read a file line by line?*" | Correct code (`open` in read mode, iterate line by line, print each line) **plus an explanation** |
| "*How do I read a CSV file using the Pandas library?*" | Step-by-step: the import, reading the data, printing the first records, then a complete example |
| "*How do I check for duplicates in a list in Java?*" | Correct Java in Java style (camelCase variable names). Another run gave **three methods**: sets, nested loops, and Java 8 Streams. |
| "*How do I make a GET request to [URL] … using the Python requests library?*" | Installation step, then code **using your exact URL**, so little editing is needed, plus an explanation |

> **Lesson:** **Specific prompts always produce more useful responses**, unless you're ideating.

### Comment prompts

You can write the request **as a code comment**, and the model infers the language from the comment style.

**Python-style comment** (`#`): "*# Request the user to provide their name and city and greet them*" → Python code. This **usually** works. In one of the instructor's few tries, the result wasn't Python.

**`//` comments are ambiguous:**
- One run gave **Java**.
- Another run of the same prompt gave **JavaScript**, which also uses `//`.

**The most reliable technique** (the instructor's preferred one) is to **name the language inside the comment**:
- `// Java` then `// Request the user …` → Java
- The same pattern for **C#** and **C++** → correct code with proper syntax
- `// JavaScript` → JavaScript
- `# Python 3` works too. Python 3 is the default today, so you'd only need to specify **Python 2** explicitly.

### Refining with follow-ups

**Wrapping code in a function.**
- *Prompt:* "*# Given a list of elements can you check to see if a particular item exists in that list?*" → correct but **standalone** code.
- *Follow-up:* "*Can you create a function that performs this check and returns true or false?*" → a function with a meaningful name (`item_exists_in_lists`) and an example call.

**Changing the library.**
- *Prompt:* "*# Read data from a CSV file and filter out all records where Age is < 20*" → ChatGPT chose **Pandas** (installed it, made a sample CSV, filtered).
- *Follow-up:* "*Can you please use the CSV reader for this?*" → redone with Python's CSV reader.

**Numbered steps inside `"""`.**
- *Prompt:*
  1. Create a list of employees who belong to departments.
  2. Create a list of department names and IDs.
  3. Combine them to get a result of 5 employees with departments.
- *Result:* granular, step-by-step code.
- No language was given, so ChatGPT picked **Python**, because the conversation had mostly been about Python. It could just as well have chosen SQL.

---

## 3. Starter code prompts and generating SQL

### Starter code prompts

Give the model **the beginning of the code**, such as a function signature, and it completes it. The starter code must be **unambiguous** and make your intent clear. A meaningful function name helps a lot.

| Starter code | Language inferred from | What the model did |
|---|---|---|
| `def is_prime_number():` | `def` and the trailing `:` → **Python** | ChatGPT stated the goal, **added the missing input argument**, wrote correct prime-checking code, and showed how to call it. **Bard** produced almost the same code with an explanation. |
| `void validateEmailAddress(String email) {` | Signature style → **Java** | Placed it in a class with a `main` and test calls. It **respected the `void` return type**: it printed whether the email was valid instead of returning true or false. Used **regular expressions**, which it explained. |
| `double calculateDistance(p1, p2` *(as described)* | Syntax → **C++** | Said "*It seems like you want a function in C++*", included the math library, defined a `Point` class, then the function |
| `function factorialRecursive(` | The `function` keyword → **JavaScript** | Followed JS best practice (`===`), and **understood "Recursive" from the name**, so it wrote a recursive solution with a `console.log` of the result |

### Generating SQL from comment-style prompts

Describe the table(s) and the task inside `"""`, **without saying "SQL"**. The word **"Table"** cues the model that the data lives in a relational database.

| Prompt (tables + instruction) | SQL the model produced |
|---|---|
| Table **Employees** (with a Department column). "*Find all employees who belong to the Operations department.*" | A simple `SELECT … FROM … WHERE`, with each clause explained |
| Tables **Employees** (with `DepartmentID`) and **Departments** (`ID`, `DepartmentName`). Same instruction, **without mentioning joins** | An **`INNER JOIN`** on the department ID, with aliases (`D`, `E`) and a filter on `DepartmentName` |
| Table **Employees**. "*Find all employees who have salaries greater than the average employee salary.*" | A **nested subquery**: `WHERE Salary > (SELECT AVG(Salary) FROM Employees)` |
| "*Count the number of employees in each department*", ending with the leading word **`SELECT`** | A **`LEFT JOIN`**, which is correct because a department could have zero employees |

**Steering the language:**
- The model may guess the wrong language, leading to "annoying back and forth".
- Either **name the language in the comment** (SQL, Java, Python), or use a **leading word**:
  - `SELECT` nudges toward SQL.
  - `import` nudges toward Python.
- In one run, ending with `import` still **didn't** give Python, though it had worked in earlier runs.

> **Lesson:** **Prompt engineering is not an exact science.** Tweak your prompts until you get what you need.

---

## 4. Code conversion and code explanation

### Converting code between languages

This is useful in **migration projects** (e.g. Python → Java). Migrations are rarely straightforward, but individual functions can be converted with generative AI. It works for simple and fairly complex functions, so test it on your own code.

**Example: a Python function that builds a dictionary** (student name → age, with error checking).

| Target | What the model did |
|---|---|
| **Java** | Mapped the dictionary to a **`HashMap`**, wrapped it in a class (`StudentDictionaryCreator`) with a `main`, and kept the error check (`if (names.length != ages.length)`) |
| **JavaScript** | Accurate conversion |
| **C++** | Used a **`vector`** for the inputs and an **`unordered_map`** in place of the dictionary |

**Python-only constructs** convert too: a **list comprehension** (keep numbers > 100) became longer, explicit Java code producing `filteredNumbers`.

> **Always double-check and test** converted or generated code, just as you would code copied from Stack Overflow.

### Explaining code

**The problem:** You copy code from Stack Overflow, it works, but you don't understand it, so you can't adapt it.

**Example 1: `process_random_number` (Python).**
- The code picks a random number from a list and returns zero, its square, or its cube.
- *Prompt:* "*Please explain what process_random_number does.*"
- *Result:* a credible, correct explanation.

**Example 2: `randomFunction` (Java).**
- The name was **deliberately meaningless**, and the word "reverse" was **nowhere** in the code. The code uses a `StringBuilder` to reverse the words in a sentence.
- *Result:* ChatGPT gave a **line-by-line explanation** and correctly worked out that the code **reverses the words**.

> Explanations "may not be perfect, but [are] enough for you to get started."

---

## 5. Debugging code and coding from documentation

### Debugging

When you're stuck on one small bug, generative AI can spot errors that would take you hours. **Always double-check** what it tells you.

**1. An infinite loop (Python, no language stated).** *Prompt:* "*Why does this code not complete?*"

| Model | Response |
|---|---|
| **GPT-3.5 (Playground)** | First claimed a missing parenthesis and colon on the `while` loop (wrong). After "*This code is in Python*", it apologized and blamed a missing indentation (also wrong, since the indentation was there), **but its fixed code was correct**: it added `count += 1`. *Right code, wrong explanation.* An apology doesn't mean the answer is right. |
| **Bard** | Opened with "the while loop is infinite", explained the fix, and gave corrected Python. **Much more useful.** |

**2. Real Stack Overflow questions pasted into Bard.**
- **`UnsupportedOperationException` (Java).** The instructor removed the stack trace and line numbers, leaving clean code and a simple question. Bard found that an **"arrays as list" call creates an unmodifiable array** that the code then tried to modify. It explained this clearly and gave complete fixed code, **matching** the accepted Stack Overflow answer.
- **A bank account bug (Python).** A beginner's `withdraw` method *added* money. The cause: `balance -- int(withdraw_amt)`, where a double negative becomes a plus. Bard pinpointed it and gave the corrected code, matching Stack Overflow's answer. *(The instructor removed an unrelated paragraph asking for practice suggestions so Bard would focus on debugging.)*
- **`TypeError` on `sum(w) != n` (Python).** `w` came from iterating a loop, so it's an **integer**, and **integers aren't iterable**. Bard gave the same fix as Stack Overflow.

> What used to take a Stack Overflow question can often be answered by generative AI today, but they **won't always get things right**, so don't rely on them blindly.

### Generating code from documentation

**The problem:** ChatGPT didn't know the **Zerodha** API (a popular Indian trading platform). It replied "*I'm sorry, but I can't assist with that request.*"

**The fix (ChatGPT):**
1. Copy the Zerodha **orders documentation** (`kite.trade/docs/connect/v3/orders/`) up to, but not including, the "retrieving orders" section. This keeps it within ChatGPT's length limit.
2. Ask: "*Using the documentation on this page, can you write a request in Python to place an order on Zerodha?*"
3. *Result:* After one "servers overloaded" error and a regenerate, it gave code using the `requests` library that was **close to correct**. You'd need to test it to be sure.

**Bard** can read web pages directly. Asked to write Python to **modify an existing order** on Zerodha, it produced code that **matched the documentation**.

> ChatGPT, Bard, and Bing Chat can all **parse documentation** and write code based on it.

---

## 6. Zero-shot and few-shot prompting

### Zero-shot prompting (zero-shot learning)

The model performs a task it **wasn't explicitly trained for**, using its general understanding, with **no examples**. You just make the task clear.

**Sentiment of Amazon reviews:**
- "*What's the sentiment of the review below?*" + a negative review → **negative**
- The same with a positive review → **positive**
- A review the instructor considered neutral but slightly negative in tone → ChatGPT firmly said **negative**

### Few-shot prompting (few-shot learning)

Give a **small number of example inputs and outputs** ("**shots**"). The model learns the task and **mimics** the examples. Unlike zero-shot (generalizing from pre-training alone), the shots **guide** it.

**1. Sentiment without saying "sentiment analysis".** Only shots were given:
- "*Truly game changing product*" → highly positive
- … → positive
- "*I'm happy I went once, but I would not go again*" → meh
- "*Well worth the two hours I spent*" → `Sentiment:` → model: **positive**

**2. Book recommendations.**
- **Zero-shot:** "*Recommend some classics that I could read*" → classics across genres and eras, but none appealed to her.
- **Few-shot:** first list books she liked (*The Count of Monte Cristo*, *Journey to the Center of the Earth*, *The Moonstone*), then ask the same question → **much better** picks: *Treasure Island*, *The Hound of the Baskervilles*, *Around the World in Eighty Days*, *The Prisoner of Zenda*.

**3. Keyword extraction.**
- **Zero-shot:** "*Extract 5 keywords*" from pasted text → five relevant keywords (a pretty decent job).
- **Few-shot:** *Text 1 / Keywords 1*, *Text 2 / Keywords 2*, then *Text 3 / Keywords 3:* → the shots also fixed the **output format**.

**4. Conversation roleplay (Parent and Teenager).**
- *Prompt:* a sample conversation ending in `Teenager:`, with **no instructions**.
- **Same session:** ChatGPT produced **keywords** instead. **Leftover context** from the keyword task confused it.
- **New chat:** it replied correctly as the Teenager.
- Later, it got **over-enthusiastic** and wrote the Teenager's line, then the Parent's, then the Teenager's again, and repeated this. Even with shots, **roleplay won't always behave perfectly**.

**5. Teaching a made-up math concept: "grrfss".**
- *Shots:* grrfss of list 1 = 5.5, list 2 = 7, list 3 = 301. (Secretly, grrfss is the **median**; the word "median" was never used.)
- **ChatGPT** this time wrongly assumed it was the **average**. (The instructor notes it got it right the first time she tried.)
- **Bard** worked out it was the **median**, explained how to compute it, checked the three examples, then answered new questions correctly: one list → **500**, and an even-length list was also correct.

**6. Teaching a made-up word (an example from a research paper on arXiv).**
- *Shot:* "*A 'whatpu' is a small furry animal native to Tanzania. An example sentence: 'We were traveling in Africa and we saw these very cute whatpus.'*"
- *Then:* "*To do a 'farduddle' means to jump up and down really fast. An example of a sentence that uses the word farduddle is:*"
- *Bard:* "*The children farduddle with excitement. The dog farduddle around the yard, chasing its tail.*"

---

## 7. Chain-of-thought prompting

**Chain-of-thought (CoT) prompting** guides an LLM to think **step by step**, by giving it examples or steps that outline the reasoning process. The model then follows a similar chain of thought.
- Earlier LLMs were weak at math, and CoT helped them.
- **Today's models often use step-by-step reasoning automatically.**
- CoT is especially useful when you want **each step of the response done your way**.

### Example 1: Data analysis

**Without CoT:** "*With customers and orders data can you give me the average order price for each customer who has more than 3 orders?*" → a **SQL query** she didn't want, with no intermediate steps. The prompt was vague.

**With CoT:** "*Using Python and Pandas can you do the following with step by step instructions and code?*"
1. Install the Pandas library.
2. Read two CSV files called customers and orders.
3. Combine the files to form a resulting dataframe.
4. Find the customers who have more than 3 orders.
5. Compute the average order price for these customers.

→ **One response step per prompt step**, each with code and explanation. Directly usable.

### Example 2: A technology decision

**Without CoT:** "*Which is better, Java or Python?*" → a good, detailed, general comparison.

**With CoT:** "*Compare Java and Python keeping the following points in mind, and tell me which one would be better for my team to use:*"
1. Consider the learning curve, as my team is mainly junior programmers.
2. Account for the fact that we use SQL.
3. We need high performance and ease of maintenance.
4. Generate strengths and weaknesses of each language.
5. Make the final decision based on these criteria.

→ Each point is addressed separately, ending with a decision: a **hybrid approach**. The instructor calls this "a bit of a cop out", noting the final decision should be yours anyway.

### Example 3: Helping a weaker model with math

**Setup:** OpenAI Playground, **legacy Completions** mode, **text-davinci-003**.
- **Without CoT:** "*The cafeteria had 23 apples. If they used 20 to make lunch and bought 6 more, how many apples do they have?*" → **9** (correct this time), but **no working**, and it won't always be right.
- **With CoT steps:**
  1. Start with the original number of apples.
  2. Consider only the apples used to make lunch and compute how many are left.
  3. Consider the newly bought apples and compute how many are left.
  - → The working is shown, so you can **verify** the answer of 9.
- **The simplest CoT:** just add "**Let's think step by step**". That alone makes the model show its reasoning and makes a correct answer more likely.
- **Newer models (GPT-3.5):** for simple math, you don't need CoT. The response is **automatically** step by step.

---

## 8. Augmented knowledge (generated knowledge) prompting

You **augment the model's knowledge** with information relevant to your business or use case, which it **didn't have before** (e.g. organization-specific rules). The model then uses it to respond. **Example use:** building an organization's chatbot.

### Case study: a computer science tutoring center chatbot

**The prompt (pasted into ChatGPT)** sets up the role and rules:
- **Role:** "*Consider that you are an assistant at a Computer Science tutoring center. You help students find the right teacher…*"
- **Step 1:** Ask the student what the problem is.
- **Step 2:** Identify which subject it belongs to: **Java, Python, C++, SQL, ML, GCP, AWS, Azure, Data Science and Analytics**.
- **Step 3:** Identify the topic area and assign a teacher who covers it. *Teachers can only help in their own areas.*
- **Step 4:** If the student asks for a specific teacher, **check** that the teacher covers that area. If not, tell the student.
- **Step 5:** Wish the student luck on their learning journey.

**Teachers mentioned in the course:**

| Subject | Teachers |
|---|---|
| Java programming | Alice, Mary, Bob |
| Python programming | Christine, Richard |
| SQL | John, Jane |
| Machine learning | Ramesh, Sudha, Ji Yiang |
| AWS | Jasmine, Raj |
| GCP | Kasia |

### How the conversations went

**Conversation 1: Python.**
1. "*I have a problem with my code*" → the bot asks which language or topic.
2. "*Python*" → suggests **Christine or Richard** (correct).
3. "*I would like to talk to Kasia*" → the bot explains **Kasia specializes in GCP, not Python**, and asks the student to pick a Python teacher.
4. "*Please assign me to Christine*" → assigned, with good wishes.

**Conversation 2: cloud upload.**
1. "*I'm trying to upload a file to the cloud…*" → narrows it to **GCP, AWS, or Azure** and asks which one.
2. "*I'm not sure*" → the bot patiently asks what service, URL, or website is being used.
3. "*The service says S3*" → identifies **S3 (Simple Storage Service) as AWS**, and suggests **Jasmine or Raj**.
4. "*Can't Ramesh help me?*" → **No, Ramesh specializes in machine learning**. It recommends Jasmine or Raj.
5. "*Any of them*" → assigned to **Jasmine**, with good wishes.

**Conversation 3: random forest.**
- "*I'm having some trouble with my random forest algorithm*" → recognizes it as **machine learning** without being told, offers Ramesh, Sudha, or Ji Yiang, and assigns **Ramesh**.

> **Lesson:** The model knew nothing about this tutoring center, but **augmenting its knowledge** in the prompt produced a working chatbot you could integrate into an app.

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **Data generation prompt** | Asks the model to create synthetic records in a chosen format, with set fields and constraints |
| **Maximum length (tokens)** | A Playground setting that caps response length; too low and output gets cut off |
| **Code generation prompt** | Asks the model to write code from a description |
| **Comment prompt** | A request written as a code comment (`#`, `//`); naming the language in it is the most reliable approach |
| **Starter code prompt** | A partial piece of code (e.g. a function signature) for the model to complete |
| **Leading word** | A word like `SELECT` or `import` that nudges the output toward SQL or Python |
| **Code conversion** | Translating code from one language to another (e.g. Python dictionary → Java `HashMap`) |
| **Code explanation** | Asking the model what a piece of code does |
| **Zero-shot prompting / learning** | Performing a task with no examples, relying on general knowledge |
| **Few-shot prompting / learning** | Giving a few example input/output "shots" to guide the task and format |
| **Chain-of-thought prompting** | Guiding the model through explicit reasoning steps, or adding "Let's think step by step" |
| **Augmented / generated knowledge prompting** | Supplying new, use-case-specific information for the model to use in its responses |

---

*Source: course transcript "Case Studies in Prompt Engineering" (10 videos). Tool behavior is as shown when the course was recorded.*

[← Previous chapter](06-exploring-prompt-engineering-techniques.md) · [Back to contents](../README.md)
