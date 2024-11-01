---

copyright:
  years: 2024, 2024
lastupdated: "2024-11-01"

keywords: instructlab, ai

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Training models
{: #model-train}


Complete the following steps to train your model on generated data, then test the model to verify the results.

## Prerequisites
{: #model-train-pre}
{: cli}

1. [Prepare your taxonomy](/docs/instructlab?topic=instructlab-getting-started#taxonomy)
1. [Add the taxonomy TAR to your COS bucket](/docs/instructlab?topic=instructlab-getting-started#taxonomy-add-ui).
1. [Generate data from your taxonomy](/docs/instructlab?topic=instructlab-data-generate).


## Training models by using the console
{: #model-train-ui}
{: ui}

1. In the console, open the [InstructLab service](https://cloud.ibm.com/instructlab/overview).

1. Click **Custom models** > **Train**.

1. Provide an alphanumeric name for the model, select the training data to use, and click **Train**. The state is `queued`, then `running`. Wait for the state to be `completed`. This process could take minutes or hours. When the training is complete, in the COS bucket, a `trained_models` directory is created with logs for troubleshooting.



## What's next?
{: #next}

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
    # Replace variable with the COS bucket name
    CUSTOMER_BUCKET="XXX"
    # Replace variable with the COS endpoint
    COS_ENDPOINT=https://s3.direct.us-east.cloud-object-storage.appdomain.cloud
    # Replace variable with the model ID
    MODEL_PREFIX="trained_models/XXX/model/"
    # Replace variable with the model directory path
    MODEL_DIR=/root/model/modeltest
    curl -v -G "$COS_ENDPOINT/$CUSTOMER_BUCKET" --data-urlencode "list-type=2" --data-urlencode "prefix=$MODEL_PREFIX" -H "Authorization: Bearer $BEARER_TOKEN" >/tmp/rawxml.txt
    cat /tmp/rawxml.txt | awk '{split($0,a,"<Key>"); for (i=1; i<=length(a); i++)  print a[i]}' >/tmp/keysonnewline.txt
    mkdir -p "$MODEL_DIR"
    while read -r line; do
        if [[ "$line" != "trained_models"* ]]; then
            continue
        fi
        KEY_TO_DOWNLOAD=$(echo "$line" | awk -F '<' '{print $1}')
        FILE_NAME=$(basename "$KEY_TO_DOWNLOAD")
        curl -X "GET" "$COS_ENDPOINT/$CUSTOMER_BUCKET/$KEY_TO_DOWNLOAD" -H "Authorization: Bearer $BEARER_TOKEN" >"${MODEL_DIR}/$FILE_NAME"
    done </tmp/keysonnewline.txt
    ```
    {: pre}
    
1. Then use the `ilab` commands to serve and chat.

    ```sh
    ilab model serve --model-path $MODEL_DIR -- --tensor-parallel-size 1 --host 0.0.0.0 --port 8080
    ```
    {: pre}
   
    ```sh
    ilab model chat --endpoint-url http://localhost:8080/v1 -m $MODEL_DIR
    ```
    {: pre}
