---

copyright:
  years: 2024, 2024
lastupdated: "2024-07-19"

keywords: instructlab, ai, data, generate

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Generating data from a taxonomy
{: #data-generate}


Complete the following steps to generate synthetic data from your taxonomy.


## Prerequisites
{: #data_generate_cli_pre}
{: cli}

1. [Install the `ilab` CLI plug-in](/docs/instructlab?topic=instructlab-getting-started#instructlab_cli_install).
1. [Prepare your taxonomy](/docs/instructlab?topic=instructlab-getting-started#instructlab_taxonomy).
1. [Upload the taxonomy TAR to your COS bucket](/docs/instructlab?topic=instructlab-getting-started#instructlab_upload).



## Generating synthetic data by using the CLI
{: #data_generate_cli_steps}
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



1. Run the `ibmcloud ilab data generate` command to generate synthetic data from your taxonomy.
    ```sh
    ibmcloud ilab data generate [--name NAME] [--taxonomy-id TAXONOMY-ID]
    ```
    {: pre}

    Example command.
    ```sh
    ibmcloud ilab data generate --name data-1 --taxonomy-id 669a88c9488ee7b95ce8fe05
    ```
    {: pre}

    Example output.
    ```sh
    id            669a88ed1d4d7e655bb537f1
    name          test-data
    state         queued
    status
    created_at    2024-07-19T15:40:29.000Z
    taxonomy_id   669a88c9488ee7b95ce8fe05
    ```
    {: screen}


1. Check the status of your data generation.
    ```sh
    ibmcloud ilab data status --id ID
    ```
    {: pre}

    Example command.
    ```sh
    ibmcloud ilab data status --id 669a88ed1d4d7e655bb537f1
    ```
    {: pre}

    Example output.
    ```txt
    id            669a88ed1d4d7e655bb537f1
    name          test-data
    state         running
    status        Generating synthetic data for taxonomy path compositional_skills->STEM->math->area: 12% 12/100 (total qna processed 1/147)
    created_at    2024-07-19T15:40:29.000Z
    taxonomy_id   669a88c9488ee7b95ce8fe05
    ```
    {: screen}



## Next steps
{: #data_generate_next}

After you've generated synthetic data from your taxonomy, you can begin [training your model](/docs/instructlab?topic=instructlab-model-train).

