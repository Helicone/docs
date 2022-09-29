---
title: Access PromptZero using GraphQL
description:
---

## Quick start using GraphQL Playground

Visit the PromptZero [playground](https://promptzero.com/api/graphql) to get started.

{% callout link="kjasd" type="note" title="Pro tip" %}
`ctrl`+`space bar`in the playground to open intellisense.
{% /callout %}

### Setup

In the bottom of the playground add your authorization header.

```json
{
  "authorization": "MY KEY"
}
```

### Request an Stable Diffusion Image

```graphql
mutation {
  requestNewPrompt(
    body: {
      stableDiffusionV1_4: {
        action: txt2img
        prompt: "blue elephant on a unicycle"
      }
    }
  ) {
    id
    prompt
  }
}
```

### Get the most recent results

```graphql
{
  requestedPrompts(
    limit: 100
    orderBy: { orderBy: CreatedAt, direction: Dsc }
  ) {
    status
    result {
      ... on Result_StableDiffusionV1_4 {
        __typename
        id
        images {
          url
        }
      }
      ... on Result_UnknownAudioV0 {
        id
        audioFiles {
          url
        }
      }
    }
  }
}
```
