---

copyright:
  years: 2024, 2024
lastupdated: "2024-11-22"

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

1. In the console, open the [{{site.data.keyword.instructlab_short}} service](https://cloud.ibm.com/instructlab/overview).

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

    Example `data get` command.
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

    Example `data get` command with the `--output json` option which includes metrics.
    ```sh
    ibmcloud ilab data get --id 66a268c170dcb21150050e8e --output json
    ```
    {: pre}

    Example JSON output
    ```json
        {                                                                                                                 
      "created_at": "2024-07-19T15:40:29.000Z",                                                                       
      "data_metrics": {                                                                                               
        "samples": {                                                                                                  
          "knowledge": 30,                                                                                            
          "skills": 70,                                                                                               
          "total": 100                                                                                                
        }                                                                                                             
      },                                                                                                              
      "id": "66a268c170dcb21150050e8e",                                                                   
      "name": "test-data",                                                                                                 
      "state": "completed",                                                                                           
      "status": "completed",                                                                                          
      "taxonomy_id": "669a88c9488ee7b95ce8fe05"                                                           
    }
    ```
    {: screen}


When the state is `completed`, in the COS bucket, a [`synthetic_data` directory](#data-bucket) is created with logs for troubleshooting.

## What's in my COS bucket after generating data?
{: #data-bucket}

After you generate data, your COS bucket contains a `synthetic_data` directory with the following files. 

Artifacts
:   These files contain the samples on each leaf node. These are not used for training the model, but are provided for readability and can be used to see if a QNA is generating the expected number of samples. 

Logs
:   These files contain the {{site.data.keyword.instructlab_short}} execution logs and system details. 

`knowledge_train_msgs.jsonl` and `skills_train_msgs.jsonl`
:   These are the Phase 1 and Phase 2 training files and contain samples used for training the model. 




## Next steps
{: #next-data}

After you've generated data from your taxonomy, you can begin [training your model](/docs/instructlab?topic=instructlab-model-train).