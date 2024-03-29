---
description: The latency of your GPT-3 endpoint is important to your application's success
---

# Latency

Helicone leverages Cloudflare's global network of servers as proxies for efficient web traffic routing. Cloudflare workers maintain extremely low latency through their worldwide distribution. This results in a fast and reliable proxy to your OpenAI requests.

### Benchmarking Helicone's proxy service

Our experiment:

* We interweaved 500 requests with unique prompts to both OpenAI and Helicone.&#x20;
* Both got the same requests in the same 1s window, and we varied which endpoint went first for each request.
* We maxed out the prompt context window to make these requests as big as possible.
* We used `text-ada-001`.
* We logged the latency of the roundtrip time to complete both roundtrips.

#### Results

| Statistic          | Openai (s) | Helicone (s) |
| ------------------ | ---------- | ------------ |
| Mean               | 2.21       | 2.21         |
| Median             | 2.87       | 2.90         |
| Standard Deviation | 1.12       | 1.12         |
| Min                | 0.14       | 0.14         |
| Max                | 3.56       | 3.76         |
| p10                | 0.52       | 0.52         |
| p90                | 3.27       | 3.29         |

The metrics are almost the same, except that Helicone had a few requests that ran longer at the right tail.

<figure><img src="../.gitbook/assets/openai-helicone.png" alt=""><figcaption></figcaption></figure>

If you have any suggestions about how to benchmark the latency addition to Helicone's proxy, drop a note in our [Discord](https://discord.gg/zsSTcH2qhG)!

