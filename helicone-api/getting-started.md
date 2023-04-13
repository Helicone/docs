---
description: Start using Helicone API easily and quickly
---

# Getting started

{% hint style="warning" %}
### Beta Warning

Helicone API is currently in beta and is subject to change, please stay tuned for the latest updates.
{% endhint %}

### Generate an API key

Go to [https://www.helicone.ai/keys](https://www.helicone.ai/keys) and generate a new Helicone key

![](<../.gitbook/assets/Screenshot 2023-04-13 at 2.33.11 PM.png>)



### Testing out in Playground&#x20;

Head to: [https://www.helicone.ai/api/graphql](https://www.helicone.ai/api/graphql)

<figure><img src="../.gitbook/assets/Screenshot 2023-04-13 at 2.38.51 PM.png" alt=""><figcaption><p>GraphQL Playground Image</p></figcaption></figure>

In the HTTP Headers add this block but with your API Key

```json
{
   "authorization": "Bearer <api_key>"
}
```

Here is an example request

```graphql
{
  heliconeRequest(
      limit: 1
      offset: 0
  ) {
      prompt
      properties{
        name
      }
      responseBody
      response

  }
}
```

Within the editor there is IntelliSense which is really helpful for learning what types of fields you can query. (ctrl + space)

### Python example

```python
from gql import gql, Client
from gql.transport.aiohttp import AIOHTTPTransport
url = "https://www.helicone.ai/api/graphql"
transport = AIOHTTPTransport(url=url, headers={
    "Authorization": "Bearer <HELICONE_API_KEY>"
})
client = Client(transport=transport, fetch_schema_from_transport=True)

query = gql(
    """
    query getContinents {
        heliconeRequest(
            limit: 100
            offset: 0
        ) { 
            prompt
            response
        }
    }
"""
)
result = client.execute(query)
print(result)
```

### Schema Docs

The Schema can be found on the right side of the playground

&#x20;[https://www.helicone.ai/api/graphql](https://www.helicone.ai/api/graphql)

![](../.gitbook/assets/image.png)

