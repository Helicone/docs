---
description: Visualize the prompts, values, and completions
---

# Templated prompts

### What are Templated Prompts?

Templating prompts is a way to separate the parameters from the prompt text (the "template"). The parameters can come from end user inputs or other variables in your application, like in a prompt chain.

In a poetry writing app, this may look like

```python
{
    "prompt": "Write an {{adjective}} poem about {{subject}}",
    "values": {
        "adjective": "amazing",
        "subject": "Helicone",
    }
}
```

### Benefits of using Templated Prompts with Helicone

* **Visualize** clearly all the values used in the prompts separate from the prompts.
* **Organize** all the requests made in your applications by prompts.
* **Analyze** prompt metrics, such as how expensive the template text is compared to the values and when finetuning may reduce costs.

### How to Use Templated Prompts

**Toggle Prompt Templating on**

Add the header `Helicone-Prompt-Format` (with any value) into the request to notify Helicone that you are sending a serialized prompt template with values string.

{% hint style="warning" %}
Do not include the `Helicone-Prompt-Format` header when you are not making a prompt template request.
{% endhint %}

#### **Serialize the prompt template and values**

Serialize a dictionary with two keys:

* `prompt` is a string with the template of your prompt. Any parameter should be wrapped with two curly bracked `{{param_name}}`
* `values` is a dictionary with keys for every `param_name` and values the supplied value for the parameter.

Helicone then formats the string, replacing the user parameter values with their actual values before passing the formatted prompt to OpenAI.

{% hint style="success" %}
On OpenAIs end, it's as if you just made the string-formatted request without serializing a dictionary.
{% endhint %}

Here is an example:

{% tabs %}
{% tab title="Python" %}
<pre class="language-python"><code class="lang-python">import json

template = {
    "prompt": "Write an {{adjective}} poem about {{subject}}",
    "values": {
        "adjective": "amazing",
        "subject": "Helicone",
    }
}

<strong>serialized_template = json.dumps(template)
</strong>
openai.Completion.create(
    model="text-davinci-003",
    prompt=serialized_template,
    headers={
<strong>        'Helicone-Prompt-Format': 'on',
</strong>    }
)
</code></pre>
{% endtab %}

{% tab title="Node.js" %}
<pre class="language-typescript"><code class="lang-typescript">const template = {
  prompt: 'Write an {{adjective}} poem about {{subject}}',
  values: {
    adjective: 'amazing',
    subject: 'Helicone',
  },
};

<strong>const serialized_template = JSON.stringify(template);
</strong>
openai.Completion.create({
  engine: 'text-davinci-002',
  prompt: serialized_template,
  headers: {
<strong>    'Helicone-Prompt-Format': 'on',
</strong>  },
});
</code></pre>
{% endtab %}

{% tab title="Curl" %}
<pre class="language-bash" data-overflow="wrap"><code class="lang-bash">curl https://oai.hconeai.com/v1/completions \
  -H 'Content-Type: application/json' \
  -H 'Authorization: Bearer YOUR_API_KEY' \
<strong>  -H 'Helicone-Prompt-Format: "on"' \
</strong>  -d '{
    "model": "text-davinci-003", 
<strong>    "prompt": "{\"prompt\":\"Write an {{adjective}} poem about {{subject}}\",\"values\":{\"adjective\":\"amazing\",\"subject\":\"Helicone\"}}" }'
</strong></code></pre>
{% endtab %}
{% endtabs %}

This is equivalent to sending the prompt `Write an amazing poem about Helicone` directly to OpenAI.

{% hint style="info" %}
You can use a parameter multiple times in the prompt
{% endhint %}

{% hint style="danger" %}
Make sure every prompt variable is defined in `values` and every value is present in `prompt` without any typos to avoid errors
{% endhint %}

#### (Optional) Assign a name to the prompt

You can give a name to the prompt you are using by passing in a header `Helicone-Prompt-Name` with the name of your prompt as the value. Otherwise, Helicone assigns a default name.

