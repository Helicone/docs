# How we calculate costs

### OpenAI Non-Streaming

OpenAI completions respond with a `usage` tag on non-streaming requests that look something like this:

```json
"usage": {
	"prompt_tokens": 11,
	"completion_tokens": 9,
	"total_tokens": 20
},
```

We capture this data and then use OpenAI pricing tables to measure the pricing based on the model returned in the body. \
[https://openai.com/pricing#language-models](https://openai.com/pricing#language-models)

### OpenAI Streaming

Unfortunately for OpenAI streaming requests, we do not get the `usage` tag back. So, we must rely on 3rd party tokenizers like [TikToken](https://github.com/openai/tiktoken) to count our tokens. However, there is a lot of added complexity when there are Chat messages since hidden tokens are abstracted away from the user. To get around this, we have reverse-engineered their hidden tokens to accurately estimate the amount of prompt and completion tokens.

### Anthropic Requests

For Anthropic requests we also have to hand calculate the tokens using a python server since there is no supported method for calculating tokens in Typescript. See our comments on this thread: [https://github.com/anthropics/anthropic-sdk-typescript/issues/16](https://github.com/anthropics/anthropic-sdk-typescript/issues/16)

### Developer

You can see our pricing table here

[https://github.com/Helicone/helicone/blob/main/web/lib/sql/constants.ts#L4-L17](https://github.com/Helicone/helicone/blob/main/web/lib/sql/constants.ts#L4-L17)
