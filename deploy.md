---

copyright:
  years: 2025, 2026
lastupdated: "2026-02-27"

keywords: instructlab, ai

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Deploying models for {{site.data.keyword.short_name}}
{: #deploy}

Choose how to deploy your model.

## Deploying the model to RHEL-AI on {{site.data.keyword.cloud_notm}}
{: #deploy-rhel-ai}

1. [Install RHEL-AI on {{site.data.keyword.cloud_notm}}](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.5/html/installing/installing_ibm_cloud).

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
    # Replace variable with the Object Storage bucket name
    CUSTOMER_BUCKET="XXX"
    # Replace variable with the Object Storage endpoint
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


## Deploying the model to Watsonx on {{site.data.keyword.cloud_notm}}
{: #deploy-watson}

1. Sign up for [IBM watsonx as a Service](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/signup-wx.html?context=wx&audience=wdp).

1. [Log in and create an API key](https://dataplatform.cloud.ibm.com/docs/content/wsj/manage-data/task-credentials.html?context=wx&locale=en&audience=wdp#accessing-task-credentials).

1. If you do not have one yet, [create a project](https://dataplatform.cloud.ibm.com/docs/content/wsj/getting-started/projects.html?context=wx&audience=wdp).

1. [Add a connection](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/deploy-custom-fm-prepare-cloud.html?context=wx&audience=wdp#add-conn-project) to the {{site.data.keyword.cos_short}} data source in {{site.data.keyword.cloud_notm}}.

1. [Import the model](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/deploy-custom-fm-prepare-cloud.html?context=wx&audience=wdp#creating-asset).

1. [Deploy the model](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/deploy-custom-fm-create-cloud.html?context=wx&audience=wdp).

1. [Test the deployment](https://dataplatform.cloud.ibm.com/docs/content/wsj/analyze-data/deploy-custom-fm-create-cloud.html?context=wx&audience=wdp#testing-the-deployment).

## Deploying the model to Red Hat OpenShift AI
{: #deploy-rhoai}


1. If you have not already, [install the Red Hat OpenShift AI add-on](/docs/openshift?topic=openshift-ai-addon-install&interface=ui) on your cluster. It may take up to 15 minutes for the add-on to install. 
1. After the add-on is installed, [navigate to the OpenShift AI dashboard](/docs/openshift?topic=openshift-ai-addon-install&interface=ui#ai-dashboard).
1. Click **Data Science Projects**, then click **Create a Project**.
1. Follow the prompts to give your project a name and description, then click **Create**.
1. Find the **Serve models** section and choose the **Single-model serving platform** option.
1. Click **Deploy model**.
1. Fill out the required configuration properties. To specify the model you trained with {{site.data.keyword.short_name}}, find the **Source model location** section and choose the **S3 compatible object storage -v1** connection type. 
1. Under **Connection details**, specify the access key, secret key, endpoint, and bucket name for the COS bucket that your trained model data is stored in. Specify a path to your model or the folder containing your model within your bucket. 
1. When the remaining configuration properties are filled out, click **Deploy**. 
1. To verify and view the health of the model deployment, click **Model** > **Model deployment** and select the Data Science Project that you created the model in. 
