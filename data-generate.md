---

copyright:
  years: 2024, 2025
lastupdated: "2025-10-20"

keywords: instructlab, ai, data, generate

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Generating data from a taxonomy for {{site.data.keyword.short_name}}
{: #data-generate}


Data generation is the process of automatically generating synthetic questions and answers based on the questions and answers that you included in the QNA files. The process {{site.data.keyword.instructlab_short}} uses to generate data focuses on content quality and relevance. 

[Learn more about the data generation process from Red Hat.](https://www.redhat.com/en/blog/how-instructlabs-synthetic-data-generation-enhances-llms)


## Prerequisites
{: #data-generate-pre}

1. [Install the `ilab` CLI plug-in](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-cli-install).{: cli}
1. [Prepare your taxonomy](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-getting-started#taxonomy).
1. [Add the taxonomy tar.gz to your {{site.data.keyword.cos_short}} bucket](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-getting-started#taxonomy-add-ui).


## Generating data by using the console
{: #data-generate-ui}
{: ui}

1. In the console, open the [{{site.data.keyword.instructlab_short}} service](https://cloud.ibm.com/instructlab/overview).

1. Click **{{site.data.keyword.short_name}} Projects** > your project > **Training data** > **Generate**.

1. Enter an alphanumeric name for the training data and select the taxonomy to use.

1. Optional: Review the estimated cost that is provided before you start the data generation process.

1. Click **Generate**. The state is `queued`, then `running`.

1. Wait for the state to be `completed`. When the data generation is completed, a `synthetic_data` directory that contains log files is created {{site.data.keyword.cos_short}} bucket. You can review these logs for troubleshooting or verification.

## Importing your own training data in the console
{: #data-generate-byo-ui}
{: ui}

You can import your own previously generated data to supplement data generation in {{site.data.keyword.short_name}}. You might want to import your own data if you need to do one or more of the following.

{{_include-segments/byo-sdg-use-cases.md}}

To import your own data, you can reference previous data generation runs, import files from your {{site.data.keyword.cos_short}} bucket, or upload files from your local machine.

Complete the following steps to import your own training data.

1. In the console, open the [{{site.data.keyword.instructlab_short}} service](https://cloud.ibm.com/instructlab/overview).

1. Click **{{site.data.keyword.short_name}} Projects** > your project > **Training data** > **Import**.

1. Enter an alphanumeric name for your data.

1. Select one of the following options.

    - **Object Storage**: Select existing files in your Object Storage bucket.

        1. Select the instance and bucket where your existing data is stored.
        1. Click **Next**.
        1. Select the files that you want to import.

    - **Upload Files**:  Select files from your local machine. Note that there is a 40 Mb limit for uploading files.
        
        1. Select an {{site.data.keyword.cos_short}} instance and bucket or create a new instance and bucket to store your data.
        1. Grant {{site.data.keyword.short_name}} Writer permissions for the bucket.
        1. **Optional**: Storage settings. Specify the following additional details for how to store your data.
            - Bucket file path.
            - Directory within the bucket.
            - Object Storage instance name.
            - Resource group.
            - Object Storage bucket name.
            - Bucket resiliency.
        1. Click **Next**.
        1. Select the knowledge and skills files that you want to upload from your local machine.

1. Click **Import**.

## Merging training data in the console
{: #data-generate-byo-train-ui}
{: ui}

You might generate data in smaller, manageable chunks, so that you can avoid timeouts or system limits. You can then merge these smaller data sets into a single data set for training.

Complete the following steps to merge data in the console.

1. In the console, open the [{{site.data.keyword.instructlab_short}} service](https://cloud.ibm.com/instructlab/overview).

1. Click **{{site.data.keyword.short_name}} Projects** > your project > **Training data**.

1. Select up to 20 of your training data entries from the list and click **Merge**.

1. Enter an alphanumeric name for your data.

1. Select the {{site.data.keyword.cos_short}} instance and bucket where you want to store the merged data.

1. Click **Create**.

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

1. Check the details of your data generation. Include the ID for the data. The state is `queued`, then `running`. Wait for the state to be `completed`. When the state is `completed`, in the {{site.data.keyword.cos_short}} bucket, a [`synthetic_data` directory](#data-bucket) is created with logs for troubleshooting.
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

1. Optional: When the state is `completed`, you can review metrics, such as [token estimates to calculate the estimated cost](/docs/instructlab?topic=instructlab-faq#costs-ilab).

    Example `data get` command with the `--output json` option
    ```sh
    ibmcloud ilab data get --id 66a268c170dcb21150050e8e --output json
    ```
    {: pre}

    Example JSON output
    ```json
    {
      "created_at": "2025-10-20T15:40:29.000Z",
      "data_metrics": {
        "samples": {
          "knowledge": 30, 
          "skills": 70,
          "total": 100
        },
        "tokens": {
          "data_leaf_nodes": {
            "compositional_<taxonomy_path>": 26196,
            "knowledge_<taxonomy_path>": 1228930,
            },
          "data_tokens_total": 5993486,
          "training_estimated": 411435913,
          "training_phases": {
            "phase_1_knowledge": 1389992,
            "phase_2_skills": 410045921
            }
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


## Importing your own training data by using the CLI
{: #data-generate-byo-cli}
{: cli}

You might want to import your own data for one or more of the following reasons.

{{_include-segments/byo-sdg-use-cases.md}}

You can import your own training data to supplement data generation in {{site.data.keyword.short_name}}. To import your own previously generated data, specify one or more of the following:
- The data generation IDs of previous runs.
- An {{site.data.keyword.cos_short}} bucket that contains `.json` or `.jsonl` knowledge and skills files.

Complete the following steps to import your data.

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

1. If you have previously generated data that you want to use, list your data and make a note of the UUIDs you want to use. You can include up to 20 data sources.
    ```sh
    ibmcloud ilab data list
    ```
    {: pre}

1. [Generate data from your taxonomy](/docs/instructlab?topic=instructlab-ilab-cli&interface=cli#ilab-cli-data-generate-command). Note the ID for the data to use in the next step. Use alphanumeric characters in the name.
    ```sh
    ibmcloud ilab data generate [--name NAME] [--taxonomy-id TAXONOMY-ID] [--internal-ids INTERNAL-IDs]
    ```
    {: pre}

    Example command to include multiple internal IDs (data sources) for data generation.
    ```sh
    ibmcloud ilab data generate --name testdata --taxonomy-id 65005b67-7de4-4216-b23c-ed4342f99c88 --internal-ids 8c6b9224-a4f1-4649-907c-0f11d14cfc59,299ee20c-0b04-4d8e-ad12-a3d98feece40 
    ```
    {: pre}

For more examples, see the next section: [Example commands for importing your own training data](/docs/instructlab?topic=instructlab-data-generate&interface=cli#data-generate-byo-cli-examples).

### Example commands for importing your own training data
{: #data-generate-byo-cli-examples}
{: cli}

Review the following example commands for importing your own training data or adding knowledge and skills files to a data generation job.

Example command to include multiple internal IDs.
```sh
ibmcloud ilab data generate --name testdata --taxonomy-id 65005b67-7de4-4216-b23c-ed4342f99c88 --internal-ids 8c6b9224-a4f1-4649-907c-0f11d14cfc59,299ee20c-0b04-4d8e-ad12-a3d98feece40
```
{: pre}

Example command to combine multiple previously generated data sources (internal IDs) as well as `.jsonl` or `.json` files from an {{site.data.keyword.cos_short}} bucket.

```sh
ibmcloud ilab data generate \
  --name testdata \
  --taxonomy-id 669a88c9488ee7b95ce8fe05 \
  --internal-ids 8c6b9224-a4f1-4649-907c-0f11d14cfc59,299ee20c-0b04-4d8e-ad12-a3d98feece40 \
  --knowledge-paths PATH \
  --skills-paths PATH \
  --skills-knowledge-cos-bucket STRING \
  --skills-knowledge-cos-bucket-endpoint ENDPOINT
```
{: pre}

Example command to combine previously generated data with `.json` or `.jsonl` knowledge and skills files stored in an {{site.data.keyword.cos_short}} bucket. You can also optionally specify an output {{site.data.keyword.cos_short}} bucket to store the generated data (SDG) output.

```sh
ibmcloud ilab data generate \
  --name testdata \
  --taxonomy-id 669a88c9488ee7b95ce8fe05 \
  --internal-ids 8c6b9224-a4f1-4649-907c-0f11d14cfc59 \
  --knowledge-paths PATH \
  --skills-paths PATH \
  --skills-knowledge-cos-bucket STRING \ 
  --skills-knowledge-cos-bucket-endpoint ENDPOINT
  --output-cos-bucket-string STRING \
  --output-cos-bucket-endpoint ENDPOINT
  
```
{: pre}


Example command to merge data by specifying their internal IDs.
```sh
ibmcloud ilab data generate \
  --name testdata \
  --internal-ids 8c6b9224-a4f1-4649-907c-0f11d14cfc59,299ee20c-0b04-4d8e-ad12-a3d98feece40 \
  --output-cos-bucket-string STRING \
  --output-cos-bucket-endpoint ENDPOINT
```
{: pre}

Example command to merge previously generated data by specifying their internal IDs as well as include skills and knowledge from an {{site.data.keyword.cos_short}} bucket.

```sh
ibmcloud ilab data generate \
  --name testdata \
  --internal-ids 8c6b9224-a4f1-4649-907c-0f11d14cfc59 \
  --knowledge-paths PATH \
  --skills-paths PATH \
  --skills-knowledge-cos-bucket STRING \ 
  --skills-knowledge-cos-bucket-endpoint ENDPOINT
  --output-cos-bucket-string STRING \
  --output-cos-bucket-endpoint ENDPOINT
```
{: pre}

Example command to merge skills and knowledge from an {{site.data.keyword.cos_short}} bucket.

```sh
ibmcloud ilab data generate \
  --name testdata \
  --knowledge-paths PATH \
  --skills-paths PATH \
  --skills-knowledge-cos-bucket STRING \ 
  --skills-knowledge-cos-bucket-endpoint ENDPOINT
  --output-cos-bucket-string STRING \
  --output-cos-bucket-endpoint ENDPOINT
```
{: pre}


## Generating data by using the API
{: #data-generate-api}
{: api}

1. List your taxonomies and make a note of the taxonomy you want to use.

    Example command.
    ```sh
    curl -X 'GET' \
    'https://us-east.instructlab.ibm.com/v1/taxonomies' \
    -H 'accept: application/json
    ```
    {: pre}

    Example output.
    ```txt
    {
      "taxonomies": [
        {
          "id": "202a03c4-dcf1-432a-82b7-abecb2e019f7",
          "name": "example-taxonomy-name-1",
          "taxonomy_path_cos": "taxonomies/taxonomy.tar.gz",
          "created_at": "2024-10-23T02:58:50.000Z"
        }
      ]
    }
    ```
    {: screen}

1. Generate data from your taxonomy. Note the ID for the data to use in the next step. Use alphanumeric characters in the name.

    Example command.
    ```sh
    curl -X 'POST' \
      'https://us-east.instructlab.ibm.com/v1/data' \
      -H 'accept: application/json' \
      -H 'Content-Type: application/json' \
      -d '{
      "name": "example-data-1",
      "taxonomy_id": "202a03c4-dcf1-432a-82b7-abecb2e019f7"
    }'
    ```
    {: pre}

    Example output.
    ```sh
    {
      "id": "add785e6-a8c3-4f5f-ab89-c506a3f115da",
      "name": "example-data-1",
      "state": "",
      "status": "queued",
      "created_at": "2024-10-23T02:58:50.000Z",
      "taxonomy_id": "202a03c4-dcf1-432a-82b7-abecb2e019f7",
      "data_metrics": {
        "samples": {
          "additionalProp1": 1,
          "additionalProp2": 2,
          "additionalProp3": 3
        }
      }
    }
    ```
    {: screen}

1. Check the details of your data generation. Include the ID for the data. The state is `queued`, then `running`. Wait for the state to be `completed`.

    Example command.
    ```sh
    curl -X 'GET' \
      'https://us-east.instructlab.ibm.com/v1/data/add785e6-a8c3-4f5f-ab89-c506a3f115da' \
      -H 'accept: application/json'
    ```
    {: pre}

    Example output.
    ```txt
    {
      "id": "add785e6-a8c3-4f5f-ab89-c506a3f115da",
      "name": "example-data-1",
      "state": "",
      "status": "queued",
      "created_at": "2024-10-23T02:58:50.000Z",
      "taxonomy_id": "202a03c4-dcf1-432a-82b7-abecb2e019f7",
      "data_metrics": {
        "samples": {
          "additionalProp1": 1,
          "additionalProp2": 2,
          "additionalProp3": 3
        }
      }
    }
    ```
    {: screen}

When the state is `completed`, in the {{site.data.keyword.cos_short}} bucket, a [`synthetic_data` directory](#data-bucket) is created with logs for troubleshooting.
   

## What's in my {{site.data.keyword.cos_short}} bucket after generating data?
{: #data-bucket}

After you generate data, your {{site.data.keyword.cos_short}} bucket contains a `synthetic_data` directory with the following files. 

`Artifacts`
:   These files contain the samples on each leaf node. These are not used for training the model, but are provided for readability and can be used to see if a QNA is generating the expected number of samples. 

`Logs`
:   These files contain the {{site.data.keyword.instructlab_short}} execution logs and system details. 

`knowledge_train_msgs.jsonl` and `skills_train_msgs.jsonl`
:   These are the Phase 1 and Phase 2 training files and contain samples used for training the model. 

To understand why and how your data gets generated, see the [SDG FAQs](https://github.com/instructlab/sdg/blob/main/docs/FAQ.md){: external} community doc.


## Next steps
{: #next-data}

After you've generated data from your taxonomy, you can begin [training your model](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-model-train).
