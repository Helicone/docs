# Streaming

Helicone smoothly integrates streaming functionality and offers benefits that you can't find with the standard OpenAI package!&#x20;

<mark style="background-color:yellow;">Currently, OpenAI doesn't provide usage statistics such as prompt and completion tokens.</mark> However, Helicone overcomes this limitation by estimating these statistics with the help of the `gpt3-tokenizer` package, which is designed to work with all tokenized OpenAI GPT models.

All you have to do is import `helicone` or import `openai` through the Helicone package and the rest of your code works as it does.

```python
from helicone import openai
```

The following examples work with or without Helicone!



**Streaming mode with synchronous requests**

In this mode, the request is made synchronously, but the response is streamed.

```python
pythonCopy codefor chunk in openai.ChatCompletion.create(
    model = 'gpt-3.5-turbo',
    messages = [{
        'role': 'user',
        'content': "Hello World!"
    }],
    stream=True
):
    content = chunk["choices"][0].get("delta", {}).get("content")
    if content is not None:
        print(content, end='')
```



**Streaming mode with asynchronous requests**

In this mode, both the request is made asynchronously and the response is streamed. You'll need to use the `await` keyword when calling `openai.ChatCompletion.acreate`, and use an `async for` loop to iterate over the response.

```python
pythonCopy codeasync for chunk in await openai.ChatCompletion.acreate(
    model = 'gpt-3.5-turbo',
    messages = [{
        'role': 'user',
        'content': "Hello World!"
    }],
    stream=True
):
    content = chunk["choices"][0].get("delta", {}).get("content")
    if content is not None:
        print(content, end='')
```
