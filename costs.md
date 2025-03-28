---

copyright:
  years: 2025, 2025
lastupdated: "2025-03-28"

keywords: instructlab, ai, about, pricing, costs

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Understanding costs
{: #costs}

Billing begins when an {{site.data.keyword.instructlab_full}} instance is created. Costs are incurred by the usage of both {{site.data.keyword.product_name}} and the [{{site.data.keyword.cos_full}}](https://cloud.ibm.com/objectstorage/create#pricing) service, which is used as a storage location.

The cost from {{site.data.keyword.product_name}} usage is based on two metrics in measure of tokens. Tokens are units of text that is processed.

Output tokens from the Synthetic Data Generation (SDG)
:   Output tokens are calculated by the volume of generated data produced by the service from the input taxonomy. 

Input tokens to the model alignment
:   Input tokens are calculated based on the amount of data fed that into the system for model alignment training, as well as the Granite base knowledge that is used to increase accuracy without knowledge loss. Because of the foundational knowledge that is used, there is a minimum cost.

The output and input tokens are billed separately because inputs can be edited or combined.

