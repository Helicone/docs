---
title: Run your own workers
description:
---

{% callout link="kjasd" type="installation" title="Don't want to run your own worker?" %}
_Subscribe to [PromptZero Cloud](https://www.promptzero.com/cloud)_
{% /callout %}

Configure your own workers and use our API to report back jobs.

The worker graphql endpoint is actually a completely separate GraphQL instance that is hosted at https://promptzero.com/api/worker/graphql.

## Running your own workers

### Generating worker API Keys

First you will need to [generate an API key](/docs/generating-api-keys) and just make sure that the `worker` permission is toggled on.

### M1 mac

_support coming soon_

### Linux or Windows with an Nvidia GPU

Make sure you have [Docker](https://docs.docker.com/engine/install/) installed.

```bash
sudo docker run -it --gpus=all --env API_KEY=<API_KEY> --env PROMPT_ZERO_URL=https://www.promptzero.com chitalian/promptzero-worker:0.0.1 bash -c "conda run --no-capture-output -n ldm python prompt_zero.py"
```

### Using RunPod

RunPod offers secure GPU rentals with a single click config. You can rent a A4000 for about ~0.20 USD/hour. This is by far the cheapest option we have found. There is also an officially support template, so you can simply make an account and select `PromptZero` as a template. Paste in your API Key and deploy!

## GraphQL

You can manually write your own worker as well with your own fine tuned parameters and use our GraphQL api to run your workers.

Worker graphql url: [https://www.promptzero.com/api/worker/graphql](https://www.promptzero.com/api/worker/graphql)

### Setup

in https heads add

```json
{
  "authorization": "MY KEY"
}
```

### Fetching a new job

This will actually set the job state to working.

```graphql
mutation {
  requestNewJob(jobType: { stableDiffusionV1_4: { action: txt2img } }) {
    prompt
    id
    params {
      ... on ResultParams_StableDiffusionV1_4 {
        action
        prompt
        width
        height
      }
    }
  }
}
```

### Sending back a result

NOTE: The images must be well formatted. Please see the example clients at https://github.com/PromptZero/worker for how to correctly format these images.

```graphql
mutation {
  postJobResult(
    jobType: {
      id: "prompt uuid"
      stableDiffusionV1_4: {
        images: [
          "byte array representing an image"
          "byte array representing an image"
        ]
      }
    }
  ) {
    message
  }
}
```
