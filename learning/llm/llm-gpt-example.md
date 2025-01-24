# LLM GPT example

```python
import openai
from dotenv import load_dotenv
import os

load_dotenv()
openai.api_key = os.getenv("OPENAI_API_KEY")

# AI 역할 설정
prompt = "넌 영화 전문가야."
messages = [{"role": "system", "content": prompt}]

# 대화 로그 파일 이름 설정
log_file = "conversation_log.txt"

# 텍스트 파일 초기화
with open(log_file, "w", encoding="utf-8") as file:
    file.write("대화 시작\n")
    file.write("="*20 + "\n")


#대화 루프
while True:
    user_input = input("Me: ")
    # 종료 조건
    if user_input.lower() == "exit":
        print("대화를 종료합니다.")
        with open(log_file, "a", encoding="utf-8") as file:
            file.write("대화 종료\n")
            file.write("="*20 + "\n")
        break

    # 사용자 입력을 대화 로그에 추가
    messages.append({"role": "user", "content": user_input})

    response = openai.ChatCompletion.create(
        model="gpt-3.5-turbo",
        messages=messages
)

# 생성된 응답 출력
    ai_response = response['choices'][0]['message']['content']
    print("AI: " + ai_response)

    # 대화 내용을 파일에 기록
    with open(log_file, "a", encoding="utf-8") as file:
        file.write(f"사용자: {user_input}\n")
        file.write(f"AI: {ai_response}\n")
        file.write("-" * 20 + "\n")    
```
