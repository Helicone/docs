---
title: Self Hosted Workers
description:
---

Configure your own workers and use our API to report back jobs.

The worker graphql endpoint is actually a completely separate GraphQL instance that is hosted at https://bhunk.io/api/worker/graphql.

## Setup

in https heads add

```json
{
  "authorization": "MY KEY"
}
```

## Fetching a new job

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

## Sending back a result

NOTE: The images must be well formatted. Please see the example clients at https://github.com/bhunkio/bhunk.io-client for how to correctly format these images.

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
