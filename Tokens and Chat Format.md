# Tokens and chat format of LLM'S

For knowing more about the kind of LLM's and various roles in OpenAI API, refer this: https://github.com/Praddyumn16/ChatGPT-Prompt-Engineering/blob/main/1.%20Introduction.md 

Below is the helper code to get started with OpenAI API:
```python
import os
import openai
import tiktoken
from dotenv import load_dotenv, find_dotenv
_ = load_dotenv(find_dotenv()) # read local .env file

openai.api_key  = os.environ['OPENAI_API_KEY']

def get_completion(prompt, model="gpt-3.5-turbo"):
    messages = [{"role": "user", "content": prompt}]
    response = openai.ChatCompletion.create(
        model=model,
        messages=messages,
        temperature=0,
    )
    return response.choices[0].message["content"]

response = get_completion("What is the capital of France?")
print(response) # prints: "The capital of France is Paris."
```
---
Now, if you take the word "lollipop" and ask ChatGPT to reverse it, this is what you see:
```python
response = get_completion("Take the letters in lollipop and reverse them")
print(response)
# output: The reversed letters of "lollipop" are "pillipol".
```
But, "lollipop" in reverse should be "popillol".

This is because, LLM's do not necessarily predict the next **Word**,  instead they predict the next **Token.**
Where, a **token** is just a commonly occuring sequence of characters.

So if I give a sentence like: "Learning new things is fun!" to ChatGPT then it will consider every word/a word with a space/an exclamation mark as a single token. Since each of them are fairly common occuring terms.

But if we give a sentence like: 
