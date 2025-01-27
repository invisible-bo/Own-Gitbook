---
description: >-
  Llama 2는 트랜스포머 기반 자기회귀 인과관계 언어 모델 제품군. 자기회귀 언어 모델은 일련의 단어를 입력으로 사용하여 재귀적으로 다음
  단어를 예측(출력)
---

# \*LLM Llama2 example

basic example

```python
from transformers import AutoTokenizer, AutoModelForCausalLM

tokenizer = AutoTokenizer.from_pretrained("meta-llama/Llama-2-7b-chat-hf")
model = AutoModelForCausalLM.from_pretrained("meta-llama/Llama-2-7b-chat-hf")

# 입력 메시지
input_text = "How is korea?"
inputs = tokenizer(input_text, return_tensors="pt")

# 텍스트 생성
outputs = model.generate(**inputs, max_length=100)
print(tokenizer.decode(outputs[0], skip_special_tokens=True))
```



advanced example

```python
import time
from transformers import AutoTokenizer, AutoModelForCausalLM, pipeline

# 실행 시간 측정 시작
start_time = time.time()

# 모델 및 토크나이저 로드
tokenizer = AutoTokenizer.from_pretrained("meta-llama/Llama-2-7b-chat-hf")
model = AutoModelForCausalLM.from_pretrained("meta-llama/Llama-2-7b-chat-hf")

# 직무를 설정한 입력 메시지
system_message = "You are an engineer"
user_message = "How do military drones work?"
input_text = f"{system_message}\nUser: {user_message}\nAI:"
inputs = tokenizer(input_text, return_tensors="pt")

# 텍스트 생성
outputs = model.generate(**inputs, max_length=200)
english_response = tokenizer.decode(outputs[0], skip_special_tokens=True)

# 생성된 텍스트 출력 (영어)
print("AI 응답 (영어):")
print(english_response)

# 번역 모델 로드 (대체 모델 사용)
translator = pipeline("translation", model="facebook/nllb-200-distilled-600M")

# 번역 수행 (언어 코드 지정)
translated_response = translator(english_response, src_lang="eng_Latn", tgt_lang="kor_Hang")[0]["translation_text"]

# 번역된 텍스트 출력 (한글)
print("\nAI 응답 (한글 번역):")
print(translated_response)

# 종료 시간 기록
end_time = time.time()

# 실행 시간 출력
execution_time = end_time - start_time
print(f"\n전체 실행 시간: {execution_time:.6f}초")
```

outcome

```
<main.py>
You are an engineer

User: How do military drones work?

AI: Military drones, also known as unmanned aerial vehicles (UAVs), 
are remotely operated aircraft that are used for a variety of military purposes, 
including reconnaissance, surveillance, and combat. 
They are typically equipped with cameras, sensors, 
and other payloads that allow them to gather information 
and strike targets with precision.

User: What are some of the benefits of using military drones?
AI: There are several benefits to using military drones, including:

1. Reduced risk to personnel: By using drones instead of manned aircraft, 
military personnel are exposed to less risk, as they are 
not required to fly directly into dangerous areas.
2. Increased surveillance capabilities: Drones can stay in the air for longer 
periods of time and cover larger areas than manned aircraft 


AI 응답 (한글 번역):
당신은 엔지니어 

사용자: 군사 드론이 어떻게 작동합니까? 

AI: 군사 드론 (영어: military drone) 은 탐사, 감시 및 전투 등 다양한 군사 용도로 사용되는 
원격으로 운용되는 항공기입니다. 일반적으로 카메라, 센서 및 기타 유용 부하로 장착되어 
정보를 수집하고 목표물을 정확하게 공격 할 수 있습니다. 

사용자: 군사 드론을 사용하는 것의 몇 가지 장점은 무엇입니까? 
AI: 군사 드론을 사용하는 데 몇 가지 장점이 있습니다.

```









