---

copyright:
  years: 2024, 2024
lastupdated: "2024-11-22"

keywords: instructlab, ai

subcollection: instructlab

content-type: tutorial

services: instructlab
account-plan: paid
completion-time: 30m

---

{{site.data.keyword.attribute-definition-list}}


# Getting started with {{site.data.keyword.instructlab_full_notm}}
{: #getting-started}
{: toc-content-type="tutorial"}
{: toc-services="instructlab"}
{: toc-completion-time="30m"}

Get ready to dive into [AI](#x3448902){: term} with {{site.data.keyword.instructlab_full}}! {{site.data.keyword.instructlab_short}} is an open source project created by IBM and Red Hat to be a cost-effective entry point into the world of [machine learning](#x8397498){: term}.
{: shortdesc}


## Prerequisites
{: #instructlab-pre}


Before you begin, you must have a paid {{site.data.keyword.cloud}} account.

The following account types are supported:

- Pay-As-You-Go
- Subscription

Trial accounts are not supported. For more information or to upgrade your account, see [Account types](/docs/account?topic=account-accounts#compare).


## Get familiar with the capabilities
{: #get-familiar}
{: step}

If you are new to machine learning, you are in the correct place. To use InstructLab, you do not need to have any preexisting knowledge. You do not even need to have an idea for what to create yet. Let's start by just getting familiar with the concepts and what kinds of things you can do with the technology.

[Generative AI](#x10298036){: term} starts with a [large language model (LLM)](#x10298052){: term}. With a prompt, these models can take sets of data and provide a statistically probable output for that prompt. You can automatically generate a data set that is similar to real data, and then use it to train the model to get the most probable output possible.

With InstructLab, you can use an existing, pre-trained LLM compiled by a community of contributors, and then generate the data to further train the model. By incorporating {{site.data.keyword.cloud_notm}}, you have a place to store the taxonomy, the informational structure, for the model as you modified it and train the model on an ongoing basis.

![Task flow diagram for generating a model with the service.](images/task-flow.svg "Task flow diagram for generating a model with the service."){: caption="Task flow diagram." caption-side="bottom"}{: external download="task-flow.svg"}


## Request access
{: #access}
{: step}


The {{site.data.keyword.instructlab_short}} service is under development and is not yet generally available. The project is currently at capacity with many critical test projects involved. As the service develops, capacity is expected to added.

For your project to be considered, request access.

1. Retrieve your production account ID from the [Account settings](https://cloud.ibm.com/account/settings){: external} page. 
1. Send an email to `instructlab@ibm.com` with the following information. 

    To
    ```txt
    instructlab@ibm.com
    ```
    {: codeblock}

    Subject
    ```txt
    Request to allowlist account: <account_id> to use IBM Cloud InstructLab Service.
    ```
    {: codeblock}

    Body
    ```txt
    Add account <account_id> to the allowlist for the IBM Cloud InstructLab service.
    Team: <team>
    Approval given by: <approver>
    UI access required: <yes/no>
    Purpose: <short summary of type of usage for the service>
    ```
    {: codeblock}

Allow 1-2 business days for the request to be processed. While you wait for your account to be added to the allowlist, you can complete most of these steps. After you are allowlisted, you can access the InstructLab UI and CLI. 



## Install the CLIs
{: #cli-install}
{: step}
{: cli}

1. Optional: Install the [Git CLI](https://docs.github.com/en/get-started/getting-started-with-git/set-up-git) to store and manage your taxonomies.

1. Install the [{{site.data.keyword.cloud_notm}} CLI](/docs/cli?topic=cli-getting-started).

1. [Install the COS CLI plugin](/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli).
    ```sh
    ibmcloud plugin install cos
    ```
    {: pre}

1. Install the plug-in.

    ```sh
    ibmcloud plugin install ilab
    ```
    {: pre}

1. Log in to your {{site.data.keyword.cloud_notm}} account from the CLI.
    ```sh
    ibmcloud login -a https://cloud.ibm.com --sso -r us-east
    ```
    {: pre}

1. If you plan to allow InstructLab to create Cloud Object Storage Instance resources for you, target a resource group.
    ```sh
    ibmcloud target -g <resource_group>
    ```
    {: pre}


## Give InstuctLab permission to create and update COS artifacts
{: #storage-auth-cli}
{: cli}
{: step}

Give InstructLab the `Writer` access role for the COS service. The logged-in user must also have the same permission.

1. Create the authrorization policy for InstructLab.
    ```sh
    ibmcloud iam authorization-policy-create Writer --source-service-name instructlab --target-service-name cloud-object-storage
    ```
    {: pre}

    If you already have COS resources to use, you can scope the authorization to only those resources.
    ```sh
    ibmcloud iam authorization-policy-create Writer --source-service-name instructlab --target-service-name cloud-object-storage --target-service-instance-id <cloud-object-storage-instance-id> --target-resource <cloud-object-storage-bucket> --target-resource-type bucket
    ```
    {: pre}

1. Verify that the authorization policy was created.
    ```sh
    ibmcloud iam authorization-policies
    ```
    {: pre}

    Result when authorization is not scoped to a specific COS bucket:
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

    Result when authorization is scoped to a specific COS bucket:
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

1. If necessary, give the `Writer` permission to the logged-in user. Include the Cloud Object Storage service instance ID from the previous step.

    ```sh
    ibmcloud iam user-policy-create <user> --roles Writer --service-instance <cloud-object-storage-instance-id>
    ```
    {: pre}



## Create an authorization policy for InstuctLab
{: #storage-auth-ui}
{: ui}
{: step}

Give InstructLab the `Writer` access role for the COS service. The logged-in user must also have the same permission.

1. Create an authrorization policy gives InstructLab `Writer` access to the COS service.

    a. In the user interface, click **Manage** > **Access (IAM)** > **Authorizations**.

    b. For the source service, select the **InstructLab** service.

    c. For the target service, select the **Cloud Object Storage** service.

    d. In the **Roles** section, for **Service access**, select **Writer**.

    e. Click **Authorize**.

1. If necessary, give the `Writer` permission to the logged-in user.

    a. In the user interface, click **Manage** > **Access (IAM)** > **Users**.
    
    b. Click the user name > **Access** and in the **Assign policies** section, click **Assign access**.
    
    c. Select the **Cloud Object Storage** service and complete the prompts.
    
    d. In the **Roles and Actions** section, for **Service access**, select **Writer**.


## Optional: Create a COS instance and bucket
{: #cos-create-manual}
{: ui}
{: step}


1. If you don't have a service instance yet, [provision a COS instance](https://cloud.ibm.com/objectstorage/create){: external} in your account.

1. [Create a new bucket](https://cloud.ibm.com/objectstorage) and make a note of the bucket name for later.


## Optional: Create a COS instance and bucket by using the CLI
{: #storage-manual-cli}
{: cli}
{: step}

1. If you don't have a service instance yet, [provision a COS instance](/docs/cloud-object-storage?topic=cloud-object-storage-provision#provision-instance){: external} in your account. Make a note of your instance ID.
    ```sh
    ibmcloud resource service-instance-create <instance-name> cloud-object-storage <plan> global
    ```
    {: pre}

1. [Create a new bucket](/docs/cloud-object-storage?topic=cloud-object-storage-ic-cos-cli#create-a-new-bucket) and make a note of the bucket name for later.
    ```sh
    ibmcloud cos bucket-create --bucket <bucket-name> [--class <class-name>] [--ibm-service-instance-id <instance-id>] [--region REGION] [--output FORMAT]
    ```
    {: pre}



## Prepare a taxonomy
{: #taxonomy}
{: step}

In this example, use the Git CLI to clone and update the InstructLab [community taxonomy](https://github.com/instructlab/taxonomy){: external}.

1. Fork the [community taxonomy repo](https://github.com/instructlab/taxonomy) by clicking **Fork** and completing the steps.

1. Clone your fork to your local machine.
    ```sh
    git clone https://github.com/<my-org>/taxonomy
    ```
    {: pre}

1. Optional: Make updates to the taxonomy in your fork. This example adds rhyming questions to the [linguistics](https://github.com/instructlab/taxonomy/tree/main/compositional_skills/grounded/linguistics) directory.

    a. In your cloned fork, create a `/instructlab-taxonomy/compositional_skills/grounded/linguistics/rhyming_words/qna.yaml` file.

    b. In the `qna.yml` file, add a question related to rhyming words.
    ```txt
    - answer: 'Here are two rhyming words for "cave":


        1\. Brave

        2\. Gave


        '
    question: 'Give me two words that rhyme with cave

        '

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


## Add your taxonomy to COS
{: #taxonomy-add-ui}
{: step}
{: ui}

After you receive access to InstructLab, store your taxonomy in COS.

1. From a command-line terminal, change directories to the parent directory of your taxonomy directory.
    ```sh
    cd <taxonomy_repo_parent_dir>
    ```
    {: pre}

    Example if your taxonomy is in `~/documents/clones/taxonomy`:
    ```sh
    cd ~/documents/clones
    ```
    {: pre}

1. TAR the local taxonomy. Use alphanumeric characters in the taxonomy name.

    ```sh
    tar -czvf <taxonomy_name>.tar.gz <taxonomy_dir_name>
    ```
    {: pre}

    Example if your taxonomy is in `~/documents/clones/taxonomy`:
    ```sh
    tar -czvf taxonomy.tar.gz taxonomy
    ```
    {: pre}

1. In the console, open the [InstructLab taxonomies](https://cloud.ibm.com/instructlab/taxonomies).

1. Click **Upload**.

1. Select the `.tar.gz` file, give the taxonomy an alphanumeric name, select the COS instance and bucket to use (or create a new one), then click **Upload**.



## Add your taxonomy to COS by using the CLI
{: #taxonomy-add-cli}
{: step}
{: cli}

After you receive access to InstructLab, store your taxonomy in COS.

1. Optional: Run the `init` command to set and save COS bucket details and credentials, which can simplify your commands going forward. If you don't want to save these details and want to include them in the `add` command instead, you can continue to the next step.

    If you want the COS service instance or bucket to be created automatically later, you do not need to add those options here. The details are saved for you.
    {: tip}

    ```sh
    ibmcloud ilab config init \
    --taxonomy-path <local-path-to-taxonomy> \
    --taxonomy-path-cos <taxonomy-path-in-cos-bucket> \
    --cos-bucket <bucket_name> \
    --cos-endpoint <endpoint> \
    --cos-region <region> \
    --cos-service-instance-id <service_id>
    ```
    {: pre}

    | Parameter | Description |
    | -------------- | -------------- |
    | `--taxonomy-path <local_directory_path` | Required. The local directory path to the taxonomy file. |
    | `--taxonomy-path-cos <directory_path>` | Optional. The relative directory path within the COS bucket to the taxonomy file. |
    | `--cos-bucket <bucket_name>` | Optional. If you are adding a taxonomy to an existing bucket, include the name. You can find this name on the **Buckets** tab of your COS instance. If you want the bucket to be created for you, you can enter a name for it. If no name is specified and a bucket does not exist yet, a bucket is created that is named `instructlab_TIME`, where `TIME` is the current epoch time. |
    | `--cos-endpoint <endpoint>` | Optional. Use the public, regional endpoint. For example `https://s3.us-east.cloud-object-storage.appdomain.cloud`. You can find these in the **Endpoints** tab of the COS console. |
    | `--cos-region <region>` | Optional. The default value is `us-east`. |
    | `--cos-service-instance-id <service_id>` | Optional. If you have a COS service instance to use, include the service ID. In the user interface for the COS service instance, click **Details**. Note the **CRN**, which can be used for the service instance ID. If you want one to be created for you, it is created with the name `InstructLab`.|
    {: caption="Understanding this command's components" caption-side="bottom"}

    Example command to save the taxonomy path, but have the COS service instance and bucket created for you later.
    ```sh
    ibmcloud ilab config init \
    --taxonomy-path /Users/USER/instructlab-taxonomy \
    ```
    {: pre}

    Example command to save the taxonomy path and the details for an existing COS service, but have the COS bucket created for you later.
    ```sh
    ibmcloud ilab config init \
    --taxonomy-path /Users/USER/instructlab-taxonomy \
    --cos-service-instance-id existing_service_instance_id
    ```
    {: pre}

    Example command to save the taxonomy path and the details for an existing bucket.
    ```sh
    ibmcloud ilab config init \
    --taxonomy-path /Users/USER/instructlab-taxonomy \
    --cos-bucket existing-instruct-lab-bucket 
    ```
    {: pre}

1. Add the taxonomy to a COS bucket.
    ```sh
    ibmcloud ilab taxonomy add --name <name>
    ```
    {: pre}

    | Parameter | Description |
    | -------------- | -------------- |
    | `--name <taxonomy_name>` | Required. The name of the taxonomy as it is to be displayed in the COS bucket. Use alphanumeric characters in the taxonomy name.|
    | `--taxonomy-path <local_directory_path>` | Required if not specified with the `init` command. The local directory path to the taxonomy. |
    | `--taxonomy-path-cos <directory_path>` | Optional. The relative directory path within the COS bucket to the taxonomy file. |
    | `--cos-bucket <bucket_name>` | Optional. If you are adding a taxonomy to an existing bucket, include the name. You can find this name on the **Buckets** tab of your COS instance. If you want the bucket to be created for you, you can enter a name for it. If no name is specified and a bucket does not exist yet, a bucket is created that is named `instructlab_TIME`. |
    | `--cos-endpoint <endpoint>` | Optional. Use the public, regional endpoint. For example `https://s3.us-east.cloud-object-storage.appdomain.cloud`. You can find these in the **Endpoints** tab of the COS console. |
    | `--cos-region <region>` | Optional. The default value is `us-east`. |
    | `--cos-service-instance-id <service_id>` | Optional. If you have a COS service instance to use, include the service ID. In the user interface for the COS service instance, click **Details**. Note the **CRN**, which can be used for the service instance ID. If you want one to be created for you, it is created with the name `InstructLab`.|
    {: caption="Understanding this command's components" caption-side="bottom"}

    Example command to use the details that were saved with the `init` command.
    ```sh
    ibmcloud ilab taxonomy add --name test
    ```
    {: pre}

    Example command to have the COS bucket created for you in an existing service instance.
    ```sh
    ibmcloud ilab taxonomy add \
    --name test \
    --taxonomy-path /Users/USER/instructlab-taxonomy \
    --cos-service-instance-id existing_service_instance_id
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

[Generate data from the taxonomy.](/docs/instructlab?topic=instructlab-data-generate)
