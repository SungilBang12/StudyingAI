
AI가 작동하는 원리를 이해하고, 모델·데이터·검색·메모리·도구·환경·평가 시스템을 하나의 재료로 다루기 위한 연습을 위한 repo입니다.

어떤 기술을 그대로 복제하는 것에서 끝나는 것이 아니라,

이해 -> 조정 -> 실험과 측정 -> 에러 만들기 -> 다시 설계

를 통해 원하는 성질을 만드는 연습용입니다

---

# 목표

이 프로젝트가 끝났을 때, AI 시스템의 성질을 이해하고 그것을 의도적으로 조형할 수 있는 역량이 있으면 합니다. 현재는,

- AI 시스템을 직접 구현할 수 있다.
- 왜 이런 구조로 동작하는지 설명할 수 있다.
- 시스템에서 조정 가능한 변수(knob)를 찾아낼 수 있다.
- 특정 변수를 바꾸면 어떤 결과가 나타날지 가설을 세울 수 있다.
- 성능을 느낌이 아니라 metric으로 비교할 수 있다.
- 시스템이 실패하는 조건과 경계를 설명할 수 있다.
- 목적에 따라 architecture를 수정할 수 있다.
- 기존 시스템을 그대로 복제하지 않고 나만의 형태로 재설계할 수 있다.

상기한 정도의 행동 목표입니다

---

# 핵심 루프

모든 주차는 대략적으로 다음과 같이 진행할 예정입니다.

```
Search
  ↓
Build
  ↓
Measure
  ↓
Tune
  ↓
Break
  ↓
Rebuild
```

## 0. Search

- 이 서비스가 제시하는 pain point와 그 해결책의 조사
- 특별한 기능, 최적화 정도, 기대한 방법과 다른 사용 방법
- AI를 사용하는 방식
	- context
	- 담당하는 역할
	- 행동 권한
	- 없다면 어떻게 되는지?
- AI input&output 데이터
- 화면 
- 사람들을 이해한 관점, 방식
- 사용한 알고리즘과 자료구조
- 아키텍쳐
- 사용한 스택(알 수 있고 사용할 수 있는 것, 혹은 대채제)
- 서비스의 작동 흐름의 분해
- Input / Representation / Model / Tool / Evaluation / Output

등등
(추가로 주요하다고 생각되는 관점이 있다면 추가할 예정)
## 1. Build

AI를 활용한 구축. 서비스를 할 생각은 없으니 local 구동만을 목표로
Baseline의 설계를 목표로

## 2. Measure

성능이나 주요 지표들의 측정.

예:

- Accuracy
- Recall / Precision
- Retrieval quality
- Latency
- Token usage
- Cost
- Hallucination
- Reliability
- Personalization
- Complexity

측정 툴들은 업데이트 예정

## 3. Tune

```
Baseline
↓
Variable A 변경
↓
Experiment A
↓
Variable B 변경
↓
Experiment B
```


## 4. Break

좋은 설정이 아닌 망가지는 설정들을 써보며 실험해보기

```
너무 작은 chunk
너무 큰 top-k
지나치게 긴 context
높은 temperature
과도한 agent retry
잘못된 memory retrieval
```

- 실패가 시작되는 경계
- 조합
- 예측과 결과의 괴리 비교
## 5. Rebuild

내가 이 시스템의 설계자라면 무엇을 다르게 만들 것인지 질문하고 구현해보기

---

# 20주 과정(20주로는 절대 안 끝날거 같지만...)

| Week   | 주제                     | 집중해서 볼 것                                 |
| ------ | ---------------------- | ---------------------------------------- |
| **01** | NotebookLM             | RAG를 검색이 아니라 사고 공간으로 만드는 방법              |
| **02** | Perplexity             | Search + LLM + Citation 구조               |
| **03** | GraphRAG               | Entity, Relationship, Traversal, Ranking |
| **04** | AI Memory              | 무엇을 기억하고 무엇을 잊을 것인가                      |
| **05** | Deep Research          | 답변이 아니라 탐구 과정을 설계하는 방법                   |
| **06** | Claude Code & Codex    | Agent가 일하기 좋은 환경과 Harness                |
| **07** | Cursor Agent           | Agent의 행동과 결과를 어떻게 검증할 것인가               |
| **08** | LangGraph & Agents SDK | Agent state와 control flow                |
| **09** | Co-Scientist           | 생성·비판·경쟁으로 사고를 만드는 구조                    |
| **10** | AlphaEvolve            | Generation → Evaluation → Evolution      |
| **11** | AlphaGo                | Search, Policy, Value, Reward            |
| **12** | AlphaFold              | AI를 새로운 과학 도구로 사용하는 방법                   |
| **13** | Palantir Ontology      | 현실 세계를 Object / Relation / Action으로 표현   |
| **14** | Knowledge Graph + LLM  | 언어 모델과 구조화된 세계 모델의 결합                    |
| **15** | Recommender Systems    | 사람의 선호를 어떻게 표현하고 탐색하는가                   |
| **16** | Generative Agents      | Memory + Reflection + Planning           |
| **17** | Voyager                | Agent가 환경 속에서 스스로 기술을 축적하는 방법            |
| **18** | Genie & World Models   | State + Action → Next State              |
| **19** | VLM & Computer Use     | AI가 보고 판단하고 행동하는 구조                      |
| **20** | My AI System           | 앞선 기술들을 결합해 나만의 시스템 설계                   |

---

# 대표적으로 찾아야 할 Knobs

|분야|Knobs|관찰할 것|
|---|---|---|
|**RAG**|chunk size, overlap, top-k, embedding, reranker|Recall ↔ Noise|
|**GraphRAG**|entity, relation, traversal depth, edge weight|연결성 ↔ 복잡도|
|**Agent**|planning depth, retry, tool selection, permissions|자율성 ↔ 안정성|
|**Memory**|save condition, importance, decay, retrieval|기억 ↔ 오염|
|**Prompt**|instruction, ordering, examples, context size|제어력 ↔ 유연성|
|**LLM Inference**|temperature, top-p, model routing|다양성 ↔ 안정성|
|**Fine-tuning**|dataset, LR, epoch, LoRA rank|적응 ↔ overfitting|
|**Multi-Agent**|role, topology, critic, voting|다양성 ↔ coordination cost|
|**Evaluator**|metric, judge, reward|측정 가능성 ↔ 실제 품질|
|**Recommender**|preference weight, recency, exploration|익숙함 ↔ 발견|
|**World Model**|state, action, reward, horizon|추상화 ↔ 현실성|
|**Inference Optimization**|quantization, batching, cache|품질 ↔ 속도 / 비용|

---
# 최소 실험 기록 템플릿

매 실험마다 최소한 아래 내용은 기록한다.

```
# Experiment

## Baseline

현재 시스템은 어떻게 동작하는가?

## Hypothesis

무엇을 바꾸면 어떤 결과가 나타날 것이라고 예상하는가?

## Variable

이번 실험에서 변경하는 단 하나의 변수는 무엇인가?

## Metric

무엇으로 결과를 판단할 것인가?

## Result

실제 결과는 어떠했는가?

## Why?

왜 이런 결과가 나타났다고 생각하는가?

## My Design

내가 실제 시스템을 만든다면 어떤 설정과 구조를 선택할 것인가?

## Reflection

이번 실험을 통해 새롭게 이해한 것은 무엇인가?
```

---

# 좋은 실험을 했는지 확인하는 질문

주차가 끝날 때 스스로 물어본다.

- 이 기술의 핵심 아이디어를 코드 없이 설명할 수 있는가?
    
- Architecture를 기억에 의존해 그릴 수 있는가?
    
- 최소 3개의 knob를 알고 있는가?
    
- 각 knob가 무엇을 변화시키는지 설명할 수 있는가?
    
- 실제로 하나 이상의 knob를 변경해봤는가?
    
- 변경 전후를 측정했는가?
    
- 시스템이 실패하는 경우를 직접 만들었는가?
    
- 실패 이유를 설명할 수 있는가?
    
- 원본과 다른 나만의 설계 선택을 하나 이상 했는가?
    
- 그 선택에 이유가 있는가?
    

---
