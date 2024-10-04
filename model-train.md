---

copyright:
  years: 2024, 2024
lastupdated: "2024-10-04"

keywords: instructlab, ai

subcollection: instructlab

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
    ibmcloud ilab model train --name test-model --data-id <data_id>
    ```
    {: pre}

1. Check the details of your data generation. Include the ID for the model. The state is `queued`, then `running`. Wait for the state to be `completed`. This process could take minutes or hours.

    ```sh
    ibmcloud ilab model get --id <model_id>
    ```
    {: pre}

    When the state is `completed`, in the COS bucket, a `trained_models` directory is created with logs for troubleshooting.

## What's next?
{: #model_next}

Optional: You can deploy the model to RHEL-AI on {{site.data.keyword.cloud_notm}}.

1. [Install RHEL-AI on {{site.data.keyword.cloud_notm}}](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.1/html/installing/installing_ibm_cloud#converting_image_to_qcow).

1. Using the {{site.data.keyword.cloud_notm}} CLI, get a bearer token.
    ```sh
    ibmcloud iam oauth-tokens
    ```
    {: pre}

1. Update the variables from this bash script and run it.

    ```sh
    #!/usr/bin/env bash
    # Replace variable with the bearer token
    BEARER_TOKEN="XXX"
    # Replace variable with the service id
    SERVICE_INSTANCE_ID="XXX"
    # Replace variable with the COS bucket name
    CUSTOMER_BUCKET="XXX"
    # Replace variable with the COS endpoint
    COS_ENDPOINT=https://s3.direct.us-east.cloud-object-storage.appdomain.cloud
    # Replace variable with the model ID
    MODEL_PREFIX="trained_models/XXX/model/"
    # Replace variable with the model directory path
    MODEL_DIR=/root/model/modeltest
    curl -v -G "$COS_ENDPOINT/$CUSTOMER_BUCKET" --data-urlencode "list-type=2" --data-urlencode "prefix=$MODEL_PREFIX" -H "Authorization: Bearer $BEARER_TOKEN" -H "ibm-service-instance-id: $SERVICE_INSTANCE_ID" >/tmp/rawxml.txt
    cat /tmp/rawxml.txt | awk '{split($0,a,"<Key>"); for (i=1; i<=length(a); i++)  print a[i]}' >/tmp/keysonnewline.txt
    mkdir -p "$MODEL_DIR"
    while read -r line; do
        if [[ "$line" != "trained_models"* ]]; then
            continue
        fi
        KEY_TO_DOWNLOAD=$(echo "$line" | awk -F '<' '{print $1}')
        FILE_NAME=$(basename "$KEY_TO_DOWNLOAD")
        curl -X "GET" "$COS_ENDPOINT/$CUSTOMER_BUCKET/$KEY_TO_DOWNLOAD" -H "Authorization: Bearer $BEARER_TOKEN" -H "ibm-service-instance-id: $SERVICE_INSTANCE_ID" >"${MODEL_DIR}/$FILE_NAME"
    done </tmp/keysonnewline.txt
    ```
    {: pre}
