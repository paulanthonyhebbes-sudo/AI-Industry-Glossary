# AI Industry Glossary

Oct 5, 2026 ·

## How to use this glossary

The terms are grouped into twelve layers that run from physical chips at the bottom to applications, evaluation and governance at the top, plus a final section of industry slang. Each layer depends on the ones beneath it: hardware runs training, training produces models, inference serves models, and applications are built on top.

Within each table, terms run roughly from foundational to advanced.

Read from the bottom up: each rung relies on the ones below, while evaluation and safety apply to the whole stack.

## Layer 1 – Hardware & Compute

AI is mostly very large amounts of matrix maths, so the chips and memory that do it fastest set the limits on what everything above can achieve.

| Term | What it means |
| --- | --- |
| **Compute** | Shorthand for the processing power used to train or run models. Often the scarcest and most expensive resource in AI. |
| **CPU** | Central Processing Unit. A general-purpose processor that handles a few tasks very quickly in sequence. Too slow for training large models, but can run small ones. |
| **GPU** | Graphics Processing Unit. A chip that performs thousands of simple calculations in parallel, which makes it ideal for neural networks. Nvidia dominates this market. |
| **Accelerator** | Umbrella term for any chip built to speed up AI work: GPUs, TPUs, NPUs and custom ASICs. |
| **TPU** | Tensor Processing Unit. Google's custom AI chip, designed specifically for the matrix maths in neural networks. |
| **ASIC** | Application-Specific Integrated Circuit. A chip designed for one job. TPUs and Amazon's Trainium are AI ASICs. |
| **NPU** | Neural Processing Unit. A small, power-efficient AI accelerator built into phones and laptops for on-device features. |
| **Tensor cores** | Specialised units inside modern Nvidia GPUs that accelerate matrix multiplication at low precision. |
| **FLOPS / FLOPs** | Floating-point operations per second (a speed) or in total (an amount). Training runs are measured in total FLOPs, for example 10^25. |
| **VRAM** | Video RAM, the memory on a graphics card. It decides the largest model you can load on a GPU. |
| **HBM** | High Bandwidth Memory. Very fast stacked memory used on data-centre GPUs. Its supply is a major industry bottleneck. |
| **Memory bandwidth** | How fast data moves between memory and the processor, in GB/s. For LLM inference it usually limits tokens per second more than raw compute does. |
| **Unified memory** | A design, such as Apple Silicon, where CPU and GPU share one pool of RAM. It lets laptops run larger models than their GPU alone could hold. |
| **CUDA** | Nvidia's software platform for programming its GPUs. Its maturity is a key reason for Nvidia's market lock-in. Rivals include AMD ROCm, Apple Metal and Vulkan. |
| **Interconnect** | High-speed links that join chips and servers, such as NVLink inside a server and InfiniBand or Ethernet between servers. |
| **Data centre** | A facility housing thousands of servers. AI data centres are increasingly sized by power draw, from megawatts up to gigawatts. |
| **Edge device** | Hardware that runs AI locally rather than in the cloud, such as phones, cameras and IoT sensors. |

## Layer 2 – Infrastructure & Distributed Systems

No single chip can train a frontier model, so this layer is about joining thousands of them together and keeping models running reliably in production.

| Term | What it means |
| --- | --- |
| **Cluster** | Many GPU servers networked together to act as one large machine. Frontier training clusters contain tens or hundreds of thousands of GPUs. |
| **Distributed training** | Splitting a training job across many chips so it finishes in weeks rather than decades. |
| **Data parallelism** | Each chip holds a full copy of the model and trains on a different slice of the data, then they share what they learned. |
| **Tensor parallelism** | Splitting the maths inside each layer across several chips, used when a single layer is too big for one chip. |
| **Pipeline parallelism** | Placing different layers on different chips and passing data along them like an assembly line. |
| **Hyperscaler** | The largest cloud providers: AWS, Microsoft Azure and Google Cloud. |
| **Neocloud** | Newer cloud providers that specialise in renting GPUs, such as CoreWeave and Lambda. |
| **GPU-hour** | The standard unit for renting compute: one GPU used for one hour. |
| **Framework** | A software library for building and training neural networks. PyTorch is dominant; JAX and TensorFlow are the main alternatives. |
| **Containerisation** | Packaging a model with all its dependencies, usually with Docker, so it runs identically anywhere. |
| **Kubernetes / Slurm** | Schedulers that allocate jobs across a cluster. Kubernetes is common for serving; Slurm is common for research training. |
| **MLOps** | The practices and tools for deploying, monitoring and updating ML models in production. Essentially DevOps for machine learning. |
| **Experiment tracking** | Logging each training run's settings and results so they can be compared, using tools such as Weights & Biases or MLflow. |
| **Model registry** | A versioned catalogue of trained models and their metadata, so teams know which model is in production. |
| **On-premises (on-prem)** | Running AI on hardware you own rather than renting from the cloud, often chosen for data privacy or cost control. |

## Layer 3 – Data

A model can only learn what is in its data, so the quantity, quality and preparation of data shape every model's strengths and blind spots.

| Term | What it means |
| --- | --- |
| **Dataset** | A structured collection of examples used to train or test a model. |
| **Corpus** | A large body of text used for training a language model, often trillions of tokens. |
| **Training / validation / test split** | Dividing data into a portion to learn from, a portion to tune settings on, and a held-back portion to measure final performance fairly. |
| **Feature** | A measurable input property in classic machine learning, such as house size when predicting price. |
| **Feature engineering** | Hand-crafting useful input features. Deep learning largely automates this by learning features itself. |
| **Label / annotation** | The correct answer attached to an example, such as 'cat' on a photo. Often produced by human annotators. |
| **Ground truth** | The verified correct answer that a model's output is compared against. |
| **Token** | The basic unit a language model reads and writes. Usually a word or part of a word; in English, roughly 0.75 words per token. |
| **Tokenisation** | Breaking text into tokens before the model processes it. |
| **Tokeniser / vocabulary** | The tool and fixed list of tokens a model uses. Different model families use different tokenisers, so token counts vary between them. |
| **BPE** | Byte-Pair Encoding. The most common tokenisation method, which merges frequent character pairs into single tokens. |
| **Web crawl** | Text gathered automatically from public websites. Common Crawl is the best-known open source of it. |
| **Data curation / filtering** | Removing low-quality, harmful or duplicate material from training data. Often matters more than adding volume. |
| **Deduplication** | Removing repeated content so the model does not over-learn or memorise it. |
| **Synthetic data** | Training data generated by AI models rather than collected from humans. Widely used now that high-quality human text is running short. |
| **Data pipeline / ETL** | The automated process that extracts, transforms and loads data into a form a model can use. |
| **Data drift** | When real-world data gradually changes after deployment, so a model's accuracy degrades over time. |
| **Data contamination** | When test questions leak into training data, inflating benchmark scores (see Layer 11). |

## Layer 4 – Machine Learning Fundamentals

Machine learning means a program improves at a task by adjusting itself against examples, rather than following rules a person wrote by hand.

| Term | What it means |
| --- | --- |
| **Artificial intelligence (AI)** | The broad field of making computers perform tasks that normally need human intelligence. Machine learning is its dominant approach today. |
| **Machine learning (ML)** | Systems that learn patterns from data instead of being explicitly programmed. |
| **Deep learning** | Machine learning using neural networks with many layers. It powers nearly all modern AI. |
| **Model** | The trained artefact that turns inputs into outputs. In practice, a file of learned numbers plus the architecture that uses them. |
| **Algorithm** | The procedure used to train a model. The algorithm is the recipe; the model is the dish. |
| **Supervised learning** | Learning from labelled examples, such as emails marked spam or not spam. |
| **Unsupervised learning** | Finding structure in unlabelled data, such as grouping customers by behaviour. |
| **Self-supervised learning** | Creating labels from the data itself, such as hiding the next word and predicting it. This is how LLMs are pre-trained. |
| **Reinforcement learning (RL)** | Learning by trial and error, guided by rewards for good outcomes and penalties for bad ones. |
| **Classification / regression** | Predicting a category (spam or not) versus predicting a number (a house price). |
| **Clustering** | Grouping similar items together without predefined labels. |
| **Parameters / weights** | The learned numbers inside a model. Model size is quoted in parameters, for example 8B means 8 billion. |
| **Hyperparameter** | A setting chosen by people before training, such as learning rate or batch size, rather than learned by the model. |
| **Loss function** | A score of how wrong the model's predictions are. Training aims to make this number as small as possible. |
| **Gradient descent** | The core training method: repeatedly nudge each weight in the direction that reduces the loss. |
| **Backpropagation** | The technique for working out how much each weight contributed to the error, so gradient descent knows which way to nudge it. |
| **Optimiser** | The algorithm that applies weight updates. AdamW is the most common for large models. |
| **Learning rate** | How big each weight update is. Too high and training becomes unstable; too low and it crawls. |
| **Batch / batch size** | The group of examples processed together before each weight update, and how many are in it. |
| **Epoch** | One complete pass through the training data. LLMs often train for about one epoch over their corpus. |
| **Overfitting** | When a model memorises its training data and performs poorly on new data. |
| **Underfitting** | When a model is too simple, or undertrained, to capture the real patterns. |
| **Generalisation** | A model's ability to perform well on data it has never seen. The real goal of training. |
| **Regularisation / dropout** | Techniques that discourage memorisation. Dropout randomly switches off parts of the network during training. |
| **Training vs inference** | Training is when a model learns; inference is when the finished model is used to make predictions (see Layer 8). |

## Layer 5 – Model Architectures

An architecture is the blueprint of a neural network; since 2017 the transformer has been the blueprint behind almost every major language model.

| Term | What it means |
| --- | --- |
| **Neural network** | Layers of simple connected units, loosely inspired by the brain, that transform inputs into outputs through weighted connections. |
| **Neuron / node** | A single unit that combines its weighted inputs and passes the result on. |
| **Layer** | A set of neurons at the same depth. Data flows from the input layer, through hidden layers, to the output layer. |
| **Activation function** | A small non-linear function applied in each neuron, such as ReLU or GELU. Without it, a deep network could only learn straight-line relationships. |
| **CNN** | Convolutional Neural Network. Scans data with small filters to detect local patterns. The classic architecture for images. |
| **RNN / LSTM** | Recurrent networks that process sequences one step at a time while carrying a memory. Largely replaced by transformers for text. |
| **Transformer** | The architecture introduced in the 2017 paper Attention Is All You Need. It processes all tokens in parallel using attention, and it is the T in GPT. |
| **Attention / self-attention** | The mechanism that lets each token weigh how relevant every other token is to it, so meaning comes from context. |
| **Multi-head attention** | Running several attention calculations side by side so the model can track different relationships at once, such as grammar and topic. |
| **Positional encoding** | Extra information added to tokens so the transformer knows word order. RoPE is the common modern method. |
| **Encoder / decoder** | An encoder turns input into an internal representation; a decoder generates output from it. Most chat LLMs are decoder-only. |
| **Autoregressive** | Generating output one token at a time, each based on all the tokens before it. |
| **Next-token prediction** | The single task an LLM is trained on: predict the most likely next token. Remarkable abilities emerge from doing this at scale. |
| **Embedding** | A list of numbers (a vector) that represents the meaning of a token, sentence or image. Similar meanings sit close together. |
| **Vector** | An ordered list of numbers. The basic data structure that models work with internally. |
| **Latent space** | The internal space of learned representations where a model organises concepts. |
| **Mixture of Experts (MoE)** | An architecture with many specialist sub-networks where only a few are used per token. It gives large-model quality at lower running cost. |
| **Total vs active parameters** | In an MoE model, total is every parameter stored; active is the subset used per token. For example, 120B total, 5B active. |
| **Diffusion model** | Generates images, audio or video by starting from random noise and refining it step by step. Behind most image generators. |
| **GAN** | Generative Adversarial Network. Two networks compete, one generating fakes and one detecting them. Largely superseded by diffusion. |
| **State space model (SSM)** | An alternative to attention, such as Mamba, that handles very long sequences more efficiently. Often combined with transformers in hybrid models. |
| **Multimodal** | A model that handles more than one type of data, such as text, images, audio and video. |
| **Vision-language model (VLM)** | A multimodal model that can see images and talk about them. |
| **World model** | A model that learns how an environment behaves so it can predict or simulate what happens next. Used in robotics and video generation. |

## Layer 6 – Training & Post-Training

Modern LLMs are built in two stages: costly pre-training gives broad knowledge, then post-training turns that raw model into a helpful, safe assistant.

| Term | What it means |
| --- | --- |
| **Pre-training** | The first, most expensive stage: training on a huge corpus to predict the next token. It produces broad knowledge and language skill. |
| **Base model** | The raw result of pre-training. It continues text rather than following instructions. |
| **Training run** | One complete training job. Frontier runs can take months and cost hundreds of millions of dollars. |
| **Checkpoint** | A saved snapshot of a model's weights partway through or at the end of training. |
| **Scaling laws** | The observed pattern that model performance improves predictably as data, parameters and compute increase. |
| **Compute-optimal (Chinchilla)** | The finding that, for a fixed budget, model size and training data should grow together. Roughly 20 tokens per parameter is the classic ratio. |
| **Post-training** | Everything after pre-training that shapes behaviour: fine-tuning, preference training and safety training. |
| **Fine-tuning** | Continuing to train an existing model on a smaller, focused dataset to specialise it. |
| **Supervised fine-tuning (SFT)** | Fine-tuning on example prompts paired with ideal responses written or approved by people. |
| **Instruction tuning** | SFT aimed at teaching a model to follow instructions. It turns a base model into an instruct model. |
| **Transfer learning** | Reusing knowledge learned on one task for another. Fine-tuning is the most common form. |
| **RLHF** | Reinforcement Learning from Human Feedback. People rank model responses, and the model is trained to produce the kinds they prefer. |
| **Reward model** | A separate model trained to predict how much people would like a response. It scores outputs during RLHF. |
| **RLAIF** | Reinforcement Learning from AI Feedback. Like RLHF, but another AI model supplies the preference judgements. |
| **Constitutional AI** | Anthropic's method of training a model to critique and improve its own responses against a written set of principles. |
| **DPO** | Direct Preference Optimisation. A simpler alternative to RLHF that learns directly from preferred-versus-rejected answer pairs without a reward model. |
| **RLVR** | Reinforcement Learning with Verifiable Rewards. Rewarding answers that can be checked automatically, such as maths results or passing code tests. Key to reasoning models. |
| **PEFT** | Parameter-Efficient Fine-Tuning. Methods that adjust only a small fraction of weights, making fine-tuning affordable on modest hardware. |
| **LoRA** | Low-Rank Adaptation. The most popular PEFT method. It trains small add-on matrices instead of the whole model. |
| **QLoRA** | LoRA applied to a quantised model, allowing large models to be fine-tuned on a single consumer GPU. |
| **Distillation** | Training a smaller student model to imitate a larger teacher model, keeping much of its ability at a fraction of the size. |
| **Continued pre-training** | Extra pre-training on domain-specific text, such as legal or medical documents, before fine-tuning. |
| **Catastrophic forgetting** | When fine-tuning on new material causes a model to lose abilities it had before. |
| **Model merging** | Combining the weights of two or more fine-tuned models into one without further training. Popular in the open-source community. |

## Layer 7 – Optimisation, Formats & Local AI

This layer makes trained models smaller, faster and portable, which is what lets a model built in a data centre run on a laptop.

| Term | What it means |
| --- | --- |
| **Precision** | How many bits are used to store each number. Fewer bits means less memory and faster maths, at some cost to accuracy. |
| **FP32 / FP16 / BF16** | 32-bit and 16-bit floating-point formats. BF16 (brain float) is the standard for training modern models. |
| **FP8 / FP4** | Very low-precision formats supported by recent data-centre GPUs, used to speed up training and inference. |
| **INT8 / INT4** | 8-bit and 4-bit integer formats, mostly used for quantised inference. |
| **Quantisation** | Converting a model's weights to lower precision, for example 16-bit to 4-bit, so it needs roughly a quarter of the memory with modest quality loss. |
| **Memory rule of thumb** | Model size in GB is roughly parameters (in billions) multiplied by bytes per weight. An 8B model is about 16 GB at FP16 and about 5 GB at 4-bit. |
| **Quant names (Q4\_K\_M, Q8\_0)** | Labels for GGUF quantisation levels. The number is bits per weight; K means a smarter mixed method; S, M and L mean small, medium and large variants. |
| **GPTQ / AWQ / EXL2** | Alternative quantisation methods, mainly for running models fully on Nvidia GPUs. |
| **Pruning** | Removing weights or whole parts of a network that contribute little, making the model smaller and faster. |
| **GGUF** | The single-file model format used by llama.cpp and tools built on it. The standard format for running models locally. |
| **Safetensors** | A safe, fast file format for storing model weights. The default on Hugging Face. |
| **ONNX** | Open Neural Network Exchange. A format for moving models between frameworks and hardware. |
| **MLX** | Apple's machine learning framework, optimised for running and fine-tuning models on Apple Silicon. |
| **llama.cpp** | The open-source C++ engine for running LLMs efficiently on ordinary CPUs and GPUs. The foundation of most local AI tools. |
| **Ollama** | A command-line tool that downloads and runs local models with one command and exposes them through a local API. |
| **LM Studio** | A desktop app for finding, downloading and chatting with local models through a graphical interface, with a built-in local server. |
| **vLLM** | A high-throughput inference server for running models at scale, widely used in production. SGLang and TensorRT-LLM are alternatives. |
| **GPU offloading** | Splitting a model between GPU and system RAM when it does not fit entirely in VRAM. It works, but runs more slowly. |
| **Local AI / on-device AI** | Running models on your own hardware rather than through a cloud API, for privacy, cost or offline use. |

## Layer 8 – Inference & Serving

Inference is the model at work, and its speed, cost and output style are controlled by the settings and techniques below.

| Term | What it means |
| --- | --- |
| **Inference** | Running a trained model to produce an output. Across the industry, inference now uses more compute than training. |
| **Prompt / completion** | The input text sent to a model and the output it generates in response. |
| **Context window** | The maximum number of tokens a model can consider at once, covering the prompt, conversation history and its reply. Ranges from a few thousand to over a million. |
| **Context rot** | The tendency for a model's accuracy to drop as its context fills up, even before the limit is reached. |
| **KV cache** | Stored attention calculations for tokens already processed, so they are not recomputed for each new token. Grows with context and uses lots of memory. |
| **Prefill vs decode** | Prefill processes the whole prompt at once (compute-heavy); decode generates the reply one token at a time (memory-bandwidth-heavy). |
| **TTFT** | Time To First Token. The delay before a reply starts appearing. Mostly driven by prefill. |
| **Tokens per second (tok/s)** | Generation speed. The headline metric in most local LLM benchmarks. |
| **Latency vs throughput** | Latency is how fast one user gets a response; throughput is how many tokens the system produces across all users. Serving often trades one for the other. |
| **Batching / continuous batching** | Processing many users' requests together on the same GPU to raise throughput. Continuous batching slots new requests in as others finish. |
| **Temperature** | Controls randomness. Low (0 to 0.3) gives focused, consistent answers; high (0.8 and above) gives more varied, creative output. |
| **Top-p (nucleus sampling)** | Restricts choices to the smallest set of tokens whose combined probability reaches p, for example 0.9. |
| **Top-k / min-p** | Restrict choices to the k most likely tokens, or to tokens above a minimum probability relative to the top one. |
| **Greedy decoding** | Always picking the single most likely next token. Deterministic but can be repetitive. |
| **Repetition penalty** | A setting that discourages the model from repeating the same words or phrases. |
| **Max tokens / stop sequence** | Limits that end generation after a set length or when a specific string appears. |
| **Streaming** | Sending tokens to the user as they are generated rather than waiting for the full reply. |
| **Speculative decoding** | A small, fast draft model guesses several tokens ahead and the large model checks them in one pass, speeding up output without changing it. |
| **FlashAttention** | A widely used technique that computes attention faster and with less memory by reorganising how the GPU reads data. |
| **Prompt caching** | Reusing the processed form of a repeated prompt prefix, such as a long system prompt, to cut cost and latency. |
| **Endpoint** | A URL where a hosted model accepts requests. |
| **Serverless inference** | Paying per request or per token for a hosted model without managing any servers. |
| **Rate limit** | A cap on how many requests or tokens an API user can send per minute or per day. |

## Layer 9 – Models & the Ecosystem

These terms describe the kinds of model on offer, how they are released and licensed, and where people find them.

| Term | What it means |
| --- | --- |
| **LLM** | Large Language Model. A transformer trained on vast text to understand and generate language. Usually billions of parameters or more. |
| **SLM** | Small Language Model. A compact model, typically under about 10B parameters, built to run cheaply or on-device. |
| **Foundation model** | A large general-purpose model trained on broad data that can be adapted to many tasks. |
| **Frontier model** | One of the most capable models at any given time, built by the leading labs. |
| **Generative AI** | AI that creates new content, such as text, images, audio, video or code, rather than only classifying or predicting. |
| **Base vs instruct / chat model** | A base model only continues text; an instruct or chat model has been post-trained to follow instructions and hold conversations. |
| **Reasoning model** | A model trained to think step by step before answering, spending extra tokens to solve harder problems in maths, code and logic. |
| **Chain of thought (CoT)** | The step-by-step working a model writes out before its final answer. |
| **Test-time compute** | Spending more compute while answering, for example longer thinking or several attempts, to get better results. Often controlled as a thinking budget or effort level. |
| **Parameter-count names (7B, 70B)** | Model sizes shown in names. B means billions of parameters; an MoE model may list total and active, such as 30B-A3B. |
| **Open weights** | A model whose trained weights are published for anyone to download and run, such as Llama, Qwen, Mistral, DeepSeek and gpt-oss. |
| **Open source AI** | Strictly, a model whose weights, code and training data details are all open. Many open-weights models do not meet this bar. |
| **Closed / proprietary model** | A model available only through its maker's app or API, such as Claude, GPT and Gemini. |
| **Licence** | The legal terms for using a model. Ranges from permissive (Apache 2.0, MIT) to custom licences with usage restrictions. |
| **Model card** | A document describing a model's intended use, training, evaluation results, limitations and safety testing. |
| **System card** | A detailed safety and capability report published alongside a frontier model release. |
| **Hugging Face** | The main online hub for sharing models, datasets and demos. Effectively the GitHub of AI. |
| **Fine-tune / derivative** | A community model built by fine-tuning someone else's base model, often for a niche task or style. |
| **Embedding model** | A model that converts text or images into vectors for search and comparison rather than generating text. |
| **Reranker** | A model that re-scores a list of search results by relevance. Commonly used in RAG pipelines. |
| **ASR / TTS** | Automatic Speech Recognition (speech to text, such as Whisper) and Text-To-Speech (text to spoken audio). |
| **Speech-to-speech / voice model** | A model that listens and replies in audio directly, enabling natural real-time voice conversations. |

## Layer 10 – Applications & Agents

The application layer turns a model into a useful product by feeding it the right context, connecting it to tools and data, and letting it act.

| Term | What it means |
| --- | --- |
| **API / SDK** | An API is the interface for sending requests to a hosted model; an SDK is a code library that makes calling it easier. |
| **Chatbot / assistant** | A conversational interface to a model, such as Claude, ChatGPT or Gemini. |
| **System prompt** | Hidden instructions given to a model before the conversation, setting its role, rules and tone. |
| **User prompt** | The message the person actually types. |
| **Prompt engineering** | Crafting prompts with clear instructions, examples and structure to get better outputs. |
| **Context engineering** | The broader discipline of deciding everything a model sees: instructions, retrieved documents, tool results and memory. |
| **Zero-shot / few-shot** | Asking a model to do a task with no examples, or with a few worked examples included in the prompt. |
| **Structured output / JSON mode** | Forcing a model to reply in a fixed machine-readable format so software can use the result reliably. |
| **RAG** | Retrieval-Augmented Generation. Searching a knowledge source for relevant passages and adding them to the prompt so answers are grounded in real, up-to-date information. |
| **Grounding** | Tying a model's answers to verifiable sources, which reduces hallucination. |
| **Chunking** | Splitting documents into smaller pieces before embedding them for retrieval. |
| **Vector database** | A database that stores embeddings and finds the most similar ones quickly, such as Pinecone, Chroma or pgvector. |
| **Semantic search** | Searching by meaning rather than exact keywords, using embeddings. |
| **Hybrid search** | Combining keyword search and semantic search for better retrieval. |
| **Tool use / function calling** | Letting a model request actions from external code, such as searching the web, querying a database or sending an email. |
| **MCP** | Model Context Protocol. An open standard, introduced by Anthropic, for connecting AI applications to tools and data sources through a common interface. |
| **Agent** | An AI system that pursues a goal over multiple steps, deciding which tools to use and acting with some autonomy. |
| **Agentic** | Describes AI that plans and takes actions rather than only answering questions. |
| **Agent loop** | The cycle an agent repeats: think, call a tool, observe the result, then decide the next step until the task is done. |
| **Harness / scaffolding** | The software around a model that supplies tools, memory and the agent loop. The same model can perform very differently in different harnesses. |
| **Multi-agent system** | Several agents working together, often an orchestrator that delegates parts of a task to specialist sub-agents. |
| **Computer use** | An agent operating a computer through screenshots, mouse clicks and typing, like a person would. |
| **Memory** | Information an AI application keeps between conversations, such as user preferences or project context. |
| **Skills** | Packaged instructions and resources that an agent can load to perform a specific kind of task well. |
| **A2A** | Agent-to-Agent protocol. A standard for agents from different vendors to communicate and delegate work to each other. |
| **Copilot** | An AI assistant embedded in another tool to help as you work, such as in a code editor or office suite. |
| **Coding agent** | An agent that reads, writes, runs and tests code across a whole project, such as Claude Code or Codex. |
| **Guardrails** | Rules, filters and checks around a model that block unsafe inputs or outputs. |
| **Human-in-the-loop** | Requiring a person to review or approve an AI's actions before they take effect, especially for risky steps. |

## Layer 11 – Evaluation & Benchmarks

Evaluation measures how good a model really is; benchmarks make comparison possible, but each one only captures a narrow slice of ability.

| Term | What it means |
| --- | --- |
| **Eval** | Any structured test of a model's performance or behaviour. Teams build custom evals for their own use cases. |
| **Benchmark** | A standard public test set used to compare models on the same tasks. |
| **Accuracy / precision / recall / F1** | Classic scoring metrics. Precision asks how many flagged items were right; recall asks how many right items were found; F1 balances the two. |
| **Perplexity** | How surprised a language model is by text. Lower is better; useful for comparing quantisation levels of the same model. |
| **Pass@k** | The chance that at least one of k attempts is correct. Common in coding benchmarks. |
| **MMLU** | Massive Multitask Language Understanding. Multiple-choice questions across 57 subjects. Now largely saturated. |
| **GPQA** | Graduate-level science questions designed so they cannot easily be looked up online. |
| **Humanity's Last Exam (HLE)** | A very hard expert-written exam spanning many fields, built to stay challenging as models improve. |
| **SWE-bench** | Tests whether a model can fix real bugs from GitHub projects. A key coding-agent benchmark, usually quoted as SWE-bench Verified. |
| **ARC-AGI** | Visual puzzles testing abstract reasoning on novel problems, which are easy for people and hard for AI. |
| **AIME** | Problems from a US maths competition, used to test mathematical reasoning. |
| **Agentic benchmarks** | Tests of multi-step tasks using tools, such as Terminal-Bench for command-line work and OSWorld for computer use. |
| **LMArena** | A public leaderboard, formerly Chatbot Arena, where people vote between two anonymous model responses. Rankings use Elo-style scores. |
| **LLM-as-a-judge** | Using a strong model to grade other models' outputs at scale instead of human reviewers. |
| **Human evaluation** | People rating outputs directly. Slow and costly but often the most trustworthy measure. |
| **Benchmark saturation** | When top models score near the maximum, so a benchmark can no longer separate them. |
| **Benchmaxxing** | Slang for tuning a model to top benchmarks at the expense of real-world usefulness. |
| **Ablation** | Removing one component or step to measure how much it contributes to performance. |
| **Vibe check** | Informal hands-on testing to see how a model feels to use. Common, unscientific and surprisingly influential. |

## Layer 12 – Safety, Ethics & Governance

This layer covers how models fail, how they are attacked, how researchers try to understand and control them, and how governments regulate them.

| Term | What it means |
| --- | --- |
| **AI safety** | The field focused on preventing AI systems from causing harm, from everyday errors to large-scale risks. |
| **Alignment** | Making an AI system's goals and behaviour match human intentions and values. |
| **Hallucination** | When a model states false information confidently, such as an invented citation or fact. |
| **Sycophancy** | A model's tendency to tell users what they want to hear rather than what is accurate. |
| **Bias** | Systematic unfairness in outputs, often inherited from patterns in training data. |
| **Fairness** | Ensuring AI outcomes do not unjustly disadvantage particular groups. |
| **Black box** | A system whose internal reasoning cannot easily be seen or explained. A common description of large neural networks. |
| **Explainability (XAI)** | Techniques that help people understand why a model produced a particular output. |
| **Interpretability** | Research into what is happening inside a model. Mechanistic interpretability tries to map specific internal circuits to specific concepts. |
| **Jailbreak** | A prompt crafted to trick a model into ignoring its safety training. |
| **Prompt injection** | Hidden instructions planted in content a model reads, such as a web page or email, that try to hijack its behaviour. A major risk for agents. |
| **Red teaming** | Deliberately attacking a model to find weaknesses and harmful behaviours before release. |
| **Reward hacking** | When a model finds a shortcut that scores well on its training reward without doing the intended task, such as editing a test so it passes. |
| **Scheming / deceptive alignment** | The risk that a model appears aligned during testing while pursuing different goals. An active research area. |
| **Misuse / dual-use** | Harm from people deliberately using AI for bad ends. Dual-use means a capability helps both good and harmful purposes, such as biology knowledge. |
| **Responsible Scaling Policy (RSP)** | Anthropic's framework that ties stronger safeguards to more capable models. Other labs publish similar frontier safety frameworks. |
| **Deepfake** | Realistic synthetic media that imitates a real person's face or voice. |
| **Watermarking / provenance** | Marking AI-generated content, or recording its origin (for example C2PA credentials), so it can be identified later. |
| **Copyright and training data** | The ongoing legal debate over whether training on copyrighted works without permission is lawful. Several major court cases are under way. |
| **Data privacy** | Protecting personal data used in training or shared with AI tools. In the UK and EU this falls under GDPR. |
| **EU AI Act** | The EU's risk-based AI law, with obligations phasing in between 2025 and 2027. It sets rules for high-risk systems and general-purpose models. |
| **AI Security Institute (UK)** | The UK government body, formerly the AI Safety Institute, that tests frontier models for national-security risks. |
| **Model welfare** | An emerging research question about whether AI systems might have experiences that matter morally, and how to act under that uncertainty. |

## Industry & Culture

These are the big-picture ideas, business terms and slang that appear constantly in AI news and discussion.

| Term | What it means |
| --- | --- |
| **Narrow AI** | AI built for specific tasks, such as recommendation engines or chess programs. All AI deployed today is narrow to some degree. |
| **AGI** | Artificial General Intelligence. AI that can match humans across most intellectual tasks. There is no agreed definition or test. |
| **ASI** | Artificial Superintelligence. Hypothetical AI that far exceeds human ability in virtually every domain. |
| **AI lab** | An organisation building frontier models, such as Anthropic, OpenAI, Google DeepMind, Meta, xAI, Mistral, DeepSeek and Alibaba's Qwen team. |
| **Emergent abilities** | Skills that appear in larger models without being explicitly trained, such as translation or arithmetic. Whether they are truly sudden is debated. |
| **The Bitter Lesson** | Rich Sutton's 2019 essay arguing that general methods using more compute beat hand-built human knowledge in the long run. |
| **Scaling hypothesis** | The belief that continuing to scale data, compute and model size will keep producing more capable AI. |
| **Stochastic parrot** | A critical phrase describing LLMs as predicting plausible text without real understanding. |
| **Price per million tokens** | The standard way API usage is billed, with separate rates for input and output tokens. |
| **Wrapper** | A product that adds a thin interface on top of someone else's model. Often used dismissively. |
| **Moat** | A durable competitive advantage, such as proprietary data, distribution or compute, that rivals cannot easily copy. |
| **GPU-rich / GPU-poor** | Slang for organisations with abundant compute versus those that must work within tight limits. |
| **Sovereign AI** | A nation building its own AI models and infrastructure to reduce reliance on foreign providers. |
| **Vibe coding** | Building software by describing what you want to an AI and accepting its code, with little manual review. |
| **AI slop** | Low-quality, mass-produced AI-generated content that clutters the web and social media. |
| **AI winter** | A historical period when funding and interest in AI collapsed after hype outran results. The main ones were in the 1970s and late 1980s. |
| **Hype cycle** | The pattern of inflated expectations, disillusionment and eventual practical adoption that new technologies often follow. |
| **Doomer / accelerationist** | Opposite camps: doomers stress catastrophic AI risk; accelerationists (e/acc) argue for building AI as fast as possible. |
