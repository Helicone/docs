# Async

Helicone works with asynchronous requests normally.

All you have to do is import `helicone` or import `openai` through the Helicone package and the rest of your code works normally.

```python
from helicone import openai
```

Let's demonstrate how you'd make synchronous or asynchronous requests with the OpenAI package. The following examples work with or without Helicone!



**Asynchronous requests not in streaming mode**

Here, the request is made asynchronously, and the response is not streamed. Note that you'll need to use the `await` keyword when calling `openai.ChatCompletion.acreate`.

```python
pythonCopy coderesponse = await openai.ChatCompletion.acreate(
    model = 'gpt-3.5-turbo',
    messages = [{
        'role': 'user',
        'content': "Hello World!"
    }],
    stream=False
)

print(response["choices"][0]["message"]["content"])
```



**Asynchronous in streaming mode**

In this mode, both the request is made asynchronously and the response is streamed. You'll need to use the `await` keyword when calling `openai.ChatCompletion.acreate`, and use an `async for` loop to iterate over the response.

```python
pythonCopy codeasync for chunk in await openai.ChatCompletion.acreate(
    model = 'gpt-3.5-turbo',
    messages = [{
        'role': 'user',
        'content': "Hello World!"
    }],
    properties={"mode": "Acreate and stream=True"},
    stream=True
):
    content = chunk["choices"][0].get("delta", {}).get("content")
    if content is not None:
        print(content, end='')
```
