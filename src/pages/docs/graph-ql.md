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
  requestNewPrompt(body: { stableDiffusionV1_4: { prompt: "Elephant!" } }) {
    id
    prompt
    user {
      id
    }
  }
}
```

### Get results

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
      ... on Result_Unknown_Audio_V0 {
        id
      }
    }
  }
}
```
