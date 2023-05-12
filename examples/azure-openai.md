# Azure-OpenAI

You can use Helicone just like you would use the OpenAI package for your Azure-OpenAI deployment, and it requires no additional code changes beyond using the OpenAI package with Helicone.

<pre class="language-python"><code class="lang-python"><strong>from helicone import openai
</strong>
openai.api_type = "azure"
openai.api_base = "https://[YOUR_AZURE_DOMAIN].openai.azure.com"
openai.api_version = "2023-03-15-preview"
openai.api_key = YOUR_AZURE_API_KEY

response = openai.ChatCompletion.create(
    engine = 'gpt-35-turbo',
    messages = [{
        'role': 'user',
        'content': "Hello World!"
    }],
    max_tokens=15,
)
</code></pre>
