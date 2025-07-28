---

copyright:
  years: 2024, 2025
lastupdated: "2025-07-28"

keywords: instructlab, ai

subcollection: instructlab

content-type: tutorial

services: {{site.data.keyword.subcollection}}
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with {{site.data.keyword.instructlab_full_notm}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-services="{{site.data.keyword.subcollection}}"}
{: toc-completion-time="30m"}

Get ready to dive into [AI](#x3448902){: term} with {{site.data.keyword.instructlab_full}}!
{: shortdesc}

{{site.data.keyword.short_name}} is an open source project created by IBM and Red Hat to be a cost-effective entry point into the world of [machine learning](#x8397498){: term}.


## Get familiar with the concepts
{: #get-familiar}

To use {{site.data.keyword.short_name}}, you don't need to have any preexisting knowledge. You don't even need to have an idea for what to create yet. Let's start by just getting familiar with the concepts and what kinds of things you can do with the technology.

With {{site.data.keyword.short_name}}, you can use an existing, pre-trained LLM compiled by a community of contributors, then contribute your own knowledge and skills, in what's known as a **taxonomy** to further train the model.

When you use {{site.data.keyword.short_name}} in {{site.data.keyword.cloud}}, you begin by uploading your taxonomy, which is the knowledge and skills you want to add to an LLM, to {{site.data.keyword.cos_short}}. You can then use {{site.data.keyword.short_name}} to further train the model by using your taxonomy data.

![Task flow diagram for generating a model with the service.](images/task-flow.svg "Task flow diagram for generating a model with the service."){: caption="Task flow diagram." caption-side="bottom"}{: external download="task-flow.svg"}

For more information, see the following resources.
- [What is InstructLab?](https://www.redhat.com/en/topics/ai/what-is-instructlab){: external}.
- [InstructLab](https://www.ibm.com/think/topics/instructlab?mhsrc=ibmsearch_a&mhq=instructlab){: external}.

## Set up your {{site.data.keyword.cloud}} account
{: #instructlab-pre}

Make sure you have the following before continuing.

* A **Pay-As-You-Go** or **Subscription** {{site.data.keyword.cloud}} account. Trial accounts are not supported. For more information or to upgrade the account, see [Account types](/docs/account?topic=account-accounts#compare).

* [An {{site.data.keyword.short_name}} project](/docs/instructlab?topic=instructlab-project).

* [Access to {{site.data.keyword.short_name}} and {{site.data.keyword.cos_short}}](/docs/instructlab?topic=instructlab-iam).

* **Optional**: If you are using a private repo to store your taxonomy knowledge documents, create [a {{site.data.keyword.secrets-manager_short}} instance](https://cloud.ibm.com/catalog/services/secrets-manager){: external}.

* [Install the CLI](/docs/instructlab?topic=instructlab-cli-install).{: cli}


## Optional: Prepare a taxonomy
{: #taxonomy}

1. Fork the IBM Cloud taxonomy or create your own.
    - If you don't already have a taxonomy, you can fork the [IBM Cloud taxonomy repo](https://github.com/IBM-Cloud/redhat-ai-instructlab-taxonomy){: external} and clone it to your local machine. This is an empty taxonomy with the correct file structure already created for you. You can add knowledge and skills in the corresponding directories.

    - To create your own taxonomy instead, see [Preparing taxonomies](/docs/instructlab?topic=instructlab-taxonomy-prep&interface=ui) for more information.

    You can also use the IBM Cloud community Jupyter notebook to create your taxonomy. For more information, see [redhat-ai-instructlab-jupyter-notebooks GitHub repo](https://github.com/IBM-Cloud/redhat-ai-instructlab-jupyter-notebooks/tree/main){: external}
    {: tip}

1. Make updates to your taxonomy. The following example adds rhyming questions to the linguistics directory.

    a. In your fork, in the `compositional_skills/linguistics` directory, create a `qna.yaml` file.

    b. In the `qna.yml` file, add a question related to rhyming words.
    ```yaml
    - answer: 'Here are two rhyming words for "cave":
        1\. Brave

        2\. Gave'
      question: 'Give me two words that rhyme with cave'
    ```
    {: codeblock}

    c. If your additions include reference documents, such as web articles or files in Github, you can reference the GitHub commit ID and SHA of the file like in [this example](https://docs.instructlab.ai/taxonomy/knowledge/file_structure/#example-of-a-knowledge-submission), you can use public `github.com` repositories. 

    ```txt
    document:
    repo: https://github.com/<organization>/<repository>
    commit: <commit_sha>
    patterns:
        - <filename>.md
    ```
    {: codeblock}

    d. Save the changes and push the changes to the fork.

    f. Optional: [Validate the updated taxonomy](/docs/instructlab?topic=instructlab-ts-debug#version).

1. In a browser, open the **Releases** page for your Github repository. For example: `https://github.com/<my-org>/taxonomy/releases`.

1. Click **Create a release**.

1. Create a tag, select a target branch, and enter a name for the release.

1. Click **Publish a release**.

1. Download the packaged `tar.gz` file that was automatically generated from the release by clicking **Source code (tar.gz)**.

1. **Optional**: If you are using a private repository for your taxonomy knowledge documents, complete the following steps.

    1. Follow the GitHub documentation to [create a classic personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens) (PAT).

    1. In the **Repository access** section, scope your PAT to your taxonomy repo.
    
    1. In the **Repository permissions** section, select **Contents** > `read-only` and **Metadata** > `read-only`.


## Upload your taxonomy by using the console
{: #taxonomy-add-ui}
{: ui}

Complete the following steps to store your taxonomy in {{site.data.keyword.cos_short}}.

1. From the **Projects** [page](https://cloud.ibm.com/instructlab/projects){: external}, select your project.

1. Click **Taxonomies**.
    
1. Click **Upload** and enter the following details.

    Taxonomy file
    :   Select your `.tar.gz` file.
    
    Taxonomy name
    :   Give the taxonomy an alphanumeric name.

    Private repository access
    :   Enable this option if your taxonomy knowledge documents are in a private repo.
    :   **{{site.data.keyword.secrets-manager_short}} service instance**: Select an existing instance or create one.
    :   **{{site.data.keyword.secrets-manager_short}} secret**: Select an existing secret or create one. If you are creating a secret, select the **Key-value** secret type and add your personal access token in the following format. Note that the value for `github_url` must contain`https://`. The URL is the same URL that you used in the `repo` section of the your taxonomy document reference.
    {: tip}

    ```json
    {
    "github_url": "https://...",
    "github_pat": "xxxxx"
    }
    ```
    {: codeblock}

    For more information, see [Creating Key-value secrets](/docs/secrets-manager?topic=secrets-manager-key-value&interface=ui).
    {: tip}
    
    Cloud storage
    :  Either select a {{site.data.keyword.cos_short}} instance and bucket to use or create an instance and bucket.

    Service authorization
    :   Check the box to allow InstructLab to write your taxonomy to {{site.data.keyword.cos_short}}

    Optional storage settings
    :   Specify the path where you want to store the taxonomy `tar.gz` in {{site.data.keyword.cos_short}}.

1. Click **Upload**

## Add the taxonomy to {{site.data.keyword.cos_short}} by using the CLI
{: #taxonomy-add-cli}
{: cli}

Complete the following steps to store your taxonomy in {{site.data.keyword.cos_short}}.

You can use the `set` command to save {{site.data.keyword.cos_short}} bucket details and credentials, and more. This can simplify your commands going forward. Note that when using the `set` command, you must set each value individually. For more information, see the [Config command reference](/docs/instructlab?topic=instructlab-ilab-cli&interface=cli#ilab-cli-config-command).
{: tip}


{{_include-segments/login.md}}


1. Create the authorization policy for {{site.data.keyword.short_name}} and {{site.data.keyword.cos_short}}.
    ```sh
    ibmcloud iam authorization-policy-create Writer --source-service-name instructlab --target-service-name cloud-object-storage
    ```
    {: pre}

1. **Optional**: If you are using a private repo to store your taxonomy knowledge documents, complete the following steps.

    1. Create a service authorization to allow {{site.data.keyword.short_name}} to access your {{site.data.keyword.secrets-manager_short}} instance and secrets.
        ```sh
        ibmcloud iam authorization-policy-create Writer --source-service-name instructlab --target-service-name secrets-manager
        ```
        {: pre}

    1. Add your personal access token (PAT) to {{site.data.keyword.secrets-manager_short}} by creating a **Key-value** secret. Make sure your key-value details are stored in the following format.
        ```json
        {
        "github_url": "https://...",
        "github_pat": "xxxxx"
        }
        ```
        {: codeblock}

        Example command for creating a key-value secret.
        ```sh
        ibmcloud secrets-manager secret-create --secret-prototype='{"name": "my-secret","description": "Description of my key-value secret.","secret_type": "kv","secret_group_id": "67d025e1-0248-418f-83ba-deb0ebfb9b4a","labels": ["dev","us-south"],"data": {"github_url": "https://...","github_pat": "xxxxx"},"custom_metadata": {"metadata_custom_key": "metadata_custom_value"},"version_custom_metadata": {"custom_version_key": "custom_version_value"}}'
        ```
        {: pre}

        For more information, see [Creating Key-value secrets](/docs/secrets-manager?topic=secrets-manager-key-value&interface=ui).
        {: tip}

    1. List your {{site.data.keyword.secrets-manager_short}} instances.
        ```sh
        ibmcloud resource service-instances --service-name secrets-manager
        ```
        {: pre}

    1. Get your instance details.
        ```sh
        ibmcloud resource service-instances INSTANCE
        ```
        {: pre}


1. Run the `taxonomy add --help` command and review the command options.
    ```sh
    ibmcloud ilab taxonomy add --help
    ```
    {: pre}

1. **Optional** If you have an existing {{site.data.keyword.cos_short}} instance that you want to use, get your service instance details.

    1. List your {{site.data.keyword.cos_short}} instances.
        ```sh
        ibmcloud resource service-instances --service-name cloud-object-storage
        ```
        {: pre}

    1. Get your instance details.
        ```sh
        ibmcloud resource service-instances INSTANCE
        ```
        {: pre}

1. Add your taxonomy to your {{site.data.keyword.cos_short}} bucket. Review the following example commands.

    [Quick start]{: tag-green} Example command to automatically create an {{site.data.keyword.cos_short}} instance and bucket in your account and upload a taxonomy from your `./taxonomy` folder to it.
    ```sh
    ibmcloud ilab taxonomy add \
    --name example-taxonomy-1 \
    --taxonomy-path "./taxonomy"
    ```
    {: pre}

    Example command to upload a taxonomy from a `taxonomy` folder on your machine to an existing {{site.data.keyword.cos_short}} instance and bucket.
    ```sh
    ibmcloud ilab taxonomy add \
	--name example-taxonomy-name-1 \
	--taxonomy-path-cos "taxonomies/taxonomy.tar.gz" \
	--taxonomy-path "./taxonomy" \
	--cos-bucket example-cloud-object-storage-bucket-1 \
	--cos-endpoint https://s3.us-east.cloud-object-storage.appdomain.cloud
    ```
    {: pre}


    Example command to use an existing {{site.data.keyword.cos_short}} instance and bucket as well as {{site.data.keyword.secrets-manager_short}} credentials.
    ```sh
    ibmcloud ilab taxonomy add \
    --name example-taxonomy-1 \
    --taxonomy-path-cos taxonomies/taxonomy.tar.gz \
    --taxonomy-path "./taxonomy" \
    --cos-endpoint https://s3.us-east.cloud-object-storage.appdomain.cloud \
    --secrets-manager-git-id SEC-MGR-ID
    --secrets-manager-git-url https://URL
    ```
    {: pre}

    Example command to upload a taxonomy from your `/Users/USER/instructlab-taxonomy` folder to an new, automatically created bucket.
    ```sh
    ibmcloud ilab taxonomy add \
    --name test \
    --taxonomy-path "/Users/USER/instructlab-taxonomy" \
    --cos-endpoint https://s3.us-east.cloud-object-storage.appdomain.cloud \
    --cos-id 628e4348-2183-42fa-a03a-6f0f78453530
    ```
    {: pre}


## What's next?
{: #next}

[Generate data from the taxonomy.](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-data-generate)
