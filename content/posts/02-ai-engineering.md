+++
tags = ['AI', 'AI Engineering by Chip Huyen', 'LLM', 'Learning']
title = 'NOTES: AI Engineering by Chip Huyen: Chapter 2'
date = 2025-09-13T14:05:07+01:00
draft = true
+++

[AI Engineering by Chip Huyen](https://www.oreilly.com/library/view/ai-engineering/9781098166298/)

## Chapter 2. Understanding Foundation Models

- "...differences in foundation models can be traced back to decisions about training data, model architecture and size, and how they are post-trained to align with human preferences."
- Sampling explains a significant portion of AI behavior, including hallucinations and inconsistencies. However, the right sampling strategy will significantly boost a model's performance and reliability. It's a duel edged sword.

## Training Data

- "The “use what we have, not what we want” approach may lead to models that perform well on tasks present in the training data but not necessarily on the tasks you care about."
- data quality is over > data quantity once quantity reaches a sufficient size.

### Multilingual Models

> English dominates the internet. An analysis of the Common Crawl dataset shows that English accounts for almost half of the data (45.88%), making it eight times more prevalent than the second-most common language, Russian (5.97%) [Source][https://arxiv.org/abs/2304.05613]

- This a reflection of English becoming the international language of choice.
- "ChatGPT is more willing to produce misinformation in Chinese than in English." [Source][https://oreil.ly/LcBfx] This is a highly interesting emergent behavior, and I'd love to see deeper research into the links between cultural norms and model behavior. Do the LLM's personalities reflect the cultural zeitgeist as it switches languages?

### Domain-Specific Models

> One of the most famous domain-specific models is perhaps DeepMind’s AlphaFold, trained on the sequences and 3D structures of around 100,000 known proteins. NVIDIA’s BioNeMo is another model that focuses on biomolecular data for drug discovery. Google’s Med-PaLM2 combined the power of an LLM with medical data to answer medical queries with higher accuracy.

#### TIP

> Domain-specific models are especially common for biomedicine, but other fields can benefit from domain-specific models too.

## Modeling

### Model Architecture

- most common by far is transformer architecture

#### Transformer architecture

- At a high level, **seq2seq** contains an encoder that processes inputs and a decoder that generates outputs.

> The transformer architecture addresses both problems with the attention mechanism. The attention mechanism allows the model to weigh the importance of different input tokens when generating each output token. This is like generating answers by referencing any page in the book.

##### NOTE

> While the attention mechanism is often associated with the transformer model, it was introduced three years before the transformer paper.

- The transformer architecture dispenses with RNNs entirely.
- Inference for transformer-based language models consists of two steps:
  1.  Prefill: The model processes the input tokens in parallel.
  2.  Decode: The model generates one output token at a time.
- **Attention mechanism**:
  - "Under the hood, the attention mechanism leverages key, value, and query vectors:"
    - "Query vector (Q) represents the current state of the decoder at each decoding step."
    - "Key vector (K) represents a previous token."
    - "Value vector (V) represents the actual value of a previous token"

> The attention mechanism computes how much attention to give an input token by performing a dot product between the query vector and its key vector. A high score means that the model will use more of that page’s content (its value vector) when generating the book’s summary.

- Each token has key and value vectors, which means as context window expand, compute and storage requirements increases exponentially.
- "With multi-headed attention, the query, key, and value vectors are split into smaller vectors, each corresponding to an attention head."
- "Transformer block contains the attention module and the MLP (multi-layer perceptron) module"
- "Attention module consists of four weight matrices: query, key, value, and output projection."

> Naively, the number of position indices determines the model’s maximum context length. For example, if a model keeps track of 2,048 positions, its maximum context length is 2,048.

#### Other model architectures

- Growing in popularity: RWKV (Peng et al., 2023), an RNN-based model that can be parallelized for training.
- Long-range memory advantage is SSMs (state space models)\

> Mamba’s inference computation scales linearly with sequence length (compared to quadratic scaling for transformers). Its performance shows improvement on real data up to million-length sequences.

### Model Size

> In general, increasing a model’s parameters increases its capacity to learn, resulting in better models. Given two models of the same model family, the one with 13 billion parameters is likely to perform much better than the one with 7 billion parameters.

- For LLMs the best measurement for the training data is the number of tokens in the dataset, instead of the number of training samples. This weighs books and such higher than tweets.
- LLMs are trained using datasets in the order of trillions of tokens:
  - 1.4 trillion tokens for Llama 1
  - 2 trillion tokens for Llama 2
  - 15 trillion tokens for Llama 3
- "The number of tokens in a model’s dataset isn’t the same as its number of training tokens ... If a dataset contains 1 trillion tokens and a model is trained on that dataset for two epochs—an epoch is a pass through the dataset—the number of training tokens is 2 trillion."

#### Scaling law: Building compute-optimal models

- 3 major takeaways:
  1.  Model performance depends on the model size and the dataset size.
  2.  Bigger models and bigger datasets require more compute.
  3.  Compute costs money.
- "Given a compute budget, the rule that helps calculate the optimal model size and dataset size is called the Chinchilla scaling law, proposed in the Chinchilla paper..." [Source][https://arxiv.org/abs/2203.15556]
  - "They found that for compute-optimal training, you need the number of training tokens to be approximately 20 times the model size."

#### Scaling extrapolation

- A parameter can be learned by the model during the training process. A hyperparameter is set by users to configure the model and control how the model learns.
  - "A 2022 paper by Microsoft and OpenAI shows that it was possible to transfer hyperparameters from a 40M model to a 6.7B model." [Source][https://oreil.ly/sHwbw]

#### Scaling bottlenecks

> This means a three-orders-of-magnitude increase in model sizes between 2018 and 2021. Three more orders of magnitude growth would result in 100-trillion-parameter models.

- Two bottlenecks for scaling: **training data** and **electricity**
  - This is why nucellar power plants are back on the table in the US, and in part why private fusion research has seen a boom in funding and engineering interest. Electricity will literally be the frontier to modern technology, and the US electric grid is in a precarious position when compared to say China's excess power grid capacities.
- "Unique proprietary data—copyrighted books, translations, contracts, medical records, genome sequences, and so forth—will be a competitive advantage in the AI race."
  - At the time of writing this, Anthropic just settled it's class action lawsuit with publishers for illegal use of books in their training data, as they pirated the copies. Where Meta has recently won their piracy case due to proving they never seeded during the piracy timeframe (a rather unique defense that I'm sure will have no future consequence toward IP protection.)
- "As of this writing, data centers are estimated to consume 1–2% of global electricity. This number is estimated to reach between 4% and 20% by 2030 (Patel, Nishball, and Ontiveros, 2024)."

## Post-Training

- Most post-training consists of two steps:
  1.  "Supervised finetuning (SFT): Finetune the pre-trained model on high-quality instruction data to optimize models for conversations instead of completion."
  2.  "Preference finetuning: Further finetune the model to output responses that align with human preference. Preference finetuning is typically done with reinforcement learning (RL)."
- "Some people compare pre-training to reading to acquire knowledge, while post-training is like learning how to use that knowledge."
  ![Shoggoth with a smiley face](https://pbrazeale.github.io/images/Shoggoth_smiley_face.jpg)

### Supervised Finetuning

- Appropriate responses examples: (_prompt, response_) and are called _demonstration data_.

> Companies, therefore, often use highly educated labelers to generate demonstration data. Among those who labeled demonstration data for InstructGPT, ~90% have at least a college degree and more than one-third have a master’s degree. If labeling objects in an image might take only seconds, generating one (prompt, response) pair can take up to 30 minutes, especially for tasks that involve long contexts like summarization.

### Preference Finetuning

- RLHF
  1.  Train a reward model that scores the foundation model’s outputs.
  2.  Optimize the foundation model to generate responses for which the reward model will give maximal scores.

> “the superior writing abilities of LLMs, as manifested in surpassing human annotators in certain tasks, are fundamentally driven by RLHF” (Touvron et al., 2023).

#### Reward model

> Llama-2 author Thomas Scialom shared that each comparison cost them $3.50. This is still much cheaper than writing responses, which cost $25 each.

## Sampling

- "Sampling makes AI’s outputs probabilistic. Understanding this probabilistic nature is important for handling AI’s behaviors, such as inconsistency and hallucination."

### Sampling Fundamentals

- "Always picking the most likely outcome = is called greedy sampling."

### Sampling Strategies

- "One sampling strategy can make the model generate more creative responses, whereas another strategy can make its generations more predictable."

#### Temperature

- "Intuitively, a higher temperature reduces the probabilities of common tokens, and as a result, increases the probabilities of rarer tokens."
  - For early 3.5 models this was the key to generating sales copy that actually mimicked human style, and resulted in higher conversions than human generated sales copy.

#### Top-k

> ... we pick the top-k logits and perform softmax over these top-k logits only. Depending on how diverse you want your application to be, k can be anywhere from 50 to 500—much smaller than a model’s vocabulary size.

#### Top-p

- "Top-p, also known as nucleus sampling, allows for a more dynamic selection of values to be sampled from."

### Test Time Compute

> To avoid biasing toward short sequences, you can use the average logprob by dividing the sum of a sequence by its length. After sampling multiple outputs, you pick the one with the highest average logprob. As of this writing, this is what the OpenAI API uses.

- OpenAI trained verifiers and found them highly effective. "In fact, the use of verifiers resulted in approximately the same performance boost as a 30× model size increase."
- "A model is considered robust if it doesn’t dramatically change its outputs with small variations in the input. The less robust a model is, the more you can benefit from sampling multiple outputs."

### Structured Outputs

- "Tasks requiring structured outputs. The most common category of tasks in this scenario is semantic parsing."
- "Tasks whose outputs are used by downstream applications. In this scenario, the task itself doesn’t need the outputs to be structured, but because the outputs are used by other applications, they need to be parsable by these applications."
  - This is what I deal with on a daily basis, and have found JSON to be the cleanest solution thus far.

#### Prompting

- Controlling the structured output by providing precise instructions with example of mandatory output structure works well, but there is no 100% accuracy with LLMs that I've found.
- Using an LMM to verify the first output can guarantee the 100% compliance buy at more than double the cost.

#### Post-processing

- "Post-processing works only if the mistakes are easy to fix. This usually happens if a model’s outputs are already mostly correctly formatted, with occasional small errors."
  - This was the approach I discovered and used for the 80,000+ part descriptions project I handled for World Parts Direct a few weeks back.

#### Constrained sampling

- "Constraint sampling is a technique for guiding the generation of text toward certain constraints. It is typically followed by structured output tools."

#### Finetuning

- "While simple finetuning doesn’t guarantee that the model will always output the expected format, it is much more reliable than prompting."
  - With the release of GPT-5 I've found that prompt adherence significantly improved over the 4x model I'd been using.

### The Probabilistic Nature of AI

- "The way AI models sample their responses makes them probabilistic." One reason hallucinations and random errors are guaranteed, and built into the way the models work.
  - Inconsistency is when a model generates very different responses for the same or slightly different prompts.
  - Hallucination is when a model gives a response that isn’t grounded in facts.

#### Inconsistency

"Model inconsistency manifests in two scenarios":

1. "Same input, different outputs: Giving the model the same prompt twice leads to two very different responses."
2. "Slightly different input, drastically different outputs: Giving the model a slightly different prompt, such as accidentally capitalizing a letter, can lead to a very different output."

#### Hallucination

- Two hypotheses about model hallucinations:
  1.  "Language model hallucinates because it can’t differentiate between the data it’s given and the data it generates." [Source][https://arxiv.org/abs/2110.10819#deepmind]
      - "Ortega and the other authors called hallucinations a form of self-delusion."
  2.  "... hallucination is caused by the mismatch between the model’s internal knowledge and the labeler’s internal knowledge." [Source][https://oreil.ly/9idN4]

> John Schulman ... proposed two solutions. One is verification: for each response, ask the model to retrieve the sources it bases this response on. Another is to use reinforcement learning. Remember that the reward model is trained using only comparisons—response A is better than response B—without an explanation of why A is better. Schulman argued that a better reward function that punishes a model more for making things up can help mitigate hallucinations.

> The rest of this book will explore how to make AI engineering, if not deterministic, at least systematic. The first step toward systematic AI engineering is to establish a solid evaluation pipeline to help detect failures and unexpected changes.

## Terms:

- **Sampling** is how a model chooses an output from all possible options.
- **Transformer** is a neural network architecture based on the multi-head [attention](<https://en.wikipedia.org/wiki/Attention_(machine_learning)> "Attention (machine learning)") mechanism, in which text is converted to numerical representations called [tokens](https://en.wikipedia.org/wiki/Large_language_model#Tokenization "Large language model"), and each token is converted into a vector via lookup from a [word embedding](https://en.wikipedia.org/wiki/Word_embedding "Word embedding") table. [Source][https://en.wikipedia.org/wiki/Transformer_(deep_learning_architecture)]
- **RNNs** (recurrent neural networks)
- **MLP** (multi-layer perceptron)
- **GANs** (generative adversarial networks)
- **SSMs** (state space models)
- **MoE** mixture-of-experts: model is divided into different groups of parameters, and each group is an expert. Only a subset of the experts is active for (used to) process each token.
- **FLOP**: floating point operation.
- **Hyperparameter**: set by users to configure the model and control how the model learns
- **SFT**: Supervised finetuning
- **RL**: reinforcement learning
- _Demonstration data_: prompt, response examples for training data
- **RLHF**: reinforcement learning from human feedback
- **PPO**: proximal policy optimization, a reinforcement learning algorithm released by OpenAI in 2017
- **Logprobs**, short for log probabilities, are probabilities in the log scale.
