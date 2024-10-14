---

copyright:
  years: 2024, 2024
lastupdated: "2024-10-14"

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

1. [Install the `ilab` CLI plug-in](/docs/instructlab?topic=instructlab-getting-started&interface=cli#cli-install).{: cli}
1. [Prepare your taxonomy](/docs/instructlab?topic=instructlab-getting-started#taxonomy).
1. [Add the taxonomy TAR to your COS bucket](/docs/instructlab?topic=instructlab-getting-started#taxonomy-add-ui).


## Generating data by using the console
{: #data-generate-ui}
{: ui}

1. In the console, open the [InstructLab service](https://cloud.ibm.com/instructlab/overview).

1. Click **Training data** > **Generate**.

1. Provide an alphanumeric name for the training data, select the taxonomy to use, and click **Generate**. The state is `queued`, then `running`. Wait for the state to be `completed`. When the data is generated, in the COS bucket, a `synthetic_data` directory is created with logs for troubleshooting.


## Generating data by using the CLI
{: #data-generate-cli}
{: cli}

1. List your taxonomies and make a note of the taxonomy you want to use.
    ```sh
    ibmcloud ilab taxonomy list
    ```
    {: pre}

    Example output.
    ```txt
    id                         name       taxonomy_path
    669a88c9488ee7b95ce8fe05   test-tax   taxonomy.tar.gz
    ```
    {: screen}

1. Generate data from your taxonomy. Note the ID for the data to use in the next step. Use alphanumeric characters in the name.
    ```sh
    ibmcloud ilab data generate [--name NAME] [--taxonomy-id TAXONOMY-ID]
    ```
    {: pre}

    Example command.
    ```sh
    ibmcloud ilab data generate --name testdata --taxonomy-id 669a88c9488ee7b95ce8fe05
    ```
    {: pre}

    Example output.
    ```sh
    id            66a268c170dcb21150050e8e
    name          test-data
    state         queued
    status
    created_at    2024-07-19T15:40:29.000Z
    taxonomy_id   669a88c9488ee7b95ce8fe05
    ```
    {: screen}

1. Check the details of your data generation. Include the ID for the data. The state is `queued`, then `running`. Wait for the state to be `completed`.
    ```sh
    ibmcloud ilab data get --id DATA_ID
    ```
    {: pre}

    Example command.
    ```sh
    ibmcloud ilab data get --id 66a268c170dcb21150050e8e
    ```
    {: pre}

    Example output.
    ```txt
    id            66a268c170dcb21150050e8e
    name          test-data
    state         running
    status        Generating data for taxonomy path compositional_skills->STEM->math->area: 12% 12/100 (total qna processed 1/147)
    created_at    2024-07-19T15:40:29.000Z
    taxonomy_id   669a88c9488ee7b95ce8fe05
    ```
    {: screen}

    When the state is `completed`, in the COS bucket, a `synthetic_data` directory is created with logs for troubleshooting.


## Next steps
{: #next}

After you've generated data from your taxonomy, you can begin [training your model](/docs/instructlab?topic=instructlab-model-train).
