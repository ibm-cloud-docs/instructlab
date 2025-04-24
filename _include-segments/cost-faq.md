## How does billing work?
{: #costs}
{: faq}

Costs are incurred by the usage of both {{site.data.keyword.product_name}} and the [{{site.data.keyword.cos_full}}](https://cloud.ibm.com/objectstorage/create#pricing) service, which is used as a storage location.


## How is cost calculated in {{site.data.keyword.product_name}}?
{: #costs-ilab}
{: faq}

The cost from {{site.data.keyword.product_name}} usage is based on two metrics that are measured in tokens. Each token corresponds to a specific amount of computational power that is required for the processing tasks. The total number of tokens consumed directly influences the scale of data generation or model fine-tuning. This metric serves as a basis for our billing system, enabling users to monitor and control their costs according to the computational resources utilized. The tokens that are processed for Synthetic Data Generation (SDG) and Model Alignment are billed separately.

Synthetic Data Generation (SDG)
:   Output tokens (`SYN-DATA-TOKEN`) are calculated by the volume of generated data produced by the service from the entire input taxonomy. The text is tokenized by using [Huggingface's tokenizer library](https://huggingface.co/docs/transformers/en/main_classes/tokenizer) with the tokenization information for the [Mistral teacher model](https://huggingface.co/docs/transformers/main/en/model_doc/mistral#mistral). 

Model alignment training
:   Input tokens (`MODEL-TRAIN-TOKEN`) are calculated based on the amount of data fed that into the system for model alignment training, as well as the Granite base knowledge that is used to increase accuracy without knowledge loss. Because of the foundational knowledge that is used, there is a minimum cost.




## How do I find and track cost information as I go?
{: #costs-tracking}
{: faq}

1. Before you begin running anything in {{site.data.keyword.instructlab_short}}, you can use the [cost estimator](https://cloud.ibm.com/estimator) to get an estimate of what the cost might be.

1. When you upload your taxonomy, look for the cost estimate based on synthetic data tokens. Then run the [data generation](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-data-generate) job.

1. After the synthetic data generation completes, but before you begin the training, look for the estimated amount of tokens for the training costs. Then, [begin training](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-model-train).


## Are failed operations billed?
{: #costs-operations}
{: faq}

Failed operations are not billed. Successful operations and user canceled operations are billed, though user canceled operations are prorated based on the processing that completed.
