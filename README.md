# HF-API-tutorial
How to use Hugging Face Inference API calls from your python


follow the full tutorial from my medium Article.

[ADD THE LINK HERE](#)

### Requirements
```
pip install --no-cache-dir transformers huggingface_hub[inference] pillow tiktoken streamlit
```

### Usage
Replace **`hf_xxxx`** with your created Hugging Face Access TOken

meta-llama/Meta-Llama-3-8B-Instruct
```python
from huggingface_hub import InferenceClient
hftoken = 'hf_xxxx'
client = InferenceClient(token=hftoken)

messages = [{"role": "user", "content": "Explain what is Science in 3 paragraphs."}]
client = InferenceClient("meta-llama/Meta-Llama-3-8B-Instruct",token=hftoken)
output = client.chat_completion(messages, max_tokens=500)
print(output.choices[0].message.content)
```

---

Using https://huggingface.co/mistralai/Mixtral-8x7B-Instruct-v0.1 with `steraming effect`
```python
from huggingface_hub import InferenceClient
hftoken = 'hf_xxxx'
client = InferenceClient(token=hftoken)
messages = [{"role": "user", "content": "Explain what is Science in 3 paragraphs."}]
stream = client.chat.completions.create(
    model="mistralai/Mixtral-8x7B-Instruct-v0.1", 
	messages=messages, 
	max_tokens=500,
	stream=True)
for chunk in stream:
    print(chunk.choices[0].delta.content, end="")
print('')
```

---

Using https://huggingface.co/Qwen/QwQ-32B-Preview with `steraming effect`
```python
from huggingface_hub import InferenceClient
hftoken = 'hf_xxxx'
client = InferenceClient(token=hftoken)
prompt = input(user: )
messages = [{"role": "user", "content": prompt}]
stream = client.chat.completions.create(
    model="Qwen/QwQ-32B-Preview", 
	messages=messages, 
	max_tokens=500,
	stream=True)
for chunk in stream:
    print(chunk.choices[0].delta.content, end="")
print('')
```

---

Using https://huggingface.co/mistralai/Mixtral-8x22B-Instruct-v0.1 with `steraming effect`
```python
from huggingface_hub import InferenceClient
hftoken = 'hf_xxxx'
client = InferenceClient(token=hftoken)
prompt = input(user: )
messages = [{"role": "user", "content": prompt}]
stream = client.chat.completions.create(
    model="mistralai/Mixtral-8x22B-Instruct-v0.1", 
	messages=messages, 
	max_tokens=500,
	stream=True)
for chunk in stream:
    print(chunk.choices[0].delta.content, end="")
print('')
```



