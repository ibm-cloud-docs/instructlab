---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-08"

keywords: instructlab, ai, about

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# About {{site.data.keyword.instructlab_full_notm}}
{: #about}

{{site.data.keyword.instructlab_full}} is a business-ready, private, and secure generative AI solution powered by Red Hat Enterprise Linux AI. In this product preview, selected accounts can work with their IBM account teams to optimize their Generative AI use cases for accuracy and cost efficiency. Reach out to your IBM account team for more information.

For more information, review the following links.

- [What is AI?](https://www.ibm.com/think/topics/artificial-intelligence){: external}
- [What is {{site.data.keyword.short_name}}?](https://www.redhat.com/en/topics/ai/what-is-instructlab){: external}


## Why {{site.data.keyword.instructlab_short}}?
{: #benefits}

Retain ownership of both the data and the model
:   You control your data and your model. You can choose to use them in the cloud, on-premises, or anywhere else your business requires. Leverage unique business data to unlock efficiencies and drive innovation by creating AI-powered solutions.

Minimize the risk of catastrophic forgetting
:   For higher accuracy and less risk, built-in Granite models are used as a foundation for learning new skills and knowledge. Previously learned information is not lost when the models learn new information.

Secure, up-to-date, and available
:   Because {{site.data.keyword.instructlab_short}} is available as a service on {{site.data.keyword.cloud}}, you can reduce unnecessary costs by paying just for what you need. Optimize IT expenditures by delivering simpler, faster, and more economical models.


## How does billing work?
{: #costs}

Billing begins when an {{site.data.keyword.instructlab_full}} instance is created. Costs are incurred by the usage of both {{site.data.keyword.product_name}} and the [{{site.data.keyword.cos_full}}](https://cloud.ibm.com/objectstorage/create#pricing) service, which is used as a storage location.

The cost from {{site.data.keyword.product_name}} usage is based on two metrics in measure of tokens. Tokens are units of text that is processed.

Output tokens from the Synthetic Data Generation (SDG)
:   Output tokens are calculated by the volume of generated data produced by the service from the input taxonomy. 

Input tokens to the model alignment
:   Input tokens are calculated based on the amount of data fed that into the system for model alignment training, as well as the Granite base knowledge that is used to increase accuracy without knowledge loss. Because of the foundational knowledge that is used, there is a minimum cost.

The output and input tokens are billed separately because inputs can be edited or combined.
