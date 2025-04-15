---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-15"

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

Get ready to dive into [AI](#x3448902){: term} with {{site.data.keyword.instructlab_full}}! {{site.data.keyword.instructlab_short}} is an open source project created by IBM and Red Hat to be a cost-effective entry point into the world of [machine learning](#x8397498){: term}.
{: shortdesc}


{{site.data.keyword.short_name}} is available to allowlisted accounts only.
{: preview}


## Prerequisites
{: #instructlab-pre}

Before you begin, you must the following

* A paid {{site.data.keyword.cloud}} account. The following account types are supported:
    - Pay-As-You-Go
    - Subscription

Trial accounts are not supported. For more information or to upgrade your account, see [Account types](/docs/account?topic=account-accounts#compare).
{: note}

* An {{site.data.keyword.cos_short}} intsance in your account.


## Get familiar with the capabilities
{: #get-familiar}

If you are new to machine learning, you are in the correct place. To use {{site.data.keyword.short_name}}, you do not need to have any preexisting knowledge. You do not even need to have an idea for what to create yet. Let's start by just getting familiar with the concepts and what kinds of things you can do with the technology.

[Generative AI](#x10298036){: term} starts with a [large language model (LLM)](#x10298052){: term}. With a prompt, these models can take sets of data and provide a statistically probable output for that prompt. You can automatically generate a data set that is similar to real data, and then use it to train the model to get the most probable output possible.

With {{site.data.keyword.short_name}}, you can use an existing, pre-trained LLM compiled by a community of contributors, and then generate the data to further train the model. By incorporating {{site.data.keyword.cloud_notm}}, you have a place to store the taxonomy, which is the informational structure, for the model as you modify and train it on an ongoing basis.

![Task flow diagram for generating a model with the service.](images/task-flow.svg "Task flow diagram for generating a model with the service."){: caption="Task flow diagram." caption-side="bottom"}{: external download="task-flow.svg"}



## Optional: Prepare a taxonomy
{: #taxonomy}

If you don't already have a taxonomy, you can use the {{site.data.keyword.short_name}} community taxonomy. Forking the community taxonomy is a great way to get started with {{site.data.keyword.instructlab_short}}. 

In this example, use the Git CLI to clone and update the InstructLab [community taxonomy](https://github.com/instructlab/taxonomy){: external}.

If you later want to create your own taxonomy, see [Preparing taxonomies](https://cloud.ibm.com/docs-draft/instructlab?topic=instructlab-taxonomy-prep&interface=ui) for more information. 
{: tip}

1. Install the [Git CLI](https://docs.github.com/en/get-started/git-basics/set-up-git) to store and manage your taxonomies.

1. Fork the [community taxonomy repo](https://github.com/instructlab/taxonomy) by clicking **Fork** and completing the steps.

1. Clone your fork to your local machine.
    ```sh
    git clone https://github.com/<my-org>/taxonomy
    ```
    {: pre}

1. Optional: Make updates to the taxonomy in your fork. This example adds rhyming questions to the [linguistics](https://github.com/instructlab/taxonomy/tree/main/compositional_skills/grounded/linguistics) directory.

    a. In your cloned fork, create a `/instructlab-taxonomy/compositional_skills/grounded/linguistics/rhyming_words/qna.yaml` file.

    b. In the `qna.yml` file, add a question related to rhyming words.
    ```yaml
    - answer: 'Here are two rhyming words for "cave":
        1\. Brave

        2\. Gave'
      question: 'Give me two words that rhyme with cave'
    ```
    {: codeblock}

    c. If your additions include reference documents in Github, such as [this example](https://github.com/instructlab/taxonomy/blob/main/knowledge/science/animals/birds/black_capped_chickadee/qna.yaml#L185), you can use public `github.com` repositories and IBM internal `github.ibm.com` repositories. 

    ```txt
    document:
    repo: https://github.ibm.com/<organization>/<repository>
    commit: <commit_sha>
    patterns:
        - <filename>.md
    ```
    {: codeblock}

    If you are using a private repository, you must give the `instructlab-ibm` user read access to the repository. Click **Settings** > **Collaborators** and in the **Manage Access** section, click **Add people**. Invite `instructlab-ibm`. The invitation is labeled as `pending` for 1-2 business days until the invitation is accepted. Until the invitation is accepted, you can continue to work with the taxonomy and generate data, but wait to complete the training steps.
    {: important}

    d. Save the changes and push the changes to the fork.

    f. Optional: Learn more about how to modify the [taxonomy](https://github.com/instructlab/taxonomy) for the model.

    g. Optional: [Validate the updated taxonomy](/docs/instructlab?topic=instructlab-ts-debug#version).



## Create an {{site.data.keyword.short_name}} project
{: #project-create-ui}
{: ui}

1. Navigate to [{{site.data.keyword.short_name}} in the console](https://cloud.ibm.com/catalog/services/instructlab).

1. Review the pricing plan.

1. In the **Configure resource** section, enter the following details.

    Service name
    :   Give your InstructLab project a name.

    Select a resource group
    :   Select the resource group where you want to create your project.

    Tags and Access management tags
    :   Enter any tags or access management tags that you want to use. Tags can help you organize your resources.

1. Accept the license agreement and click **Create**.

After your project is created, the project details page is shown.


## Upload your taxonomy to {{site.data.keyword.cos_short}}
{: #taxonomy-add-ui}
{: ui}

1. Create a packaged TAR file of the contents of the Github taxonomy repository by creating a release.

    a. In a browser, open the **Releases** page for your Github repository. Example: `https://github.com/<my-org>/taxonomy/releases`
    
    b. Click **Create a release**.

    c. Create a tag, select a target branch, and enter a name for the release.

    d. Click **Publish a release**.

    e. To download the packaged TAR file that was automatically generated, in the release that was created, click **Source code (tar.gz)**.

1. Upload the taxonomy to your project.

    a. Click **Taxonomies**.
    
    b. Click **Upload**.

    c. Select the `.tar.gz` file, give the taxonomy an alphanumeric name, select the {{site.data.keyword.cos_short}} instance and bucket to use (or create a new one), then click **Upload**.




## Install the CLIs
{: #cli-install-gs}
{: cli}

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

1. Install the {{site.data.keyword.cos_short}} CLI plugin.
    ```sh
    ibmcloud plugin install cos
    ```
    {: pre}

1. Install the {{site.data.keyword.short_name}} plug-in.

    ```sh
    ibmcloud plugin install ilab
    ```
    {: pre}

1. Log in to your {{site.data.keyword.cloud_notm}} account from the CLI.
    ```sh
    ibmcloud login -a https://cloud.ibm.com --sso -r us-east
    ```
    {: pre}

1. If you plan to allow {{site.data.keyword.short_name}} to create {{site.data.keyword.cos_full}} Instance resources for you, target a resource group.
    ```sh
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    Example:
    ```sh
    ibmcloud target -g Default
    ```
    {: pre}

1. Create a project in the {{site.data.keyword.short_name}} instance.
    ```sh
    ibmcloud resource service-instance-create <project_name> instructlab instructlab-pricing-plan us-east
    ```
    {: pre}


## Give InstuctLab permission to create and update {{site.data.keyword.cos_short}} artifacts
{: #storage-auth-cli}
{: cli}

Give {{site.data.keyword.short_name}} the `Writer` access role for the {{site.data.keyword.cos_short}} service. The logged-in user must also have the same permission.

1. Create the authorization policy for {{site.data.keyword.short_name}}.
    ```sh
    ibmcloud iam authorization-policy-create Writer --source-service-name instructlab --target-service-name cloud-object-storage
    ```
    {: pre}

    If you already have {{site.data.keyword.cos_short}} resources to use, you can scope the authorization to only those resources.
    ```sh
    ibmcloud iam authorization-policy-create Writer --source-service-name instructlab --target-service-name cloud-object-storage --target-service-instance-id <cloud-object-storage-instance-id> --target-resource <cloud-object-storage-bucket> --target-resource-type bucket
    ```
    {: pre}

1. Verify that the authorization policy was created.
    ```sh
    ibmcloud iam authorization-policies
    ```
    {: pre}

    Result when authorization is not scoped to a specific {{site.data.keyword.cos_short}} bucket:
    ```txt
    Getting authorization policies under account abc1234 as user...
    OK

    ID:                        <id>
    Source service name:       instructlab
    Source service instance:   All instances
    Target service name:       cloud-object-storage
    Target service instance:   All instances
    Roles:                     Writer
    ```
    {: screen}

    Result when authorization is scoped to a specific {{site.data.keyword.cos_short}} bucket:
    ```txt
    Getting authorization policies under account abc1234 as user...
    OK

    ID:                        <id>
    Source service name:       instructlab
    Source service instance:   All instances
    Target service name:       cloud-object-storage
    Target service instance:   bucket
    Roles:                     Writer
    ```
    {: screen}

1. If necessary, give the `Writer` permission to the logged-in user. Include the {{site.data.keyword.cos_short}} service instance ID from the previous step.

    ```sh
    ibmcloud iam user-policy-create <user> --roles Writer --service-instance <cloud-object-storage-instance-id>
    ```
    {: pre}

## Add your taxonomy to {{site.data.keyword.cos_short}}
{: #taxonomy-add-cli}
{: cli}

Complete the following steps to add your taxonomy in {{site.data.keyword.cos_short}}.

1. Optional: Run the `set` command to set and save {{site.data.keyword.cos_short}} bucket details and credentials, which can simplify your commands going forward. You must set each value individually.

    ```txt
    ibmcloud ilab config set \
        cos-bucket \
        cos-endpoint \
        cos-id \
        project-id \
        secrets-manager-git-id \
        secrets-manager-url \
        taxonomy-path \ # The local directory path to the taxonomy file. 
        taxonomy-path-cos \
    ```
    {: pre}

    | Component | Description |
    | --- | --- |
    | `cos-bucket <bucket_name>` | If you are adding a taxonomy to an existing bucket, include the name. You can find this name on the **Buckets** tab of your {{site.data.keyword.cos_short}} instance. If you want the bucket to be created for you, you can enter a name for it. If no name is specified and a bucket does not exist yet, a bucket is created that is named `instructlab_TIME`, where `TIME` is the current epoch time. |
    | `cos-endpoint <endpoint>` | Use the public, regional endpoint. For example `https://s3.us-east.cloud-object-storage.appdomain.cloud`. You can find these in the **Endpoints** tab of the {{site.data.keyword.cos_short}} console. |
    | `cos-id <service_id>` | If you have an {{site.data.keyword.cos_short}} service instance to use, include the service ID. In the user interface for the {{site.data.keyword.cos_short}} service instance, click **Details**. Note the **CRN**, which can be used for the service instance ID. If you want one to be created for you, it is created with the name `{{site.data.keyword.short_name}}`.|
    | `project-id` | Your {{site.data.keyword.short_name}} project ID. |
    | `secrets-manager-git-id` | The git ID for your Secrets Manager instance. |
    | `secrets-manager-url` | The URL to your Secrets Manager instance. |
    | `taxonomy-path-cos <directory_path>` | The relative directory path within the {{site.data.keyword.cos_short}} bucket to the taxonomy file. |
    {: caption="Understanding this command's components" caption-side="bottom"}


    Example command to save the taxonomy path, but have the {{site.data.keyword.cos_short}} service instance and bucket created for you later.
    ```sh
    ibmcloud ilab config set cos-bucket test-1
    ```
    {: pre}

    Example command to save the taxonomy path and the details for an existing {{site.data.keyword.cos_short}} service, but have the {{site.data.keyword.cos_short}} bucket created for you later.
    ```sh
    ibmcloud ilab config set taxonomy-path /Users/USER/instructlab-taxonomy
    ```
    {: pre}


1. Add the taxonomy to an {{site.data.keyword.cos_short}} bucket.
    ```sh
    ibmcloud ilab taxonomy add --name <name>
    ```
    {: pre}

    | Parameter | Description |
    | -------------- | -------------- |
    | `--name <taxonomy_name>` | Required. The name of the taxonomy as it is to be displayed in the {{site.data.keyword.cos_short}} bucket. Use alphanumeric characters in the taxonomy name.|
    | `--taxonomy-path <local_directory_path>` | Required if not specified with the `init` command. The local directory path to the taxonomy. |
    | `--taxonomy-path-cos <directory_path>` | Optional. The relative directory path within the {{site.data.keyword.cos_short}} bucket to the taxonomy file. |
    | `--cos-bucket <bucket_name>` | Optional. If you are adding a taxonomy to an existing bucket, include the name. You can find this name on the **Buckets** tab of your {{site.data.keyword.cos_short}} instance. If you want the bucket to be created for you, you can enter a name for it. If no name is specified and a bucket does not exist yet, a bucket is created that is named `instructlab_TIME`. |
    | `--cos-endpoint <endpoint>` | Optional. Use the public, regional endpoint. For example `https://s3.us-east.cloud-object-storage.appdomain.cloud`. You can find these in the **Endpoints** tab of the {{site.data.keyword.cos_short}} console. |
    | `--cos-region <region>` | Optional. The default value is `us-east`. |
    | `--cos-id <service_id>` | Optional. If you have an {{site.data.keyword.cos_short}} service instance to use, include the service ID. In the user interface for the {{site.data.keyword.cos_short}} service instance, click **Details**. Note the **CRN**, which can be used for the service instance ID. If you want one to be created for you, it is created with the name `{{site.data.keyword.short_name}}`.|
    {: caption="Understanding this command's components" caption-side="bottom"}

    Example command to use the details that were saved with the `init` command.
    ```sh
    ibmcloud ilab taxonomy add --name test
    ```
    {: pre}

    Example command to have the {{site.data.keyword.cos_short}} bucket created for you in an existing service instance.
    ```sh
    ibmcloud ilab taxonomy add \
    --name test \
    --taxonomy-path /Users/USER/instructlab-taxonomy \
    --cos-id existing_service_instance_id
    ```
    {: pre}

    Example command to use an existing bucket.
    ```sh
    ibmcloud ilab taxonomy add \
    --name test \
    --taxonomy-path /Users/USER/instructlab-taxonomy \
    --cos-bucket existing-instruct-lab-bucket 
    ```
    {: pre}


## What's next?
{: #next}

[Generate data from the taxonomy.](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-data-generate)
