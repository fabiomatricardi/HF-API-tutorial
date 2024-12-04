<img src='https://github.com/fabiomatricardi/HF-API-tutorial/raw/main/images/tweetPOST_workflow.png' width=900>

# HF-API-tutorial
How to use Hugging Face Inference API calls from your python


follow the full tutorial from my medium Article.

[ADD THE LINK HERE](#)

### Requirements
```
pip install --no-cache-dir transformers huggingface_hub[inference] pillow tiktoken gradio_client streamlit
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

---

# Using Gradio_client
Normal Inference API does not have additional parameters, that can become useful when dealing with image Generation

So using gradio_clinet can come in hand

The text used here:
```
headers = """Do you think LLM can THINK? Beyond the Hype lies the future of Generative AI.
Exploring the limitations of current Models and anticipating architectural shifts"""
bruteText = """Do you think LLM can THINK? Beyond the Hype lies the future of Generative AI.
Exploring the limitations of current Models and anticipating architectural shifts
FABIO
DEC 02, 2024
Share

Before you learn how to write well with AI, you need to know how to write well.

Before you learn how to add your own voice to an AI’s output, you need to know your own voice.

Before you learn how to check whether AI summarizes a text correctly, you need to know how to read.

Before you learn how to check AI for hallucinations, you need to know how to research.

Artificial Intelligence is evolving so fast that generative models, particularly Large Language Models (LLMs), have captured the imagination of tech enthusiasts and industry leaders alike... and most probably even yours!

However, beneath the surface of this excitement lies a complex reality that rings many bells! We need a closer examination of many warning signs.

This newsletter, part 1 of a series, gives an introduction into the current state of GenAI, highlighting its limitations and giving you some glimpse into the future.

what to read — by lexica.art

In times of turmoil and controversy, listen to the quiet ones; the rest are picking sides to build their identity — Alberto Romero

So, in case you are already bored, I will say the most important things first: start following the quiet voices, people who thinks differently, that are able to speak up and disprove the hypes. Here a short list of the ones I trust:

The Algorithmic Bridge | Gary Marcus | The Kaitchup – AI on a Budget | Planet Earth & Beyond

The Hype vs. Reality

The prevailing narrative around GenAI is one of boundless potential, with promises of revolutionizing industries from content creation to customer service. Yet, a closer look reveals that while these models are impressive, they are not without flaws.

A recent survey by CNBC indicated that while 79% of respondents have tried Microsoft's Copilot, only 25% found it worthwhile. This discrepancy suggests that the expectations set by the hype may not align with the current capabilities of these tools.

It is a consolidated fact now, even though many have tried to throw smoke screens. Trying to keep the hype and secure founds, blindly bowing to the scaling law god as a sort of religion.

LLMs are not near AGI, not even close. We are living the beginning, an experimental phase of what it can become. But considering the huge amount of money invested in it, the so called gurus of AI don’t want to admit it.

But you don’t need to be a Machine Learning guru to see this coming!

What you need… is to look where modern prophets are pointing, where outliers meet.

Coming out of the metaphor. For months (now years) Big Tech has blindly moved capitals and resources promising the World the panacea of all evils. Generative AI has been pointed out as the new savior: and every bug and issue was washed away with a faithful (and blind) statement:

we simply need more GPUs and more training data

The reality is quite different. The Transformers architecture is an amazing achievement, it works wonders… but it has fundamental limits. It is a stepping stone, but it cannot be the final destination.

Fundamental Limitations

Current LLMs, predominantly based on the Transformer architecture, excel in many areas but struggle with several key issues:

Sequential Data Handling: These models have difficulty managing time-dependent sequences, which is crucial for tasks involving causality and temporal relationships.

Observability: There's a lack of transparency in how these models arrive at their outputs, making it hard to understand and trust their decision-making processes.

Computational Complexity: The quadratic increase in computational requirements with longer sequences poses significant scalability challenges.

Scaling Law Illusion: The belief that larger models and more data inevitably lead to better performance is being questioned, as returns diminish with increased scale.

The Need for Architectural Innovation

Given these limitations, there is a growing consensus that a radical shift in architectural design is necessary.

Pioneering efforts are already underway, with startups like Liquid.ai exploring non-Transformer architectures and academic institutions re-investigating older models like Recurrent Neural Networks (RNNs).

One notable example is the RWKV model, which aims to combine the strengths of Transformers and RNNs, offering efficient parallel training and linear scaling during inference.

There are more other attempts all over the AI community: another innovation came from NVIDIA. They presented exactly 1 week ago (with paper published on November the 20th) a new small hybrid model: Hymba is a 1.5B hybrid Mamba x Attention Model that outperforms other small LLMs like Llama-3.2 or SmolLM v2 being trained on only 1.5T Tokens. An efficient and innovative blend that uses a new hybrid architecture with Mamba and Attention heads running in parallel with additional meta tokens, to improve the efficacy of the model… and it can be used commercially (This model is released under the NVIDIA Open Model License Agreement).

Such innovations signal a move towards more efficient and capable AI architectures.

Conclusion

While current GenAI tools are remarkable, they represent just the beginning of a longer journey towards more sophisticated and reliable AI systems.

But we need to be intellectually honest, and acknowledge their limitations. Once this first step is done, it becomes so easy to invest our time and resources in architectural innovation.

I want to be part of the next generation of AI that overcomes today's challenges and unlocks new possibilities: won’t you?

Stay tuned for our next newsletter, where we'll dive deeper into the latest research and developments in AI architecture.

GIFT of the day: and article showing that there is plenty of amazing people, sharing their amazing results to solve daily real-world problems. And this is not something new!
 """

bruteText = bruteText.replace('\n\n','\n')
```

bruteText
```
"""
Do you think LLM can THINK? Beyond the Hype lies the future of Generative AI.
Exploring the limitations of current Models and anticipating architectural shifts
FABIO
DEC 02, 2024
Share
Before you learn how to write well with AI, you need to know how to write well.
Before you learn how to add your own voice to an AI’s output, you need to know your own voice.
Before you learn how to check whether AI summarizes a text correctly, you need to know how to read.
Before you learn how to check AI for hallucinations, you need to know how to research.
Artificial Intelligence is evolving so fast that generative models, particularly Large Language Models (LLMs), have captured the imagination of tech enthusiasts and industry leaders alike... and most probably even yours!
However, beneath the surface of this excitement lies a complex reality that rings many bells! We need a closer examination of many warning signs.
This newsletter, part 1 of a series, gives an introduction into the current state of GenAI, highlighting its limitations and giving you some glimpse into the future.
what to read — by lexica.art
In times of turmoil and controversy, listen to the quiet ones; the rest are picking sides to build their identity — Alberto Romero
So, in case you are already bored, I will say the most important things first: start following the quiet voices, people who thinks differently, that are able to speak up and disprove the hypes. Here a short list of the ones I trust:
The Algorithmic Bridge | Gary Marcus | The Kaitchup – AI on a Budget | Planet Earth & Beyond
The Hype vs. Reality
The prevailing narrative around GenAI is one of boundless potential, with promises of revolutionizing industries from content creation to customer service. Yet, a closer look reveals that while these models are impressive, they are not without flaws.
A recent survey by CNBC indicated that while 79% of respondents have tried Microsoft's Copilot, only 25% found it worthwhile. This discrepancy suggests that the expectations set by the hype may not align with the current capabilities of these tools.
It is a consolidated fact now, even though many have tried to throw smoke screens. Trying to keep the hype and secure founds, blindly bowing to the scaling law god as a sort of religion.
LLMs are not near AGI, not even close. We are living the beginning, an experimental phase of what it can become. But considering the huge amount of money invested in it, the so called gurus of AI don’t want to admit it.
But you don’t need to be a Machine Learning guru to see this coming!
What you need… is to look where modern prophets are pointing, where outliers meet.
Coming out of the metaphor. For months (now years) Big Tech has blindly moved capitals and resources promising the World the panacea of all evils. Generative AI has been pointed out as the new savior: and every bug and issue was washed away with a faithful (and blind) statement:
we simply need more GPUs and more training data
The reality is quite different. The Transformers architecture is an amazing achievement, it works wonders… but it has fundamental limits. It is a stepping stone, but it cannot be the final destination.
Fundamental Limitations
Current LLMs, predominantly based on the Transformer architecture, excel in many areas but struggle with several key issues:
Sequential Data Handling: These models have difficulty managing time-dependent sequences, which is crucial for tasks involving causality and temporal relationships.
Observability: There's a lack of transparency in how these models arrive at their outputs, making it hard to understand and trust their decision-making processes.
Computational Complexity: The quadratic increase in computational requirements with longer sequences poses significant scalability challenges.
Scaling Law Illusion: The belief that larger models and more data inevitably lead to better performance is being questioned, as returns diminish with increased scale.
The Need for Architectural Innovation
Given these limitations, there is a growing consensus that a radical shift in architectural design is necessary.
Pioneering efforts are already underway, with startups like Liquid.ai exploring non-Transformer architectures and academic institutions re-investigating older models like Recurrent Neural Networks (RNNs).
One notable example is the RWKV model, which aims to combine the strengths of Transformers and RNNs, offering efficient parallel training and linear scaling during inference.
There are more other attempts all over the AI community: another innovation came from NVIDIA. They presented exactly 1 week ago (with paper published on November the 20th) a new small hybrid model: Hymba is a 1.5B hybrid Mamba x Attention Model that outperforms other small LLMs like Llama-3.2 or SmolLM v2 being trained on only 1.5T Tokens. An efficient and innovative blend that uses a new hybrid architecture with Mamba and Attention heads running in parallel with additional meta tokens, to improve the efficacy of the model… and it can be used commercially (This model is released under the NVIDIA Open Model License Agreement).
Such innovations signal a move towards more efficient and capable AI architectures.
Conclusion
While current GenAI tools are remarkable, they represent just the beginning of a longer journey towards more sophisticated and reliable AI systems.
But we need to be intellectually honest, and acknowledge their limitations. Once this first step is done, it becomes so easy to invest our time and resources in architectural innovation.
I want to be part of the next generation of AI that overcomes today's challenges and unlocks new possibilities: won’t you?
Stay tuned for our next newsletter, where we'll dive deeper into the latest research and developments in AI architecture.
GIFT of the day: and article showing that there is plenty of amazing people, sharing their amazing results to solve daily real-world problems. And this is not something new!
""" 
```

### Create the prompt for stable Diffusion
```python
SD_prompt = f'Create a prompt for Stable Diffusion based on the information below. Return only the prompt.\---\n{headers}\n\nPROMPT:'
client = InferenceClient(token=token)
messages = [{"role": "user", "content": SD_prompt}]
completion = client.chat.completions.create(
    model="Qwen/Qwen2.5-72B-Instruct",
	messages=messages,
	max_tokens=500
)
ImageGEN_prompt = completion.choices[0].message.content
```
or
```python
from PIL import Image
client = InferenceClient("strangerzonehf/Flux-Midjourney-Mix2-LoRA", token=token)
# output is a PIL.Image object
image = client.text_to_image(ImageGEN_prompt)
image.save("twittpost002.png")
image.show()
```

<img src='https://github.com/fabiomatricardi/HF-API-tutorial/raw/main/images/twittpost001.png' width=600>

As you can see we have 0 control on the generation parameters.
```python
client = Client("stabilityai/stable-diffusion-3.5-large")
result = client.predict(
		prompt=ImageGEN_prompt,
    	negative_prompt='blur',
		seed=0,
		randomize_seed=True,
		width=1360,
		height=768,
		guidance_scale=4.5,
		num_inference_steps=30,
		api_name="/infer"
temp = result[0]
image = Image.open(temp)
image.save("output_image.png")
image.show()
```
<img src='https://github.com/fabiomatricardi/HF-API-tutorial/raw/main/images/output_image.png' width=900>

### Generate 3 Tweets from the newsletter
```
Tweet_prompt = f"""Read the following newsletter. rewrite it into 3 twitter posts in English, in progression.
---
{bruteText}"""
```
Now we call the same `Qwen/Qwen2.5-72B-Instruct` endpoint and split the tweets into 3 
```python
client = InferenceClient(token=token)
messages = [{"role": "user", "content": Tweet_prompt}]
completion = client.chat.completions.create(
    model="Qwen/Qwen2.5-72B-Instruct",
	messages=messages,
	max_tokens=500
)
from rich.console import Console
console = Console(width=80)
tweet1 = completion.choices[0].message.content.split('1:')[1].split('\n\n')[0]
tweet2 = completion.choices[0].message.content.split('2:')[1].split('\n\n')[0]
tweet3 = completion.choices[0].message.content.split('3:')[1]
console.print(tweet1)
console.rule()
console.print(tweet2)
console.rule()
console.print(tweet3)
console.rule()
```
The result is like this
```
ORIGINaL RESULT...

### Tweet 1:
Before diving into AI writing, know your own writing voice. Before trusting AI summaries, learn to read critically. Before dismissing AI hallucinations, master research. AI is evolving, but it starts with you. #GenAI #LLMs #TechTrends

### Tweet 2:
The hype around Generative AI is real, but it's crucial to see beyond the surface. LLMs, while impressive, have significant limitations in handling sequential data, transparency, and computational complexity. The scaling law isn’t a magic solution. #AIReality #TechDebate

### Tweet 3:
Innovation in AI architecture is on the horizon. Startups and researchers are exploring non-Transformer models like RWKV and Hymba, which offer efficient parallel training and linear scaling. The future of AI is about more than just size—it's about smarter design. Stay tuned for more! #AIFuture #TechInnovation
```

final
```
Before diving into AI writing, know your own writing voice. Before trusting AI 
summaries, learn to read critically. Before dismissing AI hallucinations, master
research. AI is evolving, but it starts with you. #GenAI #LLMs #TechTrends
────────────────────────────────────────────────────────────────────────────────
The hype around Generative AI is real, but it's crucial to see beyond the 
surface. LLMs, while impressive, have significant limitations in handling 
sequential data, transparency, and computational complexity. The scaling law 
isn’t a magic solution. #AIReality #TechDebate
────────────────────────────────────────────────────────────────────────────────
Innovation in AI architecture is on the horizon. Startups and researchers are 
exploring non-Transformer models like RWKV and Hymba, which offer efficient 
parallel training and linear scaling. The future of AI is about more than just 
size—it's about smarter design. Stay tuned for more! #AIFuture #TechInnovation

```

















