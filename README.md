# ChatGPT-Application
# Ứng dụng ChatGPT với OpenAI và LangChain

## Tổng quan
Notebook này trình bày cách sử dụng ChatGPT thông qua thư viện OpenAI và LangChain cho nhiều tác vụ xử lý ngôn ngữ tự nhiên khác nhau.

## 1. Cài đặt cơ bản

### Yêu cầu hệ thống
```python
%pip install --upgrade --quiet openai
```

### Thiết lập API
```python
import openai
import IPython

OPENAI_API_KEY = ""  # Thêm API key của bạn vào đây
openai.api_key = OPENAI_API_KEY
```

### Hàm hỗ trợ
```python
def set_open_params(
    model="text-davinci-003",
    temperature=0.7,
    max_tokens=256,
    top_p=1,
    frequency_penalty=0,
    presence_penalty=0,
):
    """Thiết lập tham số cho OpenAI API"""
    return {
        'model': model,
        'temperature': temperature,
        'max_tokens': max_tokens,
        'top_p': top_p,
        'frequency_penalty': frequency_penalty,
        'presence_penalty': presence_penalty
    }

def get_completion(params, prompt):
    """Gửi yêu cầu đến OpenAI API"""
    response = openai.Completion.create(
        engine=params['model'],
        prompt=prompt,
        temperature=params['temperature'],
        max_tokens=params['max_tokens'],
        top_p=params['top_p'],
        frequency_penalty=params['frequency_penalty'],
        presence_penalty=params['presence_penalty'],
    )
    return response
```

---

## 2. Sử dụng LangChain

### Cài đặt
```python
%pip install --upgrade --quiet openai langchain
```

### Khởi tạo
```python
from langchain.chat_models import ChatOpenAI
from langchain import PromptTemplate, LLMChain
from langchain.prompts.chat import (
    ChatPromptTemplate,
    SystemMessagePromptTemplate,
    AIMessagePromptTemplate,
    HumanMessagePromptTemplate,
)
from langchain.schema import AIMessage, HumanMessage, SystemMessage

chat = ChatOpenAI(temperature=0)
```

### Ví dụ sử dụng
```python
# Phân loại cảm xúc
USER_INPUT = "I love programming."
FINAL_PROMPT = """Classify the text into neutral, negative or positive. 
Text: {user_input}. 
Sentiment:"""

chat([HumanMessage(content=FINAL_PROMPT.format(user_input=USER_INPUT))])
```

---

## 3. Các ứng dụng thực tế

### 1. Phân loại văn bản
```python
prompt = """Classify the following text into neutral, negative, positive.
Text: I think the food was okay.
This text is:"""
```

### 2. Dịch máy
```python
prompt = """Translate these sentence from vi to en language.
Text: Tôi đang học trí tuệ nhân tạo tại AI VIET NAM."""
```

### 3. Hỏi đáp
```python
prompt = """Answer the following question:
Question: Where was President Ho Chi Minh born?
Context: Hồ Chí Minh was born in Nghệ An province in the French protectorate of Annam."""
```

### 4. Hội thoại (đóng vai)
```python
prompt = """This is a conversation between a customer and a polite customer service agent.
Customer: Hi, I'd like a refund for the coffee maker I ordered. Would that be possible?
AI:"""
```

### 5. Lập luận
```python
prompt = """The odd numbers in this group add up to an even number: 15, 32, 5, 13, 82, 7, 1.
Solve by breaking the problem into steps."""
```

### 6. Ứng dụng lập trình
```python
prompt = """Write a function that calculates the average of the numbers in a Python List.
Add comments to the code"""
```

---

## 4. Hạn chế của ChatGPT

### Ví dụ về hạn chế
```python
prompt = """Question: When did the world population reach 8 billion people?"""
# ChatGPT có thể đưa ra thông tin không chính xác về các sự kiện gần đây

prompt = """Question: How many country names start with the letter V?"""
# Đôi khi kết quả có thể không đầy đủ hoặc chính xác
```

## Lưu ý quan trọng
1. Luôn kiểm tra kết quả từ ChatGPT, đặc biệt với các thông tin quan trọng
2. API key cần được bảo mật và không chia sẻ công khai
3. Có thể điều chỉnh tham số temperature để kiểm soát độ sáng tạo của kết quả
4. Với các tác vụ phức tạp, nên chia nhỏ prompt thành các bước

## Yêu cầu hệ thống
- Python 3.6+
- Thư viện: openai, langchain
- API key từ OpenAI
