---
description: >-
  However you're using OpenAI, get instant observability into your usage,
  errors, rate limits, and more
---

# Integrate in one line of code

{% tabs %}
{% tab title="Curl" %}
Replace the OpenAI base url

```url
POST https://api.openai.com/v1
```

with Helicone's

```
POST https://oai.hconeai.com/v1
```
{% endtab %}

{% tab title="Python" %}
Change the default base API url to Helicone's



<pre class="language-python"><code class="lang-python">import openai

<strong>openai.api_base = "https://oai.hconeai.com/v1"
</strong></code></pre>
{% endtab %}

{% tab title="Node.js" %}
Add a `basePath` to the `Configuration:`



Before:

```typescript
import { Configuration, OpenAIApi } from "openai";

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY
});

const openai = new OpenAIApi(configuration);
```



After:

<pre class="language-typescript"><code class="lang-typescript">import { Configuration, OpenAIApi } from "openai";

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
<strong>  basePath: "https://oai.hconeai.com/v1",
</strong>});

const openai = new OpenAIApi(configuration);
</code></pre>
{% endtab %}

{% tab title="Langchain" %}
Helpful links:

* [LangChain+Helicone Typescript Docs](https://hwchase17.github.io/langchainjs/docs/ecosystem/helicone/)
* [LangChain+Helicone Python Docs](https://langchain.readthedocs.io/en/latest/ecosystem/helicone.html)



(Python) Using env variable

<pre class="language-bash"><code class="lang-bash"><strong>export OPENAI_API_BASE="https://oai.hconeai.com/v1"
</strong>python3 your_lang_chain_program.py
</code></pre>

(Python) Change it within code

<pre class="language-python"><code class="lang-python">import openai
<strong>openai.api_base = "https://oai.hconeai.com/v1"
</strong></code></pre>

(TypeScript) add basepath on the creation of the OpenAI object

```typescript
const model = new OpenAI(
  {},
  {
    basePath: "https://oai.hconeai.com/v1",
  }
);
```
{% endtab %}

{% tab title="GPT Index" %}
Change the base URL:

<pre class="language-bash"><code class="lang-bash"><strong>export OPENAI_API_BASE="https://oai.hconeai.com/v1"
</strong>python3 your_gpt_index_program.py
</code></pre>
{% endtab %}
{% endtabs %}

📝 By integrating with our API, you agree to our [Privacy Policy](https://www.helicone.ai/privacy) and [Terms of Services](https://www.helicone.ai/terms) agreements.



### Congratulations! That was easy, wasn't it? 🙌

Once you've integrated, [**login to the web application**](https://www.helicone.ai/onboarding?step=2) to see your requests and metrics :house\_with\_garden:&#x20;



