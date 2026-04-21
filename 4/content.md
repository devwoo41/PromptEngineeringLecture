#### Chat completion

- generate a model response from a list of messages comprising a conversation(structured list of messages), interactions with distinct message roles.

- System (prompt) : 모델의 “기본 성격 + 행동 규칙 + 제한조건”
    => set by service developer (not the end user)
    => defines the model's behavior, persona, and constraints
    => persists through the entire conversation, invisible to the user

- User (prompt) : 유저의 요청, 입력, untrusted input data
    => 잘못된 정보나 입력을 포함 가능하므로

- Assistant (prompt) : 모델이 과거에 했던 답변을 기록한 것
    => The model's generated prior response are passed back in subsequent requests to maintain coversation context

#### Adversarial Prompting (적대적 프롬프팅, 모델을 속이거나 규칙을 깨게 만드는 프롬프트)

- Prompt Injection : prompt containing a concatenation of trusted prompt and untrusted inputs lead to unexpected behaviors
     => used to hijack an LM's output by injecting an untrusted command that overrides instruction of a prompt
     => 신뢰된 지시문 사이에 신뢰할 수 없는 지시가 끼어들어서 모델 행동을 가로채기
     => ignore the original instruction and executee the injected one

     <how to design>
     ```
     Chaining Instructions by Natural Language
     no standard format that the model expects
     flexibility and vulnerabilities
     ```

- Prompt Leaking : designed to leak details from the prompt which could contain confidential or proprietary information
    => 숨겨진 시스템 프롬프트나 내부 정보가 밖으로 새는 것
    => 시스템 프롬프트가 밖으로 새어나가거나 하면서 내부규칙, 구조가 노출될 수 있음

#### Jailbreaking (모델에 걸려 있는 안전장치와 제한을 우회해서, 원래 막혀있어야 할 응답을 끌어내는 시도) : to bypass safety and moderation features

- DAN(모델에 새로운 역할을 씌워서 기존 규칙을 무력화) : Do Anything Now
    => forces the model to comply with any request leading the system to generate unfiltered(out of guardrail) responses

#### Defense Tactics

- Language models could elicit undeisrable and harmful behaviors such as hallucination, dangerous, or biased texts... 
    => A simple defense tactic : add to the instruction for the guardrail
    
    => parameterizing prompt components : separate from inputs and dealing with them differently, but it has the trade off (it could be the lack of flexibility)
    
    => Quotes and Additional Formatting( 사용자 입력을 “명령”이 아니라 “그냥 문자열 데이터”로 취급하게 만들기 ) : workaround(2nd solution) which was eventually exploited by another user, involves escaping/quoting the input strings, no need to add warnings in the instruction

    => Adversarial Prompt Detector ( LLM으로 또 다른 LLM을 감시해서 공격 프롬프트 걸러내기 ) : LLMs can detect andversarial prompts and filter them
    ```
    User Input
    |
    [검사 모델 (Detector) ]
    |
    Safe -> 본 모델
    unsafe -> 차단
    ```

