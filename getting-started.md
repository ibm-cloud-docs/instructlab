---

copyright:
  years: 2024, 2025
lastupdated: "2025-05-01"

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


## Get familiar with the capabilities
{: #get-familiar}

To use {{site.data.keyword.short_name}}, you do not need to have any preexisting knowledge. You do not even need to have an idea for what to create yet. Let's start by just getting familiar with the concepts and what kinds of things you can do with the technology.

[Generative AI](#x10298036){: term} starts with a [large language model (LLM)](#x10298052){: term}. With a prompt, these models can take sets of data and provide a statistically probable output for that prompt. You can automatically generate a data set that is similar to real data, and then use it to train the model to get the most probable output possible.

With {{site.data.keyword.short_name}}, you can use an existing, pre-trained LLM compiled by a community of contributors, and then generate the data to further train the model. By incorporating {{site.data.keyword.cloud_notm}}, you have a place to store the taxonomy, which is the informational structure, for the model as you modify and train it on an ongoing basis.

![Task flow diagram for generating a model with the service.](images/task-flow.svg "Task flow diagram for generating a model with the service."){: caption="Task flow diagram." caption-side="bottom"}{: external download="task-flow.svg"}


## Prerequisites
{: #instructlab-pre}

If this is the first time {{site.data.keyword.short_name}} is being used in the account, complete these tasks.

* A **Pay-As-You-Go** or **Subscription** {{site.data.keyword.cloud}} account. Trial accounts are not supported. For more information or to upgrade the account, see [Account types](/docs/account?topic=account-accounts#compare).


* [An {{site.data.keyword.short_name}} project](/docs/instructlab?topic=instructlab-project).

* [Access to {{site.data.keyword.short_name}} and {{site.data.keyword.cos_short}}](/docs/instructlab?topic=instructlab-iam).

* [Install the CLI](/docs/instructlab?topic=instructlab-cli-install).{: cli}




## Optional: Modify the community taxonomy
{: #taxonomy}

If you don't already have a taxonomy, you can use the {{site.data.keyword.short_name}} [community taxonomy](https://github.com/instructlab/taxonomy){: external} to start.

To create your own taxonomy instead, see [Preparing taxonomies](/docs/instructlab?topic=instructlab-taxonomy-prep&interface=ui) for more information. 
{: tip}

1. Fork the [community taxonomy repo](https://github.com/instructlab/taxonomy) by clicking **Fork** and completing the steps.

1. Clone your fork to your local machine.{: cli}
    ```sh
    git clone https://github.com/<my-org>/taxonomy
    ```
    {: pre}

1. Optional: Make updates to the taxonomy in your fork. This example adds rhyming questions to the [linguistics](https://github.com/instructlab/taxonomy/tree/main/compositional_skills/grounded/linguistics) directory.

    a. In your fork, create a `/instructlab-taxonomy/compositional_skills/grounded/linguistics/rhyming_words/qna.yaml` file.

    b. In the `qna.yml` file, add a question related to rhyming words.
    ```yaml
    - answer: 'Here are two rhyming words for "cave":
        1\. Brave

        2\. Gave'
      question: 'Give me two words that rhyme with cave'
    ```
    {: codeblock}

    c. If your additions include reference documents in Github, such as [this example](https://github.com/instructlab/taxonomy/blob/main/knowledge/science/animals/birds/black_capped_chickadee/qna.yaml#L185), you can use public `github.com` repositories. 

    ```txt
    document:
    repo: https://github.com/<organization>/<repository>
    commit: <commit_sha>
    patterns:
        - <filename>.md
    ```
    {: codeblock}

    If you are using a private repository, you must give the `instructlab-ibm` user read access to the repository. Click **Settings** > **Collaborators** and in the **Manage Access** section, click **Add people**. Invite `instructlab-ibm`. The invitation is labeled as `pending` for 1-2 business days until the invitation is accepted. Until the invitation is accepted, you can continue to work with the taxonomy and generate data, but wait to complete the training steps.
    {: important}

    d. Save the changes and push the changes to the fork. {: cli}

    e. Optional: Learn more about how to modify the [taxonomy](https://github.com/instructlab/taxonomy) for the model.

    f. Optional: [Validate the updated taxonomy](/docs/instructlab?topic=instructlab-ts-debug#version).

1. In a browser, open the **Releases** page for your Github repository. For example: `https://github.com/<my-org>/taxonomy/releases`.

1. Click **Create a release**.

1. Create a tag, select a target branch, and enter a name for the release.

1. Click **Publish a release**.

1. To download the packaged TAR file that was automatically generated, in the release that was created, click **Source code (tar.gz)**.


## Upload your taxonomy to {{site.data.keyword.cos_short}} by using the console
{: #taxonomy-add-ui}
{: ui}

Complete the following steps to store your taxonomy in {{site.data.keyword.cos_short}}.

If you are using a private repository, you can specify a Secrets Manager ID when you [add your taxonomy to {{site.data.keyword.cos_short}} with the CLI](/docs/instructlab?topic=instructlab-getting-started&interface=cli#taxonomy-add-cli). 
{: tip}

1. From the **Projects** [page](https://cloud.ibm.com/instructlab/projects){: external}, select your project.

1. Click **Taxonomies**.
    
1. Click **Upload** and enter the following details.

    Taxonomy file
    :   Select your `.tar.gz` file.
    
    Taxonomy name
    :   Give the taxonomy an alphanumeric name.
    
    Cloud storage
    :   Select a {{site.data.keyword.cos_short}} instance and bucket to use or create an instance and bucket if you don't already have them.

    Service authorization
    :   Check the box to allow InstructLab to write your taxonomy to {{site.data.keyword.cos_short}}

    Optional: Storage settings
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


1. Run the `taxonomy add --help` command and review the command options.
    ```sh
    ibmcloud ilab taxonomy add --help
    ```
    {: pre}

1. **Optional** If you have an existing {{site.data.keyword.cos_short}} instance that you want to use, get your service instance details.

    List your instances.
    ```sh
    ibmcloud resource service-instances --service-name cloud-object-storage
    ```
    {: pre}

    Get the details of an instance.
    ```sh
    ibmcloud resource service-instances INSTANCE
    ```
    {: pre}


1. Add the taxonomy to an {{site.data.keyword.cos_short}} bucket. Review the following example commands.

    **Quick start**: Example command to automatically create an {{site.data.keyword.cos_short}} instance and bucket in your account and upload a taxonomy from your `Downloads` folder to it.
    ```sh
    ibmcloud ilab taxonomy add \
    --name example-taxonomy-1 \
    --taxonomy-path-cos "taxonomies/taxonomy.tar.gz" \
    --taxonomy-path "Downloads/taxonomy.tar.gz"
    ```
    {: pre}

    Example command to upload a taxonomy from a `taxonomy` folder on your machine to an existing {{site.data.keyword.cos_short}} instance and bucket.
    ```sh
    ibmcloud ilab taxonomy add \
	--name example-taxonomy-name-1 \
	--taxonomy-path-cos "taxonomies/taxonomy.tar.gz" \
	--taxonomy-path "./taxonomy" \
	--cos-bucket example-cloud-object-storage-bucket-1 \
	--cos-endpoint https://s3.us-east.cloud-object-storage.appdomain.cloud \
	--cos-id 628e4348-2183-42fa-a03a-6f0f78453530
    ```
    {: pre}


    Example command to use an existing {{site.data.keyword.cos_short}} instance and bucket as well as {{site.data.keyword.secrets-manager_short}} credentials.
    ```sh
    ibmcloud ilab taxonomy add \
    --name example-taxonomy-1 \
    --taxonomy-path-cos taxonomies/taxonomy.tar.gz \
    --taxonomy-path "Downloads/taxonomy.tar.gz" \
    --cos-bucket-information '{"service_instance_id": "628e4348-2183-42fa-a03a-6f0f78453530", "bucket": "example-bucket-1", "endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"}' \
    --secrets-manager-config '{"url": "https://12345678-abcd-1234-5678-abcdefghijkl.us-east.secrets-manager.appdomain.cloud", "git_id": "d9428888-122b-11e1-b85c-61cd3cbb3210"}'
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
