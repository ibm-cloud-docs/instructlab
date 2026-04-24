---

copyright:
  years: 2025, 2026
lastupdated: "2026-04-24"

keywords: instructlab, ai, inferencing, chatting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Inferencing with Red Hat AI on {{site.data.keyword.cloud_notm}}
{: #inference}

Use inferencing to interact with foundation models and evaluate AI-powered responses for your applications. The inferencing feature provides a production-ready API that enables you to integrate conversational AI capabilities into your workflows, test model behavior, and build intelligent applications.
{: shortdesc}

This is a beta feature that is available for evaluation and testing purposes. To get access to the beta, send an email to `instructlab@ibm.com`.
{: beta}

Inferencing solves the challenge of deploying and scaling AI models by providing immediate access to foundation models through familiar, industry-standard APIs. Whether you're prototyping a chatbot, building an AI assistant, or integrating natural language understanding into your application, inferencing eliminates the complexity of model hosting and lets you focus on creating value for your users.

Currently, the supported APIs are:

* Chat Completions `/v1/chat/completions`:
  * Create: [llamastack](https://llamastack.github.io/docs/api/openai-chat-completion-v-1-chat-completions-post){: external}, [openai](https://platform.openai.com/docs/api-reference/chat/create){: external}
  * Get: [llamastack](https://llamastack.github.io/docs/api/get-chat-completion-v-1-chat-completions-completion-id-get){: external}, [openai](https://platform.openai.com/docs/api-reference/chat/get){: external}
  * List: [llamastack](https://llamastack.github.io/docs/api/list-chat-completions-v-1-chat-completions-get){: external}, [openai](https://platform.openai.com/docs/api-reference/chat/list){: external}
  * Delete: [openai](https://platform.openai.com/docs/api-reference/chat/delete){: external}
* Models `/v1/models`:
  * Get: [llamastack](https://llamastack.github.io/docs/api/get-model-v-1-models-model-id-get){: external}, [openai](https://platform.openai.com/docs/api-reference/models/retrieve){: external}
  * List: [llamastack](https://llamastack.github.io/docs/api/openai-list-models-v-1-models-get){: external}, [openai](https://platform.openai.com/docs/api-reference/models/list){: external}

## Before you begin
{: #inf-prereqs}

* Create a Pay-As-You-Go or Subscription {{site.data.keyword.cloud_notm}} account. Trial accounts are not supported. For more information or to upgrade your account, see [Account types](/docs/account?topic=account-accounts#compare).

* Create [a {{site.data.keyword.instructlab_short}} project](/docs/instructlab?topic=instructlab-project).

* Make sure you have the Writer role or greater on the {{site.data.keyword.instructlab_short}} service. For more information, see [Managing IAM access for InstructLab](/docs/instructlab?topic=instructlab-iam&interface=ui). 





## Inferencing by using the API
{: #inf-chat-api}

With the API, you can programmatically integrate AI capabilities into your applications by using industry-standard OpenAI and Llama Stack compatible endpoints. This approach is essential for production deployments where you need to automate AI interactions, handle high volumes of requests, or embed conversational AI into existing systems. The API provides the flexibility to customize model behavior, manage conversation history, and scale your AI-powered features alongside your application.

Review the following sections for examples of how to complete common inferencing tasks by using the API.

### API endpoint
{: #inf-api-endpoint}

All API requests use the following base URL format:

```text
https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference
```
{: codeblock}

Replace `{project_id}` with your project ID. To find it, go to [{{site.data.keyword.instructlab_short}} projects](/instructlab/projects), open your project, and click **Details**.

### Authenticating to the API
{: #inf-chat-auth}

Before you can make API calls, you need to authenticate your requests. You can authenticate by using either a bearer token or an {{site.data.keyword.cloud_notm}} API key.

#### Authenticating by using a bearer token
{: #inf-chat-token}

Bearer tokens ensure secure access to your project's inferencing capabilities and are generated from your {{site.data.keyword.cloud_notm}} API key. Bearer tokens expire after a set period, so they must be refreshed periodically.

The following example shows how to retrieve a bearer token.

```bash
curl -X POST "https://iam.cloud.ibm.com/identity/token" --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" --data-urlencode "grant_type=urn:ibm:params:oauth:grant-type:apikey" --data-urlencode "apikey=${IBM_CLOUD_API_KEY}"
```
{: pre}

The bearer token is the `access_token` in the response. These tokens have an expiration date and must be periodically refreshed.

```bash
{"access_token":"xxxxx","refresh_token":"not_supported","token_type":"Bearer","expires_in":3600,"expiration":1770058324,"scope":"ibm openid"}
```

#### Authenticating by using an API key
{: #inf-chat-apikey}

There are two ways to authenticate with an API key: You can [create a service ID](/docs/iam?topic=iam-serviceids&interface=ui), which is the recommended way to distribute access and controls. If you create a service ID, you need to [create a service ID API key](/docs/iam?topic=iam-serviceidapikeys&interface=ui) as well, which you use to authenticate. 

You can also authenticate by using a user API key. For more information, see [Managing user API keys](/docs/iam?topic=iam-userapikey&interface=ui).

### Generating a chat completion
{: #inf-chat-generate}

Chat completions are the core of inferencing. They allow you to send messages to a foundation model and receive AI-generated responses. This is how you build conversational experiences, get answers to questions, generate content, or process natural language inputs. You can control the conversation flow by providing system prompts that define the model's behavior and maintain message history for context-aware interactions.

The following example shows how to generate a chat completion. For a complete list of the available parameters, see [OpenAI Chat Completion](https://llamastack.github.io/docs/api/openai-chat-completion-v-1-chat-completions-post){: external}.

```bash
curl https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference/v1/chat/completions -H "Content-Type: application/json" -H "Authorization: Bearer {bearer_token}" -d '{
 "model": "granite-4-0-h-small",
 "messages": [
   {
     "role": "developer",
     "content": "You are a helpful assistant"
   },
   {
     "role": "user",
     "content": "Hello! Tell me about yourself"
   }
 ]
}' 
```
{: codeblock}
{: curl}

```python
from llama_stack_client import LlamaStackClient
client = LlamaStackClient(
  api_key="{bearer_token}",
  base_url="https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference",
)

completion = client.chat.completions.create(
  model="granite-4-0-h-small",
  messages=[
    {"role": "developer", "content": "You are a helpful assistant."},
    {"role": "user", "content": "Hello! Tell me about yourself"}
  ]
)

print(completion.choices[0].message)
```
{: codeblock}
{: python}

### Getting a chat completion by ID
{: #inf-chat-get-completion}

Retrieving a specific chat completion by ID is useful for auditing, debugging, or analyzing past interactions. 

The following example shows how to get a chat completion by its ID. For a complete list of the available parameters, see [Get Chat Completion](https://llamastack.github.io/docs/api/get-chat-completion-v-1-chat-completions-completion-id-get){: external}.

```bash
curl -L 'https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference/v1/chat/completions/{completion_id}' \
-H 'Accept: application/json' -H "Authorization: Bearer {bearer_token}"
```
{: codeblock}
{: curl}

```python
from llama_stack_client import LlamaStackClient
client = LlamaStackClient(
  api_key="{bearer_token}",
  base_url="https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference",
)

completion = client.chat.completions.retrieve(completion_id="{completion_id}")
print(completion)
```
{: codeblock}
{: python}

### Listing chat completions
{: #inf-chat-list}

Listing chat completions provides an overview of all your inferencing activity, so you can monitor usage patterns, track costs, and analyze how your application is interacting with foundation models. This is particularly valuable for understanding user behavior, identifying popular use cases, and optimizing your AI integration strategy.

The following example shows how to list chat completions. For a complete list of the available parameters, see [List Chat Completions](https://llamastack.github.io/docs/api/list-chat-completions-v-1-chat-completions-get){: external}.

```sh
curl -L 'https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference/v1/chat/completions' \
-H 'Accept: application/json' -H "Authorization: Bearer {bearer_token}"
```
{: codeblock}
{: curl}

```python
from llama_stack_client import LlamaStackClient
client = LlamaStackClient(
  api_key="{bearer_token}",
  base_url="https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference",
)

completions = client.chat.completions.list()
print(completions)
```
{: codeblock}
{: python}

### Deleting a chat completion
{: #inf-chat-delete}

Deleting chat completions helps you clean up test data and comply with privacy requirements. 

The following example shows how to delete a chat completion. For a complete list of the available parameters, see [Delete chat completion](https://platform.openai.com/docs/api-reference/chat/delete){: external}.

```bash
curl -X DELETE https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference/v1/chat/completions/{completion_id} \
-H "Content-Type: application/json" -H "Authorization: Bearer {bearer_token}"
```
{: codeblock}
{: curl}

### Listing models
{: #inf-chat-list-models}

Discover which foundation models are accessible in your project and understand their capabilities, so you can use the best model for your specific use case and optimize for factors like response quality, speed, or cost.

The following example shows how to list models. For a complete list of the available parameters, see [OpenAI List Models](https://llamastack.github.io/docs/api/openai-list-models-v-1-models-get){: external}.

```bash
curl -L 'https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference/models' \
-H 'Accept: application/json' -H "Authorization: Bearer {bearer_token}"
```
{: codeblock}
{: curl}

```python
from llama_stack_client import LlamaStackClient
client = LlamaStackClient(
  api_key="{bearer_token}",
  base_url="https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference",
)

models = client.models.list()
print(models)
```
{: codeblock}
{: python}

### Getting a model by ID
{: #inf-chat-get-model}

Retrieving detailed information about a specific model helps you understand its characteristics, capabilities, and limitations before using it in your application.

The following example shows how to get a model by ID. For a complete list of the available parameters, see [Get Model](https://llamastack.github.io/docs/api/get-model-v-1-models-model-id-get){: external}.

```bash
curl -L 'https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference/models/{model}' \
-H 'Accept: application/json' -H "Authorization: Bearer {bearer_token}"
```
{: codeblock}
{: curl}

```python
from llama_stack_client import LlamaStackClient
client = LlamaStackClient(
  api_key="{bearer_token}",
  base_url="https://us-east.instructlab.ibm.com/v1/projects/{project_id}/inference",
)

model = client.models.retrieve("{model}")  # for example, "granite-4-0-h-small"
print(model)
```
{: codeblock}
{: python}
