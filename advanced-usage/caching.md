---
description: Reduce latency and save costs by caching on the edge
---

# Caching

Caching, by temporarily storing data closer to the user at the edge, significantly speeds up access time and enhances application performance. This edge deployment ensures low latency, resulting in faster responses and an efficient app development process.

<figure><img src="../.gitbook/assets/Screen Shot 2023-05-21 at 6.05.03 PM.png" alt=""><figcaption></figcaption></figure>

## Quick start

To get started, just set `Helicone-Cache-Enabled` to `true` in the headers, or use the Python or NPM packages to turn it on via parameters.

{% tabs %}
{% tab title="Curl" %}
<pre class="language-bash"><code class="lang-bash">curl https://oai.hconeai.com/v1/completions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
<strong>  -H 'Helicone-Cache-Enabled: true' \
</strong>  -d '{
    "model": "text-davinci-003",
    "prompt": "How do I enable caching?",
}'
</code></pre>
{% endtab %}

{% tab title="Python" %}
With the package:

<pre class="language-python"><code class="lang-python">response = openai.Completion.create(
	model="text-davinci-003",
	prompt="How do I cache with helicone?",
<strong>	cache=True,
</strong>)
</code></pre>

Without the package:

<pre class="language-python"><code class="lang-python">openai.api_base = "https://oai.hconeai.com/v1"

openai.Completion.create(
    model="text-davinci-003",
    prompt="How do I cache with helicone?",
    headers={
<strong>      "Helicone-Cache-Enabled": "true",
</strong>    }
)
</code></pre>
{% endtab %}

{% tab title="Node.js" %}
<pre class="language-typescript"><code class="lang-typescript">import { Configuration, OpenAIApi } from "openai";
const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  basePath: "https://oai.hconeai.com/v1",
  baseOptions: {
    headers: {
<strong>      "Helicone-Cache-Enabled": "true",
</strong>    },
  },
});
const openai = new OpenAIApi(configuration);
</code></pre>
{% endtab %}
{% endtabs %}

The default caching limit is `7 days` , if you want a longer cache please refer to the [Cache Parameters](caching.md#cache-parameters) section and add the `Cache-Control` header to your request.

## Limitations

The max time limit for a cache limit is `365 days`

## Cache Parameters

`Helicone-Cache-Enabled (required)`: This will enable storing and loading from your cache

`Cache-Control (optional)`: Allow you to configure based on the [Cloudflare Cache Directive](https://developers.cloudflare.com/cache/about/cache-control#cache-control-directives), currently only `max-age` is supported, but we will be adding more configuration options soon.

Example of setting the cache  to `2592000 seconds` aka `30 days:`

`"Cache-Control": "max-age=`2592000`"`&#x20;



### Cache Buckets

You can increase the size of the cache bucket, so that after the `n'th` request we randomly choose from a previously cached element within the bucket.&#x20;

Here is an example with a bucket size of `3`

```
openai.completion("give me a random number") -> "42"
# Cache Miss
openai.completion("give me a random number") -> "47"
# Cache Miss
openai.completion("give me a random number") -> "17"
# Cache Miss

openai.completion("give me a random number") -> This will randomly choose 42 | 47 | 17
# Cache Hit

```

### Configuring Bucket size

Simply add `Helicone-Cache-Bucket-Max-Size` with some number to choose how large you want your Bucket size to be.

Note: The max number of caches you can store is `20` within a bucket, if you want more you will need to upgrade to an enterprise plan.

{% tabs %}
{% tab title="Python" %}
```python
openai.api_base = "https://oai.hconeai.com/v1"

openai.Completion.create(
    model="text-davinci-003",
    prompt="Say this is a test",
    headers={
        "Helicone-Auth": "Bearer HELICONE_API_KEY",
        "Helicone-Cache-Enabled": "true",
        "Helicone-Cache-Bucket-Max-Size": "5",
    }
)
```
{% endtab %}

{% tab title="Typescript" %}
```typescript
import { Configuration, OpenAIApi } from "openai";
const configuration = new Configuration({
  apiKey: process.env.OPENAI_API_KEY,
  basePath: "https://oai.hconeai.com/v1",
  baseOptions: {
    headers: {
      "Helicone-Cache-Enabled": "true",
      "Helicone-Cache-Bucket-Max-Size": "5",
    },
  },
});
const openai = new OpenAIApi(configuration);
```
{% endtab %}
{% endtabs %}







<details>

<summary>Advanced Caching</summary>

We allow dynamic settings to configure whether or not you want to treat your cache as a read-only or write-only.\
\
Ex: When developing locally you might want to only be loading in the cache and not reading from the cache, while on prod you might only want reads from the cache. &#x20;

You can set either one of these headers instead of `Helicone-Cache-Enabled`.

```
// Only saves to the cache
"Helicone-Cache-Save": "true"

// Only reads and no saves
"Helicone-Cache-Read": "true"
```



</details>

