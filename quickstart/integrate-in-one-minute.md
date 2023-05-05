---
description: >-
  However you're using OpenAI, get instant observability into your usage,
  errors, rate limits, and more
---

# Integrate in one minute

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

2. **Add the Helicone auth header to the request**

```
"Helicone-Auth": "Bearer HELICONE_API_KEY"
```
{% endtab %}

{% tab title="Python" %}
### Package Integration

#### Step 1: Set HELICONE\_API\_KEY as an environment variable

```bash
export HELICONE_API_KEY=<your API key>
```

#### Step 2: Install the helicone package

```
pip install helicone
```

#### Step 3: Change OpenAI import to use Helicone&#x20;

<pre class="language-python"><code class="lang-python"><strong>from helicone import openai # replace `import openai` with this line
</strong></code></pre>

That's it! Your OpenAI requests now log results to Helicone. You can now use advanced Helicone features as parameters:

<pre class="language-python"><code class="lang-python">response = openai.Completion.create(
	model="text-davinci-003",
	prompt="What is Helicone?",
	user="alice@bob.com",
<strong>	cache=True,
</strong><strong>	properties={"conversation_id": 12},
</strong><strong>	rate_limit_policy={"quota": 100, "time_window": 60, "segment": "user"},
</strong><strong>	retry=True,
</strong>)
</code></pre>

### Package-less Integration

You can also integrate Helicone in Python without using any package

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
### Package Integration

#### Step 1: Set HELICONE\_API\_KEY as an environment variable

```bash
export HELICONE_API_KEY=<your API key>
```

#### Step 2: Install the helicone-openai package

```bash
npm install helicone-openai
```

#### Step 3: Change OpenAI import to use Helicone&#x20;

```typescript
const { Configuration, OpenAIApi } = require("helicone-openai"); 
// replace `require("openai")` with this line
```

#### Step 4: Include Helicone API Key in the Configuration object

<pre class="language-typescript"><code class="lang-typescript">const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
<strong>  heliconeApiKey: process.env.HELICONE_API_KEY,
</strong>})
</code></pre>

That's it! Your OpenAI requests now log results to Helicone. You can now use advanced Helicone features as `Configuration` parameters:

<pre class="language-typescript"><code class="lang-typescript">const configuration = new Configuration({
  apiKey,
  heliconeApiKey,
<strong>  cache: true,
</strong><strong>  retry: true,
</strong><strong>  properties: {
</strong><strong>    Session: "24",
</strong><strong>    Conversation: "support_issue_2",
</strong><strong>  },
</strong><strong>  rateLimitPolicy: { 
</strong><strong>    quota: 10, 
</strong><strong>    time_window: 60,
</strong><strong>    segment: "Session",
</strong>  }
});
</code></pre>

### Package-less Integration

You can also integrate Helicone in Node.js without using any package. Update your existing OpenAI library configuration as follows:

<pre class="language-typescript"><code class="lang-typescript">import { Configuration, OpenAIApi } from "openai";

const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
<strong>  basePath: "https://oai.hconeai.com/v1",
</strong>  baseOptions: {
    headers: {
<strong>      "Helicone-Auth": `Bearer ${process.env.HELICONE_API_KEY}`,
</strong>    },
  },
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



