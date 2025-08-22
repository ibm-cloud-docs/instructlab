---

copyright:
  years: 2025, 2025
lastupdated: "2025-08-22"

keywords: instructlab, rhel ai, faq

subcollection: instructlab

content-type: faq

---

{{site.data.keyword.attribute-definition-list}}


# FAQ for {{site.data.keyword.product_name}}
{: #faq}


Review the following FAQ for {{site.data.keyword.short_name}}. To find all FAQ for {{site.data.keyword.cloud}}, see our [FAQ library](/docs/faqs).
{: shortdesc}




## What is {{site.data.keyword.short_name}}?
{: #faq-ilab-1}
{: faq}

{{site.data.keyword.short_name}} is a private, secure generative AI solution powered by Red Hat Enterprise Linux AI, available on IBM Cloud. It allows users to retain ownership of their data and models, leverage unique business data for innovation, and minimize the risk of catastrophic forgetting.



## Why should I use {{site.data.keyword.short_name}} for my generative AI solution?
{: #faq-ilab-2}
{: faq}

{{site.data.keyword.short_name}} offers several benefits for your generative AI solution. First, it allows you to retain ownership of both the data and the model, giving you control over how your data is used and how your model performs. Second, it enables you to leverage unique business data to unlock efficiencies and drive innovation by creating AI-powered solutions. Third, it minimizes the risk of catastrophic forgetting by using built-in Granite models as a foundation for learning new skills and knowledge. Fourth, it is available as a service on IBM Cloud, allowing you to reduce unnecessary costs by paying just for what you need and optimize IT expenditures by delivering simpler, faster, and more economical models.

## What are the benefits of {{site.data.keyword.short_name}} on IBM Cloud?
{: #faq-ilab-3}
{: faq}

{{site.data.keyword.short_name}} on IBM Cloud offers several benefits, including:

Data ownership
:   Users retain ownership of both the data and the model, allowing them to control their data and model.

Leveraging unique business data
:   Users can unlock efficiencies and drive innovation by creating AI-powered solutions using their unique business data.

Minimizing the risk of catastrophic forgetting
:   {{site.data.keyword.short_name}} uses Granite models as a foundation for learning new skills and knowledge, minimizing the risk of losing previously learned information when learning new information.

Secure, up-to-date, and available
:   {{site.data.keyword.short_name}} is available as a service on IBM Cloud, allowing users to reduce unnecessary costs and optimize IT expenditures.

Data portability
:   Users can export their content and configuration to other infrastructures.

Enterprise-grade cloud infrastructure
:   {{site.data.keyword.short_name}} uses IBM Cloud's robust and secure infrastructure, designed to meet the stringent requirements of business critical workloads.

Flexibility
:   {{site.data.keyword.short_name}} offers access to a wide variety of hardware profiles, VMware compute accelerators, and the capability for new capacity expansion within the hour.

Advanced Cloud Services
:   IBM Cloud provides access to the latest GPUs and IBM watsonx services gen AI, inferencing, and machine learning to fast-track innovation into business processes.

## What are Granite models?
{: #granite}
{: faq}

Fit for purpose and open source, these enterprise-ready, multimodal models deliver exceptional performance against safety benchmarks and across a wide range of enterprise tasks from cybersecurity to RAG.

## Which Granite model does {{site.data.keyword.short_name}} use?
{: #granite-model}
{: faq}

{{site.data.keyword.short_name}} uses the `granite-3.1-8b-starter-v1` model.

## What is a taxonomy?
{: #taxonomy-faq}
{: faq}

A taxonomy is a file directory that consists of the data you feed to the model. It is organized in a cascading structure where each sub-directory, or "branch", of the taxonomy "tree" ends with a "leaf node", which is a set of files that contain the relevant data. You can contribute to a taxonomy by adding an entirely new "branch", or by adding new data to an existing `qna.yaml` file. For more information on the taxonomy structure, see [How taxonomies are structured for {{site.data.keyword.short_name}}](/docs/instructlab?topic=instructlab-taxonomy-overview&interface=ui){: external}. You can also view the [InstructLab taxonomy on GitHub](https://github.com/IBM-Cloud/redhat-ai-instructlab-taxonomy){: external}.


## How does taxonomy validation work?
{: #faq-tax-validation}
{: faq}

When you upload a taxonomy to {{site.data.keyword.short_name}}, the checks are performed: 
- Validating the formatting and syntax of your `qna.yaml` files by using the `ilab diff` command.
- Attempting to clone the knowledge and skills documents that are referenced in your `qna.yaml` files.
- Checking that you have the correct service authorizations in place, such as for {{site.data.keyword.cos_short}} and {{site.data.keyword.secrets-manager_short}}.


## How does billing work?
{: #costs-faq}
{: faq}

Costs are incurred by the usage of both {{site.data.keyword.product_name}} and the [{{site.data.keyword.cos_full}}](https://cloud.ibm.com/objectstorage/create#pricing) service, which is used as a storage location.

If you choose to deploy the model on another service, additional charges can come from that service as well.


## How is cost calculated in {{site.data.keyword.product_name}}?
{: #costs-ilab}
{: faq}

The cost from {{site.data.keyword.product_name}} usage is based on two metrics that are measured in tokens. Each token corresponds to a specific amount of computational power that is required for the processing tasks. The total number of tokens consumed directly influences the scale of data generation or model fine-tuning. This metric serves as a basis for our billing system, enabling users to monitor and control their costs according to the computational resources utilized. The tokens that are processed for Synthetic Data Generation (SDG) and Model Alignment are billed separately.

Synthetic Data Generation (SDG)
:   Output tokens (`SYN-DATA-TOKEN`) are calculated by the volume of generated data produced by the service from the entire input taxonomy. The text is tokenized by using [Hugging Face's tokenizer library](https://huggingface.co/docs/transformers/en/main_classes/tokenizer) with the tokenization information for the [Mistral teacher model](https://huggingface.co/docs/transformers/main/en/model_doc/mistral#mistral). 

Model alignment training
:   Input tokens (`MODEL-TRAIN-TOKEN`) are calculated based on the amount of data fed that into the system for model alignment training, as well as the Granite base knowledge that is used to increase accuracy without knowledge loss. Because of the foundational knowledge that is used, there is a minimum cost.




## How do I find and track cost information as I go?
{: #costs-tracking}
{: faq}

1. Before you begin running anything in {{site.data.keyword.instructlab_short}}, you can use the [cost estimator](https://cloud.ibm.com/estimator) to get an estimate of what the cost might be.

1. When you upload your taxonomy, look for the cost estimate based on data tokens. Then run the [data generation](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-data-generate) job.

1. After the data generation completes, but before you begin the training, look for the estimated amount of tokens for the training costs. Then, [begin training](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-model-train).


## Are failed operations billed?
{: #costs-operations}
{: faq}

Failed operations are not billed. Successful operations and user canceled operations are billed, though user canceled operations are prorated based on the processing that completed.


## What is data generation?
{: #faq-data-gen}
{: faq}

Data generation is the process of generating questions and answers based on the questions and answers that you included in the QNA files.


## What is model training?
{: #faq-model-train}
{: faq}

Training is the process of learning the questions and answers. The training begins with knowledge and foundational skills, then moves on to compositional skills.




## How long does it take to run?
{: #faq-time}
{: faq}

Data generation and model training both take significant time to complete. You can find general estimates in the console when you start the processes.

Factors that impact completion time:
- The contents of the knowledge documents
- The number of other jobs in the queue

## How long does data generation take?
{: #faq-time-data}
{: faq}

After queuing, data generation usually takes 2-6 hours to run. For an estimate, the general formula is to take the number of output tokens, divided by about 5000 tokens per second, divided by 60 seconds per minute, and divided by 60 minutes in an hour.

```txt
Tokens / 5000 / 60 / 60 = Number of hours
```
{: codeblock}


## How long does model training take?
{: #faq-model}
{: faq}

For model training, the general formula is to take the number of output tokens, divided by about 4000 tokens per second, divided by 60 seconds per minute, and divided by 60 minutes in an hour.

```txt
Tokens / 4000 / 60 / 60 = Number of hours
```
{: codeblock}


## Can I import my own training data?
{: #faq-byo-sdg}

Yes, you can import your own training data. Importing your own training data is beneficial for a variety of use cases and can help you optimize performance and efficiency across hybrid environments.

- Training models to your specific needs and maintain control over your data sources, whether that's on-premises or in {{site.data.keyword.cloud_notm}}.
- Generating data in smaller, manageable chunks, so that you can avoid timeouts or system limits. You can later combine these smaller data sets into a single data set for training.
- Combining previously generated training data with new data, so that you can iteratively retrain models with both existing and newly acquired knowledge.

Other use cases:

{{_include-segments/byo-sdg-use-cases.md}}
