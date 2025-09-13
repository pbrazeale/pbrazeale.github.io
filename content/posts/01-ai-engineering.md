+++
tags = ['AI', 'AI Engineering by Chip Huyen', 'LLM', 'Learning']
title = 'NOTES: AI Engineering by Chip Huyen: Chapter 1'
date = 2025-08-02T09:05:07+01:00
draft = false
+++

[AI Engineering by Chip Huyen](https://www.oreilly.com/library/view/ai-engineering/9781098166298/)

## Introduction to Building AI Applications with Foundation Models

- **Scale** the one word for AI post 2020.
- AI Engineering is one of the fastest growing disciplines.
- AI isn't new. Long before LLMs there was ML doing the hard work of data analysis.
- Future prediction is impossible, as we're closing on the black swan. (Singularity moment)
- [OpenAI Tokenizer](https://platform.openai.com/tokenizer)
  - GPT4 is about 3/4 word to token, or 75 words per 100 tokens.
    - It's vocabulary is 100,256

### Note

Why token instead of words?

1. tokens carry unique meaning. Cooking = "cook", "ing"
2. fewer unique tokens compared to words
   - The OED is the definitive record of the English language, featuring **600,000 words**, 3 million quotations, and over 1,000 years of English.
3. tokenization helps the model understand and learn unkown words.

- LLMs come in two flavors: _masked language models_ and _autoregressive language models_
  - masked is mostly used for "sentiment analysis and text classification"
  - autoregressive language models is the most common, and what most are familiar with from Chat GPT
- "In self-supervised learning, labels are inferred from the input data. In unsupervised learning, you don’t need labels at all."
- GPT-2 was 1.5 billion parameters, at time of book, 100 billion is now considered "large"
-

## From Large Language Models to Foundation Models

- Gemini and GPT-4V are sometimes called LLMs, but should better be known as foundation models.
  - These are the multimodal models
- essentially embeddings are vectors that aim to capture the meanings of the original data
- foundation models mark the transition to general purpose models, instead of task specific models.

## From Foundation Models to AI Engineering

- AI engineering is the process of building applications on top of foundation models.
  - This differs from ML engineering or MLOps, as AI engineering uses preformed models, and MLOps builds their own.
- Three major factors leading to AI Engineering as it's own specialized discipline:
  - Factor 1: General-purpose AI capabilities
  - Factor 2: Increased AI investments
    - "200 billion globally by 2025" this was way under estimated!
  - Factor 3: Low entrance barrier to building AI applications
    - In a September 2022 interview, Sam Altman, CEO of OpenAI, said that the biggest opportunity for the vast majority of people will be to adapt these models for specific applications.
      - _This has proven out in my experience._

### WHY THE TERM “AI ENGINEERING?”

- Most people preferred AI engineering. I decided to go with the people.

## Foundation Model Use Cases

- "The number of potential applications that you could build with foundation models seems endless."
  - Based on my experience if you can write out an operational manual for the processes of the task/position you can automate the position using AI to at least 80% effectiveness. Mostly it comes down to risk tolerance of errors and financial decision points to decide when/where an organization wants to place the human in the loop (if at all).

> [Eloundou et al. (2023)](https://arxiv.org/abs/2303.10130) has excellent research on how exposed different occupations are to AI. They defined a task as exposed if AI and AI-powered software can reduce the time needed to complete this task by at least 50%. An occupation with 80% exposure means that 80% of the occupation’s tasks are exposed. According to the study, occupations with 100% or close to 100% exposure include interpreters and translators, tax preparers, web designers, and writers ... Not unsurprisingly, occupations with no exposure to AI include cooks, stonemasons, and athletes. This study gives a good idea of what use cases AI is good for. [Source][https://arxiv.org/abs/2303.10130]

### Coding

- "[Jensen Huang, CEO of NVIDIA](https://oreil.ly/zUpGu), predicts that AI will replace human software engineers and that we should stop saying kids should learn to code."
- "[AWS CEO Matt Garman](https://oreil.ly/Hz_3i) shared that in the near future, most developers will stop coding."
- "[McKinsey](https://oreil.ly/aqUmX) researchers found that AI can help developers be twice as productive for documentation, and 25–50% more productive for code generation and code refactoring."
- Based on her research and feedback from the many engineers she has interviewed, "AI is much better at frontend development than backend development."
  - My initial instinct is that this stems from frontend programming having been converted into mostly framework plug-and-play coding; whist the UI has become easily replicable with the AI Image generation. However, as my frontend experience is highly limited, this is pure speculation on my part.

### Image and Video Production

- AI is highly efficient at these tasks, and the increased volume of production allows for rapid testing in marketing efforts, streamlining the process and ultimately increasing ROI.

### Writing

> MIT study ([Noy and Zhang, 2023](https://oreil.ly/IzQ6F)) assigned occupation-specific writing tasks to 453 college-educated professionals and randomly exposed half of them to ChatGPT. Their results show that among those exposed to ChatGPT, the average time taken decreased by 40% and output quality rose by 18%.

> In June 2023, [NewsGuard](https://oreil.ly/mZKjr) identified almost 400 ads from 141 popular brands on junk AI-generated websites. One of those junk websites produced 1,200 articles a day.

### Education

- Ai promises the offer the highest quality education we've even seen by crafting tailed tutoring to each student. The sort of education that use to be reserved for the children of the ultra wealthy. The future is one-on-one education where AI is the instructor and Teachers become advisors with the students to help them learn how to get the most out of the AI agents.

> If the risk is that AI can replace many skills, the opportunity is that AI can be used as a tutor to learn any skill. For many skills, AI can help someone get up to speed quickly and then continue learning on their own to become better than AI.

### Information Aggregation

- "According to Salesforce’s 2023 Generative AI Snapshot Research, 74% of generative AI users use it to distill complex ideas and summarize information."
- Information aggregation and distillation can reduce the burden on middle management for larger organizations.

> The more information you gather, the more important it is to organize it. Information aggregation goes hand in hand with data organization.

### Data Organization

- "AI can automatically generate text descriptions about images and videos, or help match text queries with visuals that match those queries."
- Data analysis is one of the key strengths of AI. It can generate insightful data visualizations, label outliers, and extrapolate trends to make forecast predictions.
  - Data analysist and Data Scientists are highly expose to AI automation and replacement, and must adapt to using AI to leverage their skills and drastically increase their output.
- "It’s estimated that the IDP, intelligent data processing, industry will reach $12.81 billion by 2030, growing 32.9% each year.[Source][https://oreil.ly/vnDNK]"

### Workflow Automation

- This is literally my day job, and it's proven to be highly impactful. And I've only just begun to hit the midlevel tasks. Only automating the simplest of tasks increased productivity by over 20% across the customer service team. That's before counting the secondary effects of eliminating the tedious tasks from the staff's plate, allowing them to focus on the more mentally engaging work; thus increasing work satisfaction. Could easily be looking at 30% productivity improvements when factoring 2nd order effects.
- Agents are the AI with access to tools to accomplish tasks with minimal or zero human input. (perhaps just final approval at key decision points, like a manager signoff.)

## Planning AI Applications

> However, if you’re doing this for a living, it might be worthwhile to take a step back and consider why you’re building this and how you should go about it. It’s easy to build a cool demo with foundation models. It’s hard to create a profitable product.

### Use Case Evaluation

1. If you don’t do this, competitors with AI can make you obsolete.
   - This is a factor of the company's core service and how exposed it is to AI disruption. Marketing companies for instance are having their business slashed as it has never been easier to roll that function internally for organizations. Two or three fresh college grads can become an entire marketing department now with the power of AI, and for a fraction of the traditional cost of Marketing firms.
2. If you don’t do this, you’ll miss opportunities to boost profits and productivity.
   - Essentially the ability to automate large portions of any position that can be defined in the Operations Manual.
3. You’re unsure where AI will fit into your business yet, but you don’t want to be left behind.
   - This is really an R&D project for large corporations, and not relevant to small and medium companies; unless they're a startup with the purpose of trying to disrupt an industry.

#### The role of AI and humans in the application

- Critical or complementary
  - For now AI mistakes are tolerated more when AI is complementary to the product. However, the most valuable applications/services are the ones built upon AI and wouldn't function without it.
- Reactive or proactive
  - Reactive happens instantly in response to user input; where proactive is a feature that happens automatically based on conditions the user in unaware of.
  - "Because users don’t ask for proactive features, they can view them as intrusive or annoying if the quality is low. Therefore, proactive predictions and generations typically have a higher quality bar."
- Dynamic or static
  - Microsoft (2023) proposed a framework for gradually increasing AI automation
    1. Crawl means human involvement is mandatory.
    2. Walk means AI can directly interact with internal employees.
    3. Run means increased automation, potentially including direct AI interactions with external users.

#### AI product defensibility

- "This also means that if the underlying models expand in capabilities, the layer you provide might be subsumed by the models, rendering your application obsolete."
  - Literally my biggest fear with the development of SARAH.
- "In AI, there are generally three types of competitive advantages: technology, data, and distribution—the ability to bring your product in front of users."
  - My advantage is the distribution as I have a built in audience and an excellent reputation within the community at large.
  - Given time data will also become part of my moat as I'll gain refined outputs and aggregate the best refined prompts based on several datapoints (that I'll not be sharing here LOL)

> Many startups eventually overtake bigger competitors, starting by building a feature that these bigger competitors overlooked.

### Milestone Planning

> It took them (LinkedIn) one month to achieve 80% of the experience they wanted. This initial success made them grossly underestimate how much time it’d take them to improve the product. They found it took them four more months to finally surpass 95%. A lot of time was spent working on the product kinks and dealing with hallucinations. The slow speed of achieving each subsequent 1% gain was discouraging. [Source][https://www.linkedin.com/blog/engineering/generative-ai/musings-on-building-a-generative-ai-product]

### Maintenance

- Must constantly evaluate ROI of model usage and 3rd party services
- All models have a shelf life. Prompting and workflow design is forever in flux as you must adapt to new improved models.
- Inference cost changes will constantly result in a market competition struggle between increased ROI and reduced consumer subscriptions. Meaning modeling future revenue cycles is hard.
- IP law is still a high concern as the courts change their interpretations of generated content ownership.
  - Though the latest rulings from the federal courts seem to lean toward all models allowed to use any IP they need, and thus outputs belong to the end user creating the output with the copyrighted prompts.

## The AI Engineering Stack

> Existing ML engineers can add AI engineering to their lists of skills to expand their job prospects. However, there are also AI engineers with no previous ML experience.

### Three Layers of the AI Stack

1. Application development
   - "Application development involves providing a model with good prompts and necessary context. This layer requires rigorous evaluation."
2. Model development
   - "This layer provides tooling for developing models, including frameworks for modeling, training, finetuning, and inference optimization. Because data is central to model development, this layer also contains dataset engineering."
3. Infrastructure
   - "At the bottom is the stack is infrastructure, which includes tooling for model serving, managing data and compute, and monitoring."

- AI applications still need to solve business problems

### AI Engineering Versus ML Engineering

- Building applications with foundation models differ from traditional ML engineering in 3 key ways:
  1.  "With AI engineering, you use a model someone else has trained for you."
  2.  "AI engineering works with models that are bigger, consume more compute resources, and incur higher latency than traditional ML engineering." Meaning that understanding the underlining hardware and how to maximize performance has never been more important. Minor efficiency gains per prompt, results in massive savings across time.
  3.  "AI engineering works with models that can produce open-ended outputs. Open-ended outputs give models the flexibility to be used for more tasks, but they are also harder to evaluate. This makes evaluation a much bigger problem in AI engineering." As such we must spend more time analyzing the results and tweaking the inputs to maximize outputs. Where ML Engineering is almost always a blue ocean experience. AI Engineering is highly competitive and results are easily compared to competitors. This means wins are bigger, but also failures are easier to be held accountable for. The engineering bar has been raised, and it's our responsibility to meet it.
- Model adaptation:
  1.  "Prompt-based techniques, which include prompt engineering, adapt a model without updating the model weights."
  2.  "Finetuning, on the other hand, requires updating model weights."

#### Model development

- Most commonly associated with ML Engineering:
  1.  Modeling and training
      - PyTorch
      - Pre-training and Finetuning
  2.  Dataset engineering
      - Curating, generating, and annotating the data needed for training and adapting AI models.
  3.  Inference optimization
      - Making models faster and cheaper

#### Application development

> With traditional ML engineering, where teams build applications using their proprietary models, the model quality is a differentiation. With foundation models, where many teams use the same model, differentiation must be gained through the application development process.

1. Evaluation
   - Mitigate risk, and discover opportunities.
   - While it was important in ML engineering, it's magnified within AI engineering "these challenges chiefly arise from foundation models’ open-ended nature and expanded capabilities."
   -
2. Prompt engineering
   - It's about creating desired behavior without changing the model weights. This is where I have the most experience; and what provides my competitive advantage in the market.
3. AI interface
   - The UI for users to interface with the AI application.
   - APIs are becoming vital for building out the tools for true AI Agents.

##### Table 1-6 The importance of different categories in app development for AI engineering and ML engineering.

|                    |                              |                                 |
| ------------------ | ---------------------------- | ------------------------------- |
| Category           | Building with traditional ML | Building with foundation models |
| AI interface       | Less important               | Important                       |
| Prompt engineering | Not applicable               | Important                       |
| Evaluation         | Important                    | More important                  |

### AI Engineering Versus Full-Stack Engineering

> The increased emphasis on application development, especially on interfaces, brings AI engineering closer to full-stack development.

- I've never used more JavaScript than I have in the past two months, and we're considered a Python shop.
- "An advantage that full-stack engineers have over traditional ML engineers is their ability to quickly turn ideas into demos, get feedback, and iterate."
- The new paradigm is to build the application first with a foundation model, and once feedback justifies the investment into the idea, expand into model finetuning or development.
  - AI engineers are tightly tied into the product development, where historically ML engineers were completely separated from product development.

## Terms

- **Language model**: encodes statistical information about one or more languages
- **Model as a service**: e.g., OpenAI
- **Self-supervision**: model training without external labels
- **Token**: a character, word, or portion of a word
- **Tokenization**: text → tokens
- **Model’s vocabulary**: the set of tokens a model can understand and use
- **Masked language model**: predicts missing words when given part of a sentence (e.g., limericks)
- **Autoregressive LM**: predict next token
- **Foundation models**: massive deep learning models with emergent capabilities [Source][https://arxiv.org/abs/2108.07258]
- **Multimodal (LMM)**: generative models across text, image, video
- **RAG**: retrieval-augmented generation
- **HITL**: human-in-the-loop, involving humans in AI’s decision-making processes.
