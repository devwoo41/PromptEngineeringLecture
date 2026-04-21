#### Promptification

- Relying heavily on the quality of the prompts provided to the AI system

- The quality of results depend on;
    => How much Information you provide it
    => How well-crafted the prompt is

- A prompt can contain information such as
    => the instruction or question you are passing to the model
    => other details such as context, inputs, or examples

#### Difference between prompting and promptification

- prompting
    => refers to the act of crafting and using a prompt to interact with an AI model
    => scope : single interaction

- promptification
    => the process of converting tasks, workflows, or structured inputs into prompt-based interactions with AI
    => scope : process-oriented

#### Linguistic knowledge

- knowledge of the underlying grammatical rules and structures of language ensure that prompts are formulated.

- understanding the *nuances* of language and how it is *used in different contexts* is essential for PE.

#### Types of Prompts

- Text-based Prompts : Command-line prompts, In-app text prompts
    => Command-line prompts : 모델을 "조작"하는 프롬프트
    => In-app prompts : 사용자를 "유도"하는 프롬프트

- Graphical Prompts : Dialog boxes, Tooltips

- Voice-based Prompts : Overview of voice user interfaces, voiced prompts in software engineering

- Code-based Prompts : Code snippets, Code templates

#### Key components in PE

- Instruction

- Context

- Input data

- Output Indicator

#### How to write Better Prompts
```
Give Context
Ask for a precise response
Provide an example
Keep it concise(간결)
Follow up
Avoid yes/no questions
Use chain-of-thought prompting
Use the Self-Ask Technique(모델이 질문을 자가생성)
```

#### PETechniques

- Zero-shot prompting : algorithms to make predictions about new classes by using prior knowledge

- Few-shot prompting : enable in-context learning

- CoT(Chain of Thought) Prompting : instructing the model to reason about the task when responding
    => *Demonstrations* are utilized. Demonstrations refer to explicit examples provided within the prompt to guide the AI model in reasoning through a problem step by step, show the *step-by-step reasoning pattern* from the previous examples.

- Zero-shot CoT Prompting : Involves *Let's think step by step* to the original prompt.

- AutoCoT : diversity of demonstrations
    => *Question Clustering* : partition questions of a given dataset into a few clusters
    => *Demonstration sampling* : encourages the model to use simple and accurate demonstrations.

- Multimodal CoT : *two-stage framework* incorporating text and vision
    => rationale generation
    => answer inference

- In Context Learning : Demonstrations of the task are provided to the model as part of the prompt in natural Language
    => Induction heads : predict repeated sequences
    ```
    prefix matching : 과거에서 비슷한 패턴 찾음
    copying : 그 다음 토큰 복사
    ```

#### Hallucinations

- Factual Hallucination(사실 오류) : 없는 사실을 만들어냄
    => 모델은 사실 검증을 안한다
 
- Logical Hallucination(논리 오류) : 논리적으로 말이 안되는 답
    => 모델은 논리엔진이 아니다

- Reference Hallucination(출처 오류) : 없는 논문/출처 만들어냄
    => 출처 스타일만 따라한다

- Contextual Hallucination(맥락 오류) : 질문 맥락과 안 맞는 답
    => 모델이 질문 의도를 잘못 잡음

#### Well inducing Hallucinations

- Person : Issue of generating fictional characters

- Location : The case of generating fictional places is addressed in

- Number : generation of imaginary numbers

- Acronym(약어) : generation of inaccurate responses for acronym

#### Lexical knowledge : the meaning of words and phrases in a text
    
    <3 steps>

- morphological analysis(형태 분석) : breaking down words into their smallest meaningful units, 단어를 조각으로 쪼개기

- syntatic analysis(구문 분석) : determines the pos of words and understands how they interact with each other to clump them together, 단어들의 연결관계를 살핀다.

- semantic analysis(의미 분석) : understanding the meaning of words and how they are in context, 문맥 속 의미를 이해

- Lexical knowledge가 NER(Named Entity Recognition)에 도움을 줘서 Hallucination 감소에 도움을 준다.

#### Semantic / pragmatic knowledge (어떤 말인지 + 의도가 무엇인지)

- modality : Speaker's or writer's attitude towards the world
```
certainty
possibility
willingness
obiligation
necessity
ability
```

- grammatical mood : grammatical feature of verbs / verbal inflection (발화의 어조) / representing the intention
```
interrogative
indicative
imperative
conditional
subjunctive
```

- tense(시제) : form allows express time
```
past
present
future
```

- aspect(행동의 상태) : time-related characteristics(ongoing / repeated / completed)
```
simple(단순)
progressive(진행)
perfective(완료)
perfect progressive(완료 진행)
```

#### Readability (가독성)

- sentence length

- word complexity

- text's complexity

- familiarity

- legibility

- typography

#### Formality (격식, 전문성)

- sophistication(세련됨)

- decorum(품위)

- politeness(공손함)

#### Concreteness (구체성, 얼마나 현실에 부어있는지)

- tangible (실재하는)

- perceptinle (감지되는)

    => more concrete and specific terms help reduce hallucinations