---
title: Typescript SDK
description: Use typescript SDK to easily access PromptZero within your applications
---

You can find the most up to date documentation and package information on npm here
[https://www.npmjs.com/package/promptzero](https://www.npmjs.com/package/promptzero)

## Install

```
yarn add promptzero
```

## Example

Here is an example

```typescript
import { PromptZero } from 'promptzero'

const promptZero = new PromptZero('<KEY>')
const newPrompt = await promptZero.requestNewPrompt('cheese')
const promptId = newPrompt.data.requestNewPrompt.id
console.log(newPrompt.data.requestNewPrompt.id)

// Right now you will have to poll for the
// result until we implement webhooks. (coming soon!)
for (let i = 0; i < 10; i++) {
  const status = await promptZero.getPromptStatus(promptId)
  console.log(status)
  if (status.toLowerCase() === 'completed') {
    break
  }
  await new Promise((f) => setTimeout(f, 3000))
}

const result = await promptZero.getPromptResult(promptId)
console.log(result.data.requestedPrompt.result.images)
```

### Have an issue?

Please file an Issue or PR [here](https://github.com/PromptZero/typescript-sdk).
