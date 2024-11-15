---

copyright:
  years: 2024, 2024
lastupdated: "2024-11-15"

keywords: instructlab, ai, data, generate

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Generating data from a taxonomy
{: #data-generate}


Complete the following steps to generate data from your taxonomy.

Data cannot augmented, curated, or manually uploaded to train the model. Use this task to generate the data.
{: restriction}


## Prerequisites
{: #data-generate-pre}


1. [Prepare your taxonomy](/docs/instructlab?topic=instructlab-getting-started#taxonomy).
1. [Add the taxonomy TAR to your COS bucket](/docs/instructlab?topic=instructlab-getting-started#taxonomy-add-ui).


## Generating data by using the console
{: #data-generate-ui}
{: ui}

1. In the console, open the [{{site.data.keyword.instructlab_short}} service](https://cloud.ibm.com/instructlab/overview).

1. Click **Training data** > **Generate**.

1. Provide an alphanumeric name for the training data, select the taxonomy to use, and click **Generate**. The state is `queued`, then `running`. Wait for the state to be `completed`. When the data is generated, in the COS bucket, a `synthetic_data` directory is created with logs for troubleshooting.



## Next steps
{: #next-data}

After you've generated data from your taxonomy, you can begin [training your model](/docs/instructlab?topic=instructlab-model-train).
