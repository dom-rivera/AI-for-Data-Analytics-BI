# Chapter 3 · Artificial Intelligence and Machine Learning

**Part 1 — Activate** · Instructor: Janani Ravi · [← Previous chapter](02-introduction-to-gpt-models.md) · [Back to contents](../README.md) · [Next chapter →](04-deep-learning-and-neural-networks.md)

---

## At a glance

- **AI** is the broad umbrella. **Machine learning (ML)** is a subset of AI: algorithms that **learn from data**. **Deep learning** is a subset of ML that uses **neural networks**.
- An ML model learns **patterns** from training data, then makes **predictions on unseen data**. It's "garbage in, garbage out".
- **Supervised learning** needs **labeled data** (regression, classification). **Unsupervised learning** works with **unlabeled data** (clustering).
- **Regression** predicts continuous values (evaluated with **R²**). **Classification** predicts categories (**accuracy, precision, recall**). **Clustering** finds groups (**elbow method, silhouette score**).
- **Traditional models** covered: linear regression, logistic regression, decision trees.
- **Ensemble learning** ("wisdom of the crowds") combines many models: **bagging, boosting, stacking**.

---

## 1. What are AI and ML?

AI is now part of almost every part of professional and personal life. Even if you don't build models, it helps to understand these terms so you can talk with the data scientists and technologists you work with.

### Defining AI

The term has been around since at least the **1950s** and covers so many techniques that it's hard to pin down.

- **A layman's definition:** AI is an activity devoted to making machines intelligent. **Intelligence** is the quality that lets an entity function appropriately and with foresight in its environment.
- **AI is its own kind of intelligence.** It is not the same as human intelligence. AI can perceive objects, but maybe not the way we do.
- AI is broader than ML. Traditionally it also covered non-ML fields such as **game theory**.
- **AI refers to the whole system.** *Example:* With ChatGPT, Google Bard, or Bing Chat, the whole chatbot system is "AI". The large language model behind it is the model powering it.

**What "AI" means depends on who's talking:**
- **Everyday use:** a catch-all for applications that perform human-like tasks without human help
- **People in big tech:** often something specific, such as deep learning models that extract meaningful representations from data for prediction. Engineers and data scientists may mean only the **model**, not the whole system.

### AI vs. ML vs. deep learning

| Term | What it is |
|---|---|
| **Artificial intelligence** | An umbrella term for software that mimics human cognition to perform complex, human-like tasks (walking, detecting obstacles, conversing) |
| **Machine learning** | A **subfield of AI**: algorithms trained on data to produce **models** that can make predictions. Once trained on data, the algorithm is called a model. |
| **Deep learning** | A **subset of ML** that uses **neural networks** for the most complex tasks |

- There's **no standard way** to separate AI and ML, which is why the terms are often used interchangeably.
- A **neural network** is a model architecture made of learning units called **neurons**, arranged in **layers**.

### Real-world AI systems (with ML at their heart)

| AI system | ML inside it |
|---|---|
| **Self-driving car** | Computer vision to recognize stop signs, signals, and obstacles, then act on them |
| **Conversational chatbot** | Understanding natural language and recognizing patterns in your prompts to respond |
| **Voice assistants (Alexa, Siri)** | Speech-to-text and text-to-speech models, plus natural language processing |

---

## 2. Understanding machine learning

**ML algorithms learn from data.** A normal program applies rules someone wrote. An ML algorithm has **no predefined rules**. It **learns the rules from data** during training.

- An algorithm on its own (linear regression, logistic regression, support vectors, decision trees) **knows nothing**.
- Only after training on lots of data can it understand and reproduce the **statistical patterns** in it, and predict outcomes on **unseen data**.
- Put simply: **ML is a massive pattern recognition exercise.**

> **Example: predicting home prices.** The model might learn that larger homes and homes by the seaside tend to cost more, and that older homes cost less because they need maintenance. This works only if the data has enough samples of each attribute.

### Steps to build an ML model

1. **Choose an algorithm.** "Algorithm" usually means the model before it's trained, e.g. Naïve Bayes, decision tree, support vector machine, linear or logistic regression. Neural networks are usually called **architectures** instead, because they don't use one specific learning algorithm.
2. **Feed in training data.** The algorithm finds statistical patterns, and this learning **trains the model's parameters**. This is **iterative**: early predictions are poor and improve as the model sees more data.
3. **Get a trained model.** You start with an algorithm and end up with a model.
4. **Validate on test data** the model hasn't seen. This is essential, because it shows how the model will really perform.

### Two phases

| Phase | What happens |
|---|---|
| **Training** | Feed a large corpus of data to the algorithm so its parameters learn the patterns. Then validate and test. |
| **Prediction** | Deploy the model to production and use it on **new, unseen** instances (e.g. homes not in the training data) |

**Models get outdated quickly.** Real-world data changes, so models must be **retrained and redeployed** regularly. A home-price model trained on 1990s–2000s prices won't help today, and even year-old data may be too stale.

### How a model learns: the spam vs. ham example

A **classification** model sorts emails into **spam** or **ham** (ham = genuine, useful email).

- **What the model might learn:**
  - **Spam** tends to come from addresses not in your contacts, uses many exclamations and superlatives, and tries to sell you something or says you've won something.
  - **Ham** tends to come from known addresses, uses simple and clear language, is professional, and doesn't try to sell anything.
- **Training data:** hundreds of thousands (even millions) of emails, each **correctly labeled** as spam or ham.
- **Using the model:** send spam to the spam folder or trash, and ham to the inbox.

**Key vocabulary:**

| Term | Meaning | In the spam example | In the home-price example |
|---|---|---|---|
| **Features / x variables** | The input attributes | The email text (without its label) | The home's attributes |
| **Label / target / y variable** | What the model predicts | Spam or ham | The price |

**Loss:** During training the model keeps making predictions, poor ones at first. The difference between its prediction and the actual label is the **loss**, which is fed back to **adjust the model's parameters**. This repeats over and over. It's like how people improve when they get feedback.

**Garbage in, garbage out.** A model is only as good as its training data. Even the best algorithm performs poorly on bad data, so **data quality is as important as the algorithm, or more**.

### Three common types of ML problems

| Type | Predicts | Examples |
|---|---|---|
| **Classification** | **Discrete categories** | Spam/ham; dog, cat, or bird; yes/no |
| **Regression** | **Continuous values** (any number in a range) | Home price, stock price, rainfall, crop yield |
| **Clustering** | **Logical groups** in the data | Which social media users like sports, music, or movies |

---

## 3. A brief history of machine learning

ML has gained attention in the last ten years, but it dates back to the **1940s**. The instructor notes this is a selection, not a complete list.

### 1940s–1950s: the seeds

| Year | Milestone |
|---|---|
| **1943** | **Warren McCulloch and Walter Pitts** built the first neural network using an electric circuit, aimed at communication between computers |
| **1950** | **Alan Turing** proposed the **Turing Test**: can humans tell whether answers come from a machine or a human? (Whether the answers are true doesn't matter.) |
| **1952** | **Arthur Samuel**, a machine learning pioneer, created the first program to play **championship-level checkers** |
| **1957** | Psychologist **Frank Rosenblatt** developed the **Perceptron**, considered the first neural network unit and algorithm. It learned by adjusting its parameters until it reached an optimal solution, which is still how ML is trained today. |

### Symbolic vs. subsymbolic AI (the 1950s debate)

| | Symbolic AI | Subsymbolic AI |
|---|---|---|
| **Also called** | Classical AI, "good old-fashioned AI" | — |
| **Works with** | Symbols and concepts, explicit rules | **Numeric data**: calculations, parallel and connectionist processing |
| **Mimics** | **Conscious** thought | **Unconscious** thought |
| **Intelligence comes from** | Reasoning, rationality, formal logic | An **emergent** phenomenon: patterns of activation across interconnected units (neurons) |
| **How it works** | Rule-based, deterministic, deduction; doesn't typically learn from data | Learns from data or the environment, by induction |
| **Good for** | Knowledge-based reasoning, constraint-based reasoning, combinatorial search | Pattern recognition and messy, sensory-rich inputs |
| **Inspired by** | Mathematical logic | Neuroscience and systems theory |
| **Today** | More like traditional computer science; still has its place | The **neural networks** used for today's most complex tasks; it has overtaken symbolic AI in importance |

### 1960s–1970s

| Year | Milestone |
|---|---|
| **1967** | **Nearest neighbor** algorithm, to find patterns in large datasets (still used today, improved) |
| **1974** | **Backpropagation**, initially designed to help neural networks recognize patterns. It's still how neural networks are trained. |
| **1979** | The **Stanford Cart** crossed a room with obstacles on its own, an "autonomous vehicle from the 70s" |

### The AI Winter (late 1970s to early 1990s)

AI has had highs and lows. In the **AI Winter**, funding dried up and many projects shut down for lack of success. Earlier **hype cycles** had led to disappointment among developers, researchers, users, and the media. Excitement returned in the late 1980s, and milestones continued:

| Year | Milestone |
|---|---|
| **1981** | **Gerald Dejong**: **Explanation-Based Learning (EBL)**. The computer creates a general rule by discarding unimportant data and focusing on what's relevant. |
| **1985** | **Terry Sejnowski**: **NETtalk**, a program that learned to pronounce words |
| **1989** | **Yann LeCun** and others showed a **convolutional neural network** recognizing handwritten digits (still a classic first image task) |

### 1990s

| Year | Milestone |
|---|---|
| **1992** | **Gerald Tesauro**: a neural-network **backgammon** program that rivaled top players |
| **1997** | **Sepp Hochreiter** and others: the **LSTM** (long short-term memory) recurrent network for sequences such as speech and video (still used today) |
| **1997** | IBM's **Deep Blue** beat **Garry Kasparov**, the first defeat of a reigning world chess champion by a computer under tournament conditions |
| **1998** | Team led by **Yann LeCun**: the **MNIST** dataset (Modified National Institute of Standards and Technology), still a handwriting-recognition benchmark |

### 2000s

| Year | Milestone |
|---|---|
| **2000** | University of Montreal researchers: ***A Neural Probabilistic Language Model***, modeling language with feedforward neural networks |
| **2002** | **Torch**, the first open-source ML library (deep learning algorithms in C). It's the basis of today's **PyTorch**. |
| **2006** | **Geoffrey Hinton** coined the term **"deep learning"** |
| **2006 / 2009** | **Fei-Fei Li** began work on **ImageNet** (introduced 2009), a catalyst for the AI boom and the basis of an annual image-recognition competition |
| — | **Netflix Prize**: a competition to beat Netflix's own recommendation algorithm |

### 2010s

| Year | Milestone |
|---|---|
| **2010** | Microsoft **Kinect** motion sensor; **Kaggle** launched for ML competitions |
| **2012** | A deep **CNN** won the **ImageNet** challenge, triggering a wave of deep learning research |
| **2013** | **DeepMind** introduced reinforcement learning |
| **2014** | **Ian Goodfellow** and others: **generative adversarial networks (GANs)**. **Variational autoencoders** also introduced. |
| **2017** | Google researchers developed the **transformer** (using **attention**), with a direct line to OpenAI's GPT |
| **2018** | OpenAI released **GPT**, paving the way for other LLMs |

---

## 4. Supervised vs. unsupervised learning

| | Supervised learning | Unsupervised learning |
|---|---|---|
| **Data** | **Labeled**: features (x) **and** targets (y) | **Unlabeled**: only features (x) |
| **Goal** | Learn the relationship **y = f(x)** to predict y on unseen data, by "reverse engineering" how x maps to y | Find **intrinsic patterns** in the data itself |
| **Training** | Compares predictions against the true labels to improve | No labels to compare against, so learns from the data structure alone |
| **Limitation / strength** | Labeling is **manual and time-consuming**, and labeled data is a **small fraction** of all data | **Very powerful**, because most of the world's data is unlabeled |
| **Examples** | **Regression** (stock price, car mileage, tomorrow's temperature); **classification** (dog, cat, or plane; positive or negative review) | **Clustering** (grouping similar data points) |

---

## 5. Regression

**Regression** is a **supervised** technique that predicts **continuous values**. The output can be any number. *Example:* the same stock-price model works for penny stocks and stocks worth thousands of dollars.

- **Algorithms that can do regression:** linear regression (the simplest), decision trees, support vector machines, random forests, neural networks
- Often used in **cause-and-effect analysis:** the features are the causes, and the model figures out how much each contributes to the effect.

**The intuition:** Plot your data points in *n*-dimensional space (*n* = number of features). The line or curve that **best fits** those points is your regression model.

**Example problems from the course:**
- Home features (rooms, oceanfront view, zip code, lot size, renovations) → **price**
- Car features (make, model, age, horsepower, miles driven) → **mileage**
- Hours of study → **GPA** (just one feature)
- Concrete ingredient mix (water and other chemicals) → **strength**

### Worked example: exercise vs. weight

- **Exercise** (minutes per day) is the cause, the **x variable**. **Weight** (lbs or kg) is the effect, the **y variable**.
- Survey data is plotted in 2D. Many lines or curves could pass through the points. A straight line means a **linear** relationship.
- **What is a "best fit"?** The line or curve that **minimizes the distances** from all the data points.
- **Don't overfit.** A curve through *every* point is useless for prediction. You want a model that captures the **general** pattern.
- In **linear regression**, training finds the **best-fit line**.

### Evaluating regression: R²

- **R²** (the **coefficient of determination**) measures **quality of fit**: how much of the **variance** in the data the model captures.
- With multiple features (**multiple regression**), it's called the **coefficient of multiple determination**.
- It ranges from **0 to 1** (or 0–100%). The maximum is 1, and **higher is better**.
- Points close to the line give a **high R²**. Scattered points far from the line give a **low R²**.
- **A good model** minimizes the distance between the fitted line and the training points, and its prediction errors are **small and unbiased**.

---

## 6. Classification

**Classification** is a **supervised** technique that sorts inputs into **discrete classes**.

| Type | Number of categories |
|---|---|
| **Binary classification** | Two (e.g. spam or ham) |
| **Multi-class classification** | More than two |

**What the model outputs:** a **probability score for each class**. The scores add up to **1**, and the highest one is the prediction. *Example:* spam 80%, ham 20% → predicted **spam**.

### Evaluation metrics

| Metric | Question it answers |
|---|---|
| **Accuracy** | What fraction of *all* predictions were right? (e.g. 800 right out of 1,000 = 80%) |
| **Precision** | Of everything the model labeled **positive**, how much was actually positive? |
| **Recall** | Of all the **actual positives**, how many did the model find? |

> **Why accuracy alone can mislead (skewed data):** Imagine tumor scans where 99.99% are benign and 0.01% malignant. A model that *always* says "benign" scores 99.99% accuracy but never catches a malignant tumor. Use **precision and recall** here. A good classifier is judged on **all three** metrics.

### Worked example: confusion matrix (spam = positive class)

A **confusion matrix** shows actual values (rows) against predictions (columns). It's **2×2** for binary classification.

| | Predicted **ham** | Predicted **spam** |
|---|---|---|
| **Actually ham** | 780 | 45 |
| **Actually spam** | 55 | 120 |

- **Accuracy** = (780 + 120) ÷ (780 + 120 + 55 + 45) = 900 ÷ 1,000 = **0.9**
- **Precision** (spam) = 120 ÷ (120 + 45) = 120 ÷ 165 = **0.727**
- **Recall** (spam) = 120 ÷ (120 + 55) = 120 ÷ 175 = **0.685** *(as given in the course)*

**Note:** You must first decide **which class is "positive"**, meaning the one you're trying to identify. Precision and recall change depending on that choice.

---

## 7. Clustering

**Clustering** is an **unsupervised** technique. It needs **no labels**, which makes it powerful, since most data is unlabeled and labeling is slow and manual. It's the most common unsupervised technique. Others include **anomaly detection** and **dimensionality reduction**, which this course didn't cover.

**How it works:**
1. Convert each record's attributes into **numbers**. *Example:* social media users on Facebook or LinkedIn, described by clicks, groups, and personal data.
2. Plot the records in ***n*-dimensional space**.
3. Find **logical groups**. Clustering has two objectives:
   - **Similar** points go in the **same** cluster (close together in space).
   - **Dissimilar** points go in **different** clusters.

**Uses:**
- **Targeted marketing:** show music ads to the music-loving cluster, sports ads to the sports cluster.
- **Grouping documents:** cluster newspaper articles (text converted to numbers via NLP) into topics like business, sports, and politics.

### How many clusters? The elbow method

Some algorithms find the best number of clusters automatically. For those that don't:
1. Run clustering with *k* = 1, 2, 3, 4, … clusters.
2. For each *k*, compute the **sum of squared distances** (within-cluster sum of squares): the squared distance from each point to its cluster's **centroid** (center). **Lower is better**, meaning tighter clusters.
3. Plot it against *k*. The **elbow** is where the decrease **slows down**. This is the trade-off between tight clusters and a reasonable number of clusters, and it's the optimal *k*.

The elbow (or "knee") is a common heuristic for a **point of diminishing returns**. Going beyond it **overfits**: the model becomes too specific to your data and won't generalize well in production.

### How good is the clustering? The silhouette score

The **silhouette coefficient** is calculated for **each data point** and ranges from **−1 to 1**:

| Value | Meaning |
|---|---|
| **1** | The point is far from neighboring clusters (well placed) |
| **0** | The point is very close to, or on, the boundary of a neighboring cluster |
| **−1** | The point is likely in the **wrong** cluster |

- The **silhouette score** is the **average** coefficient across all points. **Higher = better clustering.**
- It can also find the optimal *k*: plot the score for each *k* and pick the highest.

---

## 8. Traditional ML models: linear regression, logistic regression, decision trees

ML models can be split into **traditional models** and **representation-based deep learning models**.

| | Traditional ML models | Deep learning / neural networks |
|---|---|---|
| **Structure** | A **fundamental algorithmic structure**: fit a line or curve, build a tree, compute probabilities | No fundamental algorithm, just different **architectures** |
| **Features** | Need **manual feature extraction**: pick, extract, and preprocess the important features first | — |
| **Raw data** | Don't do well on raw data | — |

### Linear regression (regression)

- **Example:** rainfall (inches) → crop yield (metric tons per hectare). This is a simplified, hypothetical relationship: more rain, higher yield.
- **Training** finds the **best-fit straight line** through the points.
- **Prediction:** For 13 inches of rain, go up from the x-axis to the line, then across to the y-axis to read the yield.
- **Simple regression** uses one x variable. **Multiple regression** uses several (rain, fertilizer, soil quality). The algorithm is the same: fit a line, use it to predict.

### Logistic regression (classification, despite the name)

- It models the **probability** of a class or event: pass/fail, spam/ham, true/false, healthy/sick. The class with the higher probability is the prediction.
- **Example:** hours studied → **pass or fail**. Pass = 1 and fail = 0. Few hours → likely fail; many hours → likely pass.
- The model fits an **S-curve (logistic curve)**: flat near 0 at the bottom, a rising slope, then flat near 1 at the top.
- Points on the slope get probabilities between 0 and 1, so you set a **decision threshold**. *Example:* with a threshold of 0.5, a student who studied 3.5 hours gets a pass probability of 0.75 → **passed**.

### Decision trees (classification *and* regression)

**Example:** "Should I go surfing today?"
- You need **labeled data**: weather conditions (swell, wind, wind direction, …) with the surf / don't-surf outcome.
- Training builds a tree. The **most important variable** goes at the **root**, and every node is a **decision variable with a threshold**.

How the example tree decides:
1. **Is there a swell?** No → **don't surf**. Yes → next question.
2. **Wind?** Low or none → **surf**.
3. High wind **onshore** → **don't surf**. High wind **offshore** → **surf**.

Once the tree is built, you **walk down it** to reach a decision.

---

## 9. Ensemble learning

**The idea, "wisdom of the crowds":** One person's guess at Google's stock price a year from now is a coin toss. The **combined guess of 100,000 or a million people** is more likely to be right.

**Ensemble learning** combines the predictions of multiple **base models** (called **weak learners** or **base classifiers**) to improve overall predictive performance. Ensembles differ in *how the learners learn* and *how their predictions are combined*.

| Technique | How learners are trained | How predictions are combined | Example |
|---|---|---|---|
| **Bagging** | **In parallel**, each on a random sample of the data | **Majority vote** (classification) or **average / weighted average** (regression) | **Random forest** (decision trees as base models) |
| **Boosting** | **In sequence**, each focusing on the previous model's **mistakes** | Similar to bagging | — |
| **Stacking** | A diverse set of base models | A trained **meta model** (blender) learns how best to combine them | Meta model can be simple, like linear or logistic regression |

### Bagging (bootstrap aggregating)

- Each base model is trained on a **random subset** of the data, sampled **with replacement** (**bootstrap sampling**). *Example:* from 1 million records, each model gets 600,000.
- With replacement means each record is put back after it's picked, so some records appear several times and others not at all.
- Each model sees slightly different data, so each has its own strengths and weaknesses. This **diversity reduces overfitting**.

### Boosting

1. Train **Model 1** on the original data (with a set of weights on the data points).
2. **Increase the weight** of the points it got wrong, so **Model 2** pays more attention to the hard examples.
3. Repeat for a set number of iterations, or until a condition is met. Each learner fixes the mistakes of the ones before it.
4. **At prediction time**, the input goes through every learner, and the outputs are combined.

### Stacking

1. Split the data into two parts:
   - Part 1 trains the **base models**.
   - Part 2 (the **holdout set**) trains the **meta model**.
2. The base models predict on the holdout set, and those predictions train the meta model.
3. **For a new instance:** the base models predict → their predictions go through the meta model → final prediction.

---

## Key terms

| Term | Meaning (as used in the course) |
|---|---|
| **Artificial intelligence** | A system that behaves intelligently; its own kind of intelligence, not human intelligence |
| **Machine learning** | A subset of AI: algorithms that learn rules and patterns from data |
| **Deep learning** | A subset of ML built on neural networks |
| **Algorithm vs. model** | An algorithm is untrained; a model is the algorithm after training on data |
| **Features (x) / label (y)** | Inputs to the model / the value it predicts |
| **Loss** | How far predictions are from the true labels; used to adjust parameters |
| **Unseen / test data** | Data not used in training; used to judge real-world performance |
| **Overfitting** | A model too specific to its training data, which generalizes poorly |
| **R²** | Coefficient of determination; the share of variance a regression captures (0–1) |
| **Accuracy / precision / recall** | Share of all predictions correct / share of predicted positives correct / share of actual positives found |
| **Confusion matrix** | A table of actual vs. predicted classes |
| **Elbow method** | Picking the number of clusters where improvement starts to slow |
| **Silhouette score** | Average of per-point silhouette coefficients (−1 to 1); higher = better clusters |
| **Logistic regression** | A classification model that fits an S-curve of probabilities |
| **Decision tree** | A tree of variables and thresholds used to reach a decision |
| **Ensemble learning** | Combining many weak learners: bagging, boosting, stacking |
| **AI Winter** | Late 1970s to early 1990s, when AI funding and interest dried up |

---

*Source: course transcript "Artificial Intelligence and Machine Learning" (11 videos).*

[← Previous chapter](02-introduction-to-gpt-models.md) · [Back to contents](../README.md) · [Next chapter →](04-deep-learning-and-neural-networks.md)
