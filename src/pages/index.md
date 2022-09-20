---
title: Getting started
pageTitle: Bhunkio
description: Cache every single thing your app could ever do ahead of time, so your code never even has to run at all.
---

Quickly get started using Bhunkio and get read to ship your product across the world 🌍.{% .lead %}

---

## How bunkio works

Bhunkio provides a similar user experience as [Dream Studio](https://beta.dreamstudio.ai/dream), however we give power to the user and offer a low barrier to entry while empowering users to scale their products built on top of Stable Diffusion.

We do this by allowing you to request any image generation request, and having it either run on any of your [client nodes](/docs/writing-plugins) or on our [cloud platform](https://bhunk.io/cloud-platform).

## Using our UI

Users can easily access our UI by [signing up](https://bhunk.io/sign-up).

TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here

### Requesting an Image

TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here
TODOTODOTODOTODOTODOTODOTODO Screenshot here

### Understanding the queue

Each image you request will be queued and not actually ran until you set up a worker to execute these jobs.

Here you have two options

1. [Run your own client](/docs/host-yourself)
1. [Subscribe to bhunkio cloud](https://bhunk.io/cloud-platform)

## Using our API

After you have [generated your API key](/docs/generating-api-key) the rest is easy!

You can choose to

## Quick start for **free** using your own hardware!

{% callout link="kjasd" type="installation" title="Are you a bhunkio cloud subscriber?" %}
_Skip this section and go straight to [Quick start API](#quick-start-api)_.
{% /callout %}

### Generating worker API Keys

First you will need to [generate an API key](/docs/generating-api-key) and just make sure that the `worker` permission is toggled on.

### M1 mac

Requirements: 8 Gigs of RAM

```bash
brew install bhunkio
bhunkio run --api_key <API_KEY>
```

### Windows or Linux with an Nvidia GPU

Make sure you have [Docker](https://docs.docker.com/engine/install/) installed.

```bash
sudo docker run -it --gpus=all --env API_KEY=<API_KEY> --env BHUNKIO_URL=https://www.bhunk.io chitalian/bhunkio-client:0.0.1 bash -c "conda run --no-capture-output -n ldm python bhunkio.py"
```

### Using RunPod

RunPod offers secure GPU rentals with a single click config. You can rent a A4000 for about ~0.20 USD/hour. This is by far the cheapest option we have found. There is also an officially support template, so you can simply make an account and select `Bhunkio` as a template. Paste in your API Key and deploy!
