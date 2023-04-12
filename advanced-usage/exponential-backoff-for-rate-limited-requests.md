---
description: Intelligently retry requests to overcome rate limits and overloaded servers
---

# Retries

Retrying requests is a common best practice when dealing with overloaded servers or hitting rate limits. These issues typically manifest as HTTP status codes 429 (Too Many Requests) and 500 (Internal Server Error). For more information on error codes, see the [OpenAI API error codes documentation](https://platform.openai.com/docs/guides/error-codes/api-errors).

### Exponential Backoff

To effectively deal with retries, we use a strategy called exponential backoff. Exponential backoff involves increasing the wait time between retries exponentially, which helps to spread out the request load and gives the server a chance to recover. This is done by multiplying the wait time by a factor (default is 2) for each subsequent retry.

### Quick Start

To get started, set `Helicone-Retry-Enabled` to  `true`

{% tabs %}
{% tab title="Curl" %}
<pre class="language-bash"><code class="lang-bash">curl https://oai.hconeai.com/v1/completions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
<strong>  -H 'Helicone-Retry-Enabled: true' \
</strong>  -d '{
    "model": "text-davinci-003",
    "prompt": "How do I enable retries?",
}'
</code></pre>
{% endtab %}

{% tab title="Python" %}
<pre class="language-python"><code class="lang-python">openai.api_base = "https://oai.hconeai.com/v1"

openai.Completion.create(
    model="text-davinci-003",
    prompt="How do I enable retries?",
    headers={
<strong>      "Helicone-Retry-Enabled": "true",
</strong>    }
)
</code></pre>
{% endtab %}

{% tab title="Node" %}
<pre class="language-typescript"><code class="lang-typescript">import { Configuration, OpenAIApi } from "openai";
const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  basePath: "https://oai.hconeai.com/v1",
  baseOptions: {
    headers: {
<strong>      "Helicone-Retry-Enabled": "true",
</strong>    },
  },
});
const openai = new OpenAIApi(configuration);
</code></pre>
{% endtab %}
{% endtabs %}

### Advanced Usage

You can customize the behavior of the retries feature by setting additional headers in your request.

| Parameter                    | Description                                       | Default Value |
| ---------------------------- | ------------------------------------------------- | ------------- |
| `helicone-retry-num`         | Number of retries                                 | 5             |
| `helicone-retry-factor`      | Exponential backoff factor                        | 2             |
| `helicone-retry-min-timeout` | Minimum timeout (in milliseconds) between retries | 1000          |
| `helicone-retry-max-timeout` | Maximum timeout (in milliseconds) between retries | 10000         |

{% hint style="info" %}
Header values have to be strings, for example `"helicone-retry-num": "3"`
{% endhint %}

