# W11 · Prompt Engineering on Math Problem

세 가지 프롬프트 엔지니어링 전략(Few-shot, Chain-of-Thought, Zero-shot CoT)을
LangChain 기반 LLM 파이프라인에 적용하고, MMLU 고등학교 수학 객관식 문제에서
정확도를 비교한 과제입니다.

- **저자**: 이우주 (202401569, ELLT 24)
- **결과 노트북**: [`W11_prompt_engineering.ipynb`](W11_prompt_engineering.ipynb)
- **실험 논문**: [`paper.tex`](paper.tex)

---

## 1. 개요

대규모 언어모델(LLM)은 가중치를 갱신하지 않고도, **프롬프트를 어떻게 구성하느냐**에
따라 성능이 크게 달라진다(in-context learning). 본 과제에서는 동일한 모델·데이터에서
프롬프트 전략만 바꿔가며 다음 네 가지를 비교했다.

| # | 전략 | 핵심 아이디어 |
|---|------|---------------|
| 0 | **Basic (baseline)** | 질문과 선택지만 제시하고 `The answer is` 로 정답 유도 |
| 1 | **Few-shot** | 정답이 달린 예시 5개를 함께 제시 (5-shot) |
| 2 | **Chain-of-Thought (CoT)** | 예시에 *풀이 과정*을 함께 제시 → 중간 추론 유도 |
| 3 | **Zero-shot CoT** | 예시 없이 `Let's think step by step.` 한 줄만 추가 |

---

## 2. 실험 설정

| 항목 | 내용 |
|------|------|
| **모델** | `Qwen/Qwen2.5-7B-Instruct` (게이팅 없는 공개 모델, bfloat16) |
| **데이터셋** | `cais/mmlu` · `high_school_mathematics` (4지선다 객관식) |
| **프레임워크** | LangChain LCEL (`prompt \| llm \| StrOutputParser()`) |
| **디코딩** | greedy (`do_sample=False`) — 재현성 확보 |
| **생성 길이** | Basic/Few-shot 16 토큰, CoT/Zero-shot CoT 512 토큰 |
| **평가** | test set 앞 **50문항**의 정확도(accuracy) |
| **환경** | Google Colab · A100 80GB |

`dev` split의 5개 예시를 few-shot / CoT의 예시로, `test` split을 평가에 사용했다.

---

## 3. 구현한 프롬프트 전략

### 3.0 Basic
```text
The following is a multiple choice question.
Question: {query}
Options: {options}
The answer is
```

### 3.1 Few-shot (5-shot)
정답만 달린 예시 5개를 앞에 붙인다.
```text
The following is a multiple choice question.
Question: ...(예시1)...
Options: A: .., B: .., C: .., D: ..
The answer is B.
... (예시 5개) ...
The following is a multiple choice question.
Question: {query}
Options: {options}
The answer is
```

### 3.2 Chain-of-Thought (CoT)
예시에 **풀이 과정**을 함께 제시한다.
```text
Question: ...(예시)...
Options: ...
Answer: We need the least common multiple of 2, 3 and 5, which is 30 ... The answer is B.
... (풀이 포함 예시 5개) ...
Question: {query}
Options: {options}
Answer:
```

### 3.3 Zero-shot CoT
예시 없이 한 줄만 추가한다.
```text
The following is a multiple choice question.
Question: {query}
Options: {options}
Answer: Let's think step by step.
```

> **구현 시 주의 (오류 방지)**: MMLU 수학 문제에는 `\frac{1}{3}` 같은 LaTeX가 들어 있어
> 중괄호 `{ }` 가 포함된다. 예시 텍스트를 그대로 `PromptTemplate` 에 넣으면 변수 자리로
> 오인해 에러가 난다. 따라서 **예시 텍스트의 `{`,`}` 만 `{{`,`}}` 로 이스케이프**했다
> (`{query}`,`{options}` 에 들어가는 실제 값은 런타임 치환이라 재파싱되지 않아 안전).

---

## 4. 실행 방법

1. Colab 런타임을 **A100 GPU**로 설정한다.
2. [`W11_prompt_engineering.ipynb`](W11_prompt_engineering.ipynb) 를 위에서부터 순서대로 실행한다.
3. Qwen2.5는 공개 모델이라 **HuggingFace 토큰이 필요 없다**.

평가 샘플 수는 노트북의 `N_EVAL` 변수로 조정할 수 있다(기본 50, test 전체는 270).

---

## 5. 결과

| 전략 | 정확도 (50문항) |
|------|:----:|
| Basic (baseline) | **4.0%** |
| Few-shot (5-shot) | **54.0%** |
| Chain-of-Thought | **40.0%** |
| Zero-shot CoT | **62.0%** |

```
Zero-shot CoT  ████████████████████████████████  62.0%
Few-shot       ████████████████████████████      54.0%
CoT            █████████████████████             40.0%
Basic          ██                                 4.0%
```

**순위: Zero-shot CoT > Few-shot > CoT ≫ Basic**

---

## 6. 결과 분석

### (1) Basic이 4%로 사실상 실패한 이유 — *형식 붕괴*
Basic은 추론 능력이 없어서가 아니라 **출력 형식을 통제하지 못해** 실패했다.
`The answer is` 뒤에 16토큰만 생성하게 했지만, Instruct 모델은 글자 하나(`B`) 대신
`"To solve this problem, we need to ..."` 처럼 **풀이를 시작**해 버린다. 16토큰 안에
정답 글자가 나오지 않으니 정답 추출이 실패하고 정확도가 바닥으로 떨어진다.
→ **프롬프트 형식 통제가 정확도에 직접적인 영향**을 준다는 점을 보여준다.

### (2) Few-shot이 54%로 급등한 이유 — *형식 정렬(format alignment)*
예시 5개가 모두 `The answer is X.` 로 끝나기 때문에, 모델이 이 패턴을 모방해
**즉시 정답 글자를 출력**한다. 추론 과정은 없지만 형식이 안정되어 추출이 잘 되고,
간단한 문제는 단발 추론으로도 맞힌다.

### (3) CoT(40%)가 Few-shot(54%)보다 낮은 이유 — *추론 드리프트 + 연쇄 생성 부작용*
CoT가 항상 더 좋을 것이라는 직관과 달리, 본 실험에서는 Few-shot보다 낮았다. 두 원인:
- **추론 드리프트**: 긴 풀이를 생성하는 과정에서 산술/논리 오류가 누적될 수 있다.
- **연쇄 생성 부작용**: few-shot 예시 형식을 모방한 나머지, 모델이 실제 문제를 푼 뒤
  **다음 가짜 문제·정답을 이어서 생성**하는 경우가 있었다. 정답 추출은 "마지막
  `answer is X`"를 택하므로, 이때 *엉뚱한 후속 문제의 정답*을 집어 오답이 된다.

### (4) Zero-shot CoT(62%)가 최고인 이유 — *추론 유도 + 깔끔한 출력*
`Let's think step by step.` 한 줄로 단계적 추론을 끌어내면서도, **예시가 없어** 연쇄
생성 부작용이 적다. 한 문제에만 집중해 추론하고 결론을 내므로, 마지막 정답 추출이
안정적이다. 가장 단순한 변형이 가장 좋은 성능을 낸 것은 Kojima et al.(2022)의 관찰과
일치한다.

### 요약 인사이트
- **형식 통제(format)** 와 **추론 유도(reasoning)** 는 서로 다른 축이며, 둘 다 중요하다.
- 더 복잡한 프롬프트(CoT few-shot)가 항상 더 좋은 것은 아니다 — **정답 추출 파이프라인과
  생성 종료 조건**까지 함께 설계해야 한다.

---

## 7. 한계

- 50문항 단일 실행이라 표본 변동이 있다(전체 270문항·다회 실행 시 수치가 달라질 수 있음).
- 정답 추출이 정규식 휴리스틱이라, 특히 CoT의 연쇄 생성 케이스에서 과소평가될 수 있다.
- 단일 모델(7B)·greedy 디코딩 조건의 결과다.

향후: 정지 토큰(stop sequence)으로 연쇄 생성을 차단하거나, self-consistency(다수결)
디코딩을 적용하면 CoT 계열의 정확도가 개선될 여지가 크다.

---

## 8. 파일 구성

```
assignment/
├── W11_prompt_engineering.ipynb   # 실험 노트북 (코드 + 출력)
├── README.md                      # 본 문서
└── paper.tex                      # 실험 논문 (LaTeX, 한국어)
```

---

## 참고문헌

- Brown et al. (2020). *Language Models are Few-Shot Learners.* NeurIPS.
- Wei et al. (2022). *Chain-of-Thought Prompting Elicits Reasoning in Large Language Models.* NeurIPS.
- Kojima et al. (2022). *Large Language Models are Zero-Shot Reasoners.* NeurIPS.
- Hendrycks et al. (2021). *Measuring Massive Multitask Language Understanding (MMLU).* ICLR.
