---
title: Access Bhunkio using GraphQL
description: Quidem magni aut exercitationem maxime rerum eos.
---

## What is GraphQL?

TODO

## Quick start using GraphQL Playground

### Setup

in https heads add

```json
{
  "authorization": "MY KEY"
}
```

### Request an Audio prompt

```graphql
mutation {
  requestNewPrompt(body: { unknownAudioV0: { prompt: "my new song" } }) {
    id
    prompt
    user {
      id
    }
  }
}
```

### Request an Image prompt

```graphql
mutation {
  requestNewPrompt(
    body: {
      stableDiffusionV1_4: {
        action: txt2img
        prompt: "blue elephant on a unicycle"
        steps: 40
      }
    }
  ) {
    id
    prompt
  }
}
```

### Get results Audio

```graphql
{
  requestedPrompts(limit: 100) {
    status
    result {
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

### Get results Stable Diffusion

```graphql
{
  requestedPrompts(limit: 100) {
    status
    result {
      ... on Result_StableDiffusionV1_4 {
        __typename
        id
        images {
          url
        }
      }
    }
  }
}
```
