---
description: (Coming soon)
---

# Exponential Backoff for Rate-Limited Requests

Helicone will soon supports exponential backoff, a technique used to handle rate-limited requests.

When an API returns a rate-limit error, it typically means that the user or client has exceeded the maximum number of requests allowed within a specific period of time. In this situation, the user or client needs to wait before making another request.&#x20;

Exponential Backoff is a technique that Helicone uses to handle rate-limited requests in a more efficient way. Instead of immediately retrying the request, Helicone will wait for a short period of time and then retry the request. If the request is still rate-limited, Helicone will wait for a longer period of time before retrying the request. This process continues, with each retry increasing the wait time exponentially, until the request is successful or the maximum number of retries is reached.

### Configuring exponential backoff

Exponential backoff is not enabled by default and will be fully configurable. You will be able to specify how many attempts to make and how long to wait between repeated attempts.
