---
description: Omit response and requests
---

# Omit Logs

In some cases you may not want to have Helicone store or log your request body or response body.

You can easily omit these by adding the `Helicone-Omit-Request` or `Helicone-Omit-Response` header and setting it to `"true"`.

## Getting Started

{% tabs %}
{% tab title="Curl" %}

<pre class="language-bash"><code class="lang-bash">curl https://oai.hconeai.com/v1/completions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
<strong>  -H 'Helicone-Omit-Request: true' \
</strong><strong>  -H 'Helicone-Omit-Response: true' \
</strong> -d '{
    "model": "text-davinci-003",
    "prompt": "How do I enable custom rate limit policies?",
}'
</code></pre>

{% endtab %}

{% tab title="Python" %}

<pre class="language-python"><code class="lang-python">openai.api_base = "https://oai.hconeai.com/v1"

openai.Completion.create(
    model="text-davinci-003",
    prompt="How do I enable retries?",
    headers={
<strong>        "Helicone-Omit-Request": "true",
</strong> <strong>        "Helicone-Omit-Response": "true",
</strong>    }
)
</code></pre>

{% endtab %}

{% tab title="Node" %}

<pre class="language-javascript"><code class="lang-javascript">import { Configuration, OpenAIApi } from "openai";
const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  basePath: "https://oai.hconeai.com/v1",
  baseOptions: {
    headers: {
<strong>      "Helicone-Omit-Request": "true",
</strong><strong>      "Helicone-Omit-Response": "true",
</strong>    },
  },
});
const openai = new OpenAIApi(configuration);
</code></pre>

{% endtab %}
{% endtabs %}
