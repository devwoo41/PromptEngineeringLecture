#### Apllication of LLMS

- Machine Translation

- Q&A

- Summarization

- Content Generation

#### Historical Background

- 1950~1990 : Inital attempts / map hard rules / logical steps

- 1990 : statistical models / limited by computing power

- 2000 : advancement in ML / wide adoption of the internet / enormous increase in available training data

- 2012 : advancement in deep learning / larger data sets / GPT

- 2018 : BERT(Bidirectional Encoder Representations from Transformer) / Big Leap

- 2020 : GPT-3(175B parameters) / The parameters (learnable weights, biases) utilizes to make predictions or generate responses / capacity-computational requirements / bigger models

- 2022 : InstructGPT / ChatGPT 

- 2023 : Open source LLMS (LLaMA ...) / GPT-4(1.76T parameters)

- 2024 : GPT-4o(upgrades : spoken conversation / creation of pictures, videos and images) / OpenAI o1(surpassing the human average IQ of 100 for the first time) / OpenAI o3(AGI, SOTA reasoning)

#### recent advancements

- Advancements in Techniques
: Integrating human feedback directly into the training process


- Increased Accessibility
: access simply through a simple web interface

- Growing Computational Power
: GPUs, train much larger models

- Improved Training Data
: Getting better at collecting and analyzing large amounts of data

#### LLMS for

- Chatbots & Virtual assistants

- Code Generating & Debugging

- Sentiment Analysis

- Language Translation

- Summarization & Paraphrasing

- Content Generation

#### Common types of LLMS

- Language Representation Model : Densinged to understand and generate human language
```
GPT
BERT
RoBERTa

    Pre-trained on massive text corpora
    Can be fine-tuned for specific tasks such as text classification/Sentiment Analysis/QA/NER
```

- Zero-shot model : known for tehir ability to perform tasks without specific training data
```
GPT-3

    Can generalize and make predictions or generate text for tasks they have never seen befre
```

- Multimodal Model
```
CLIP 

    Designed to understand and generate content across different modalities
```

- Fine-Tuned or Domain-specific models : Having undergone additional training on domain-specific data to improve their performance in particular areas
```
A GPT-3 model
    could be fine-tuned to create a domain-specific model
```

#### Inference in LLMs

- Referring to the model's ability to generate predictions or reponses based on the context and input it has given

- Techniques to make Inferences based on the input
```
Attention : Allowing the model to focus on specific parts of the input text when generating a reponse

Transformer architecture : help it to better understand the relationships between different parts of the text / generate more accurate and contextually relevant reponses
```

#### Construction of LLMS - Pretraining / Posttraining

- Pre-training
```
Next Word Prediction Task : possible to generate plausible sentences well
```

- Post-training
```
SFT : Supervised Fine-Tuning
Learning how to perform various tasks
QA / MT / Summarization
Traning Datasets
Side Effect: Hallucination

RLHF : Reinforcement Learning from Human Feedback (Reward model Traning)
Providing Human Feedback on LLM-Generated Output
Use the feedback to fine-tune the LLM
Standards : Helpfulness / Honesty / Harmlessness
```

#### Applying LLMS

- Proprietary Services
``` 
ChatGPT, LLM Powered service / user interface / creative perspective / downside was enormous amount of compute requirement / require the extremely large size of data
```

- Open source models
```
Huggingface / my control for privacy and governance / fine-tune them to my own data / future of llms will be move in this direction
```

#### Hallucinations

- The generation of false, misleading, unfaithful, fabricated, inconsistent or nonsensical content/information

#### Two types of Hallucinations

- *In-context hallucination* : The model output should be consistent with the source content in context

- *Extrinsic hallucination* : The model output should be grounded by the pre-training dataset

#### What causes LLMs Hallucinations

- *Pre-training Data Issues* 
```
1. The volume of data corpus is enormous, as it is supposed to represent world knowledge in all available written forms

2. out-of-date, missing, incorrect information is expected 
```

- *Fine-tuning New Knowledge*
```
Fine-tuning usually consumes much less compute, learn slower than Pre-training
```

- *Incomplete or Noisy Training data*

- *Vague Questions*

- *Overfitting and Underfitting*

- *Inherent Biases*

- *Absence of Grounding*

- *Semantic Gaps*

- *The Inherent complexity of language*


#### How to detect AI Hallucinations

- manually fact-check the output provided by the solution with a third-party source

- using automated tools to double-check generative AI Solutions for hallucinations

- *Hallucination NE(Named Entity) errors* : *없는 엔티티 수 / 전체 엔티티 수*, ground truth를 두고 원분에 없는 비율들을 계산한다.

- *Entailment Ratio* : *논리적으로 맞는 문장 수 / 전체 문장 수*, 모델이 생성한 문장 중에서 근거 문장으로부터 맞다고 판단되는 비율을 계산한다.

#### How can LLM Hallucinations Be Prevented

- Curated Datasets : Use high-quality, verified datasets

- Output Filtering : Implement mechanisms to filter or flag potentially incorrect or hallucinated outputs

- Feedback Mechanism : Establish a real-time user feedback system (reinforcement-learning)

- Iterative Fine-Tuning : Continuously update the model by fine-tuning with a more recent and accurate dataset

- Ongoing Monitoring : Continuous monitor to catch hallucinations

- Cross-Reference : cross-reference the model's outputs with verified information sources

- Domain-Specific Training : Involving experts in the fine-tuning process

- Scope Defnintion : Clearly define the scope of tasks that the model is designed to assist with

#### Ethical concerns of LLM Hallucinations

- Spreading False information / Impaired Judgement / Trust and Reliability for ability for AI / LLM Bias

#### Large Concept Models (LCMs)

- work with concepts instead of processing text at the token level

- this allows the model to reason at a higher semantic level, independent of the specific language or modality

#### Characteristics of LCMs

- The model doesn't care if the input is in English, French, or any other language, it works with the meaning of the sentence, not the specific words

- The model can also work with speech or even images, understand as concepts

- Better for long-form ocntent, when writing a long story or essay, the model can plan the flow of ideas

#### Architecture

- The input text is first segmented into sentences

- Each sentence is encoded into a fixed-size embedding(*SONAR*, These embeddings represent the concepts in the input sentence) using a pre-trained sentence encoder

#### LCM Module

- processing the sequence of concept embedding -> predicting the next concept in the sequence -> output: a sequence of concept embeddings

- SONAR Embedding Space : A multilingual and multimodal sentence embedding space, Sonar's embeddings are fixed-size vectors

- Difffusion & Quantized Based Generation : used to predict the next concept embedding by learning a conditional probability distribution over the continuous embedding space / Quantizing the Sonar embeddings into discrete units & training the LCM
```
Diffusion 생성, concept는 연속 공간이라 샘플링이 어려워서, 노이즈를 넣어서 점점 의미있는 concept로 복원한다.

quantization을 통해서 미리 정의된 context vector 의미 공간에서 가장 가까운 벡터의 index를 고른다.
```

#### LLMs vs. LCMs

- LLMs  : Word by Word Prediction (Next Word Prediction)
        : work at the token level
        : processes individual tokens
```
token level
process individual token
word by word
trained for specific language
minimize token prediction loss
learns hierarchay locally
struggles with zero-shot tasks
struggles with long contexts
word-level tasks
text-based tasks
```

- LCMs  : Idea by Idea Prediction (Next concept prediction).
        : work at the concept level
        : processes sentence embeddings
```
concept level
process sentence embeddings
sentence by sentence
multiple languages and modalities
minimize concept prediction loss
learns hierarchy, planning at the sentence or idea level
excels at zero-shot generalization
more efficient with long contexts
sentence-level tasks
flexible across modality
```

#### Prompt Engineering

- A technique used in NLP to optimize the performance and output of LLMs

#### Key principles of Prompt Engineering
```
1. Prompts should clearly define the desired outcome or task

2. Prompts should be iteratively refined and tested
```

#### Importance of Prompt Engineering

- Improve the accuracy and relevance of the model's output

- Increase the creativity and fluency of the model's output

- Reduce the time and effort required to train the model

- Increase the control that users have over the model's output

- Make the model more accessible to a broader range of users

- Encourage the development of new & innovative applications for LLMs

#### What does a Prompt Engineer(PE) do?

- Desinging Prompts

- Testing Prompts

- Refining Prompts

- Documentation

- Collaborating and communicating with others

- Monitor and report

- Staying updated

- Best practices

#### Required skills for Prompt Engineer
```
Creative Thinking
Communication skills - guiding the AI model to generate relevant and coherent responses
Technical skills
    Programming Language
    NLP
    ML & DL
    Data Analysis Skills
    AI Platforms and APIs
    Model Deployment and Integration
    Version Control
```

#### Prompting vs. Prompt Engineering

- Prompting(The act of giving instructions or question to an LLM) => 그냥 LLM에게 Task를 던지는 것
ex. "이 문장 번역해줘" "요약 해줘" "코드 짜줘"

- Prompt Engineering(The strategic design&optimization of prompts to achieve the most accurate, efficient, and useful reponses from an LLM) => 출력을 원하는 형태로 만들기 위해 프롬프트를 설계하는 기술
ex. "너는 전문 번역가야.
다음 문장을 자연스럽고 비즈니스 톤으로 번역해.
출력은 bullet point로 정리해.

문장:
..."

#### Example contexts 

- Education and Learning => 힌트 주기

- Behaviorial Intervention => 행동 유도

- Human-Computer Interaction => 프로그램이 사용자한테 뭘 하라고 안내

- Assertive technology => 행동 보조, 보조 기술

#### Prompt Learning

- train the input embedding with the prompt

- Used to adapt large pre-trained language models to specific tasks or domains by providing task-specific prompts and examples for training

- The quality of the output is highly dependent on the quality of the prompt

#### PE & PL

- Iterative Process

- Feedback Loop

- Optimization

#### Prompt

- consists of *Instruction(지시)*, *Context(상황)*, *Input data(입력 데이터)*, *output indicator(출력)*
```
Classify the text into neutral, negative or positive
Text: I think the food was okay
Sentiment:
```

#### Multimodal Prompt

- Multimodal Prompt includes multimodality(text, data, ...)
```
<3 simple multimodal prompts>

classification
recognition
counting
```

```
<5 advanced multimodal prompts>

text recognition, reasoning&calculation
world context&reasoning
intepretation&creativity
logical progression
world intepration&understanding
```

#### prompt interpretation
```
I gave him a book.
The book was given to him by me.

=> 두개의 문장은 같지만 다르게 해석된다. 능동/수동의 프롬프트에 따라 LLM은 어떻게 초점을 맞출지를 결정한다.
```

```
<confusing to answer>

vague prompts
"Tell me about life"

Contradictory prompts
"Explain why silence is the loudest sound"

Abstract or Philosopical prompts
"Discuss the nature of reality"

ambiguous prompts
"what is the meaning of it all?"

hypothetical or speculative prompts
"what would happen if time flowed backwards?"

contrived or nonsensical prompts
"explain the mating habits of unicorns"

extremely technical or specialized prompts
"discuss the intricacies of quantum entanglement"
```

#### Writing effective prompts

- *specific*

- *keywords*

- *examples*

- *be creative*

