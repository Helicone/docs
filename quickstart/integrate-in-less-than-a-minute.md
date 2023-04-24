---
description: >-
  However you're using OpenAI, get instant observability into your usage,
  errors, rate limits, and more
---

# Integrate in less than a minute

First, claim your `HELICONE_API_KEY` by signing up [here](https://www.helicone.ai/), or if you are already signed up, login and go to the [Keys page](https://www.helicone.ai/keys).&#x20;

{% tabs %}
{% tab title="Curl" %}
1. **Replace the OpenAI base url**

```url
POST https://api.openai.com/v1
```

with Helicone's

```
POST https://oai.hconeai.com/v1
```

2. **Add the Helicone auth header**

```
"Helicone-Auth": "Bearer HELICONE_API_KEY"
```
{% endtab %}

{% tab title="Python" %}
Change the default base API url to Helicone's



<pre class="language-python"><code class="lang-python">import openai

<strong>openai.api_base = "https://oai.hconeai.com/v1"
</strong>openai.Completion.create(
    # ...other parameters
    headers={
<strong>      "Helicone-Auth": "Bearer HELICONE_API_KEY",
</strong>    }
)
</code></pre>
{% endtab %}

{% tab title="Node.js" %}
<pre class="language-typescript"><code class="lang-typescript">import {Configuration, OpenAIApi} from "openai";

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  // Add a basePath to the Configuartion
<strong>  basePath: "https://oai.hconeai.com/v1",
</strong>  {
    headers: {
      // Add your Helicone API Key
<strong>      "Helicone-Auth": "Bearer HELICONE_API_KEY",
</strong>    },
  }
});

const openai = new OpenAIApi(configuration);
</code></pre>
{% endtab %}

{% tab title="Langchain" %}
Helpful links:

* [LangChain+Helicone Typescript Docs](https://hwchase17.github.io/langchainjs/docs/ecosystem/helicone/)
* [LangChain+Helicone Python Docs](https://langchain.readthedocs.io/en/latest/ecosystem/helicone.html)

### Python

<pre class="language-python"><code class="lang-python"><strong>openai.api_base = "https://oai.hconeai.com/v1"
</strong>
llm = OpenAI(
  temperature=0.9,
  headers={
<strong>    "Helicone-Auth": "Bearer HELICONE_API_KEY"
</strong>  }
)
</code></pre>

### Typescript

<pre class="language-typescript"><code class="lang-typescript">const model = new OpenAI(
  {},
  {
<strong>    basePath: "https://oai.hconeai.com/v1",
</strong>    baseOptions: {
      headers: {
<strong>        "Helicone-Auth": "Bearer HELICONE_API_KEY"
</strong>      },
    },
  }
);
</code></pre>
{% endtab %}
{% endtabs %}

📝 By integrating with our API, you agree to our [Privacy Policy](https://www.helicone.ai/privacy) and [Terms of Services](https://www.helicone.ai/terms) agreements.



### Congratulations! That was easy, wasn't it? 🙌

Once you've integrated, [**login to the web application**](https://www.helicone.ai/onboarding?step=2) to see your requests and metrics :house\_with\_garden:&#x20;



