---

copyright:
  years: 2024, 2024
lastupdated: "2024-09-11"

keywords: instructlab, ai

subcollection: {{site.data.keyword.subcollection}}

---

{{site.data.keyword.attribute-definition-list}}


# Training models
{: #model-train}


Complete the following steps to train your model on generated data, then test the model to verify the results.

## Prerequisites
{: #model_train_cli_pre}
{: cli}

1. [Prepare your taxonomy](/docs/instructlab?topic=instructlab-getting-started#instructlab_taxonomy)
1. [Add the taxonomy TAR to your COS bucket](/docs/instructlab?topic=instructlab-getting-started#instructlab_add).
1. [Generate data from your taxonomy](/docs/instructlab?topic=instructlab-data-generate&interface=cli).


## Training a model by using the CLI
{: #model_train_cli_steps}
{: cli}


1. Get the ID for the data to use.

    ```sh
    ibmcloud ilab data list
    ```
    {: pre}

1. Run the command to start training the model with the generated data. Note the ID.

    ```sh
    ibmcloud ilab model train --name test-model --id <data_id>
    ```
    {: pre}

1. Check the details of your data generation. Include the ID for the model. The state is `queued`, then `running`. Wait for the state to be `completed`. This process could take minutes or hours.

    ```sh
    ibmcloud ilab model get --id <model_id>
    ```
    {: pre}

    When the state is `completed`, in the COS bucket, a `trained_models` directory is created with logs for troubleshooting.
