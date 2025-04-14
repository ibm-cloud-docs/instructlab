---

copyright:
  years: 2024, 2025
lastupdated: "2025-04-14"

keywords: instructlab, ai

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Training models
{: #model-train}


Complete the following steps to train your model on generated data. Then test the model to verify the results.

Configuration information or files cannot be passed to the model for fine tuning.
{: note}


## Prerequisites
{: #model-train-pre}

1. [Prepare your taxonomy](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-getting-started#taxonomy)
1. Add the taxonomy TAR to your {{site.data.keyword.cos_short}} bucket. You can use the [CLI](https://cloud.ibm.com/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-getting-started&interface=cli#taxonomy-add-cli) or the [UI](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-getting-started#taxonomy-add-ui).
1. [Generate data from your taxonomy](/docs/{{site.data.keyword.subcollection}}?topic={{site.data.keyword.subcollection}}-data-generate).


## Aligning models by using the console
{: #model-train-ui}
{: ui}

1. From the **InstructLab Projects** [page](https://cloud.ibm.com/instructlab/projects){: external}, Click your project > **Aligned models** > **Align**.

1. Enter an alphanumeric name for the model, select the training data to use, and click **Alignx**. The state is `queued`, then `running`. Wait for the state to be `completed`. This process could take minutes or hours. When the alignment is complete, in the Object Storage bucket, a `trained_models` directory is created with logs for troubleshooting.



## Training models by using the CLI
{: #model-train-cli}
{: cli}


1. Get the ID for the data to use.

    ```sh
    ibmcloud ilab data list
    ```
    {: pre}

1. Run the command to start training the model with the generated data. Note the ID.

    ```sh
    ibmcloud ilab model train --name testmodel --data-id <data_id>
    ```
    {: pre}

1. Check the details of your data generation. Include the ID for the model. The state is `queued`, then `running`. Wait for the state to be `completed`. This process could take minutes or hours.

    ```sh
    ibmcloud ilab model get --id <model_id>
    ```
    {: pre}

    Example `model get` command with the `--output json` option.
    ```sh
    ibmcloud ilab model get --id daef9836-631f-4686-ad18-e0e6a0910f5d --output json 
    ```
    {: pre}

    Example JSON output
    ```json
    {                                                                                                                 
      "base_model": "granite-7b",                                                                                     
      "created_at": "2024-10-10T16:06:05.000Z",                                                                       
      "data_id": "8b1433c0-e375-4b00-b36d-2ad00697014e",                                                              
      "id": "daef9836-631f-4686-ad18-e0e6a0910f5d",                                                                   
      "model_metrics": {                                                                                              
        "mmlu": {                                                                                                     
          "overall_average": 0.51,                                                                                    
          "scores": {                                                                                                 
            "mmlu_abstract_algebra": 0.3,                                                                             
            "mmlu_anatomy": 0.43,                                                                                     
            "mmlu_astronomy": 0.49                                                                                    
          }                                                                                                           
        },                                                                                                            
        "mt_bench": {                                                                                                 
          "error_rate": 0.01,                                                                                         
          "overall_average": 6.86,                                                                                    
          "scores": {                                                                                                 
            "turn_one": 7.25,                                                                                         
            "turn_two": 6.47                                                                                          
          }                                                                                                           
        },                                                                                                            
        "mt_bench_branch": {                                                                                          
          "error_rate": 0.01,                                                                                         
          "improvements": {                                                                                           
            "compositional_skills/STEM/math/time_series/qna.yaml": 8.67,                                              
            "compositional_skills/extraction/invoice/csv/qna.yaml": 8.4                                               
          },                                                                                                          
          "no_change": {                                                                                              
            "compositional_skills/roleplay/explain_like_i_am/primary_schooler/qna.yaml": 0,                           
            "compositional_skills/writing/freeform/technical/proposal/qna.yaml": 0                                    
          },                                                                                                          
          "regressions": {                                                                                            
            "compositional_skills/extraction/inference/qualitative/sentiment/qna.yaml": -9,                           
            "compositional_skills/extraction/information/named_entities/places/qna.yaml": -9                          
          }                                                                                                           
        }                                                                                                             
      },                                                                                                              
      "name": "test",                                                                                                 
      "state": "completed",                                                                                           
      "status": "completed",                                                                                          
      "taxonomy_id": "e62ccea5-97e6-4568-86bf-2f359987b115"                                                           
    }
    ```
    {: screen}


When the state is `completed`, in the {{site.data.keyword.cos_short}} bucket, a `trained_models` directory is created with logs for troubleshooting.


## Training models by using the API
{: #model-train-api}
{: api}

1. Get the ID for the data to use.

    Example command.
    ```sh
    curl -X 'GET' \
      'https://us-east.instructlab.ibm.com/v1/data' \
      -H 'accept: application/json'
    ```
    {: pre}

    Example output.
    ```txt
    {
      "data": [
        {
          "id": "add785e6-a8c3-4f5f-ab89-c506a3f115da",
          "name": "example-data-1",
          "state": "",
          "status": "queued",
          "created_at": "2024-10-23T02:58:50.000Z",
          "taxonomy_id": "202a03c4-dcf1-432a-82b7-abecb2e019f7"
        }
      ]
    }
    ```
    {: screen}   

1. Run the command to start training the model with the generated data. Note the ID.

    Example command.
    ```sh
    curl -X 'POST' \
      'https://us-east.instructlab.ibm.com/v1/models' \
      -H 'accept: application/json' \
      -H 'Content-Type: application/json' \
      -d '{
      "name": "example-model-1",
      "data_id": "add785e6-a8c3-4f5f-ab89-c506a3f115da"
    }'
    ```
    {: pre}

    Example output.
    ```json
    {
      "id": "baa8cfb5-e306-4e15-869d-735b74b1919d",
      "name": "example-model-1",
      "state": "",
      "status": "queued",
      "created_at": "2024-10-23T02:58:50.000Z",
      "data_id": "add785e6-a8c3-4f5f-ab89-c506a3f115da",
      "base_model": "granite-7b",
      "taxonomy_id": "202a03c4-dcf1-432a-82b7-abecb2e019f7",
      "model_metrics": {
        "mmlu": {
          "overall_average": 0.3,
          "scores": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        },
        "mmlu_branch": {
          "error_rate": 0.4,
          "improvements": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "regressions": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "no_change": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        },
        "mt_bench": {
          "overall_average": 0.8,
          "error_rate": 0.6,
          "scores": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        },
        "mt_bench_branch": {
          "error_rate": 0.4,
          "improvements": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "regressions": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "no_change": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        }
      }
    }
    ```
    {: screen}   

1. Check the details of your data generation. Include the ID for the model. The state is `queued`, then `running`. Wait for the state to be `completed`. This process could take minutes or hours.

    Example command.
    ```sh
    curl -X 'GET' \
      'https://us-east.instructlab.ibm.com/v1/models/baa8cfb5-e306-4e15-869d-735b74b1919d' \
      -H 'accept: application/json'
    ```
    {: pre}

    Example output.
    ```json
    {
      "id": "baa8cfb5-e306-4e15-869d-735b74b1919d",
      "name": "example-model-1",
      "state": "",
      "status": "queued",
      "created_at": "2024-10-23T02:58:50.000Z",
      "data_id": "add785e6-a8c3-4f5f-ab89-c506a3f115da",
      "base_model": "granite-7b",
      "taxonomy_id": "202a03c4-dcf1-432a-82b7-abecb2e019f7",
      "model_metrics": {
        "mmlu": {
          "overall_average": 0.3,
          "scores": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        },
        "mmlu_branch": {
          "error_rate": 0.4,
          "improvements": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "regressions": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "no_change": {
            "additionalProp1": 1,
            "additionalProp3": 3,
            "additionalProp2": 2
          }
        },
        "mt_bench": {
          "overall_average": 0.8,
          "error_rate": 0.6,
          "scores": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        },
        "mt_bench_branch": {
          "error_rate": 0.4,
          "improvements": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "regressions": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          },
          "no_change": {
            "additionalProp1": 1,
            "additionalProp2": 2,
            "additionalProp3": 3
          }
        }
      }
    }
    ```
    {: screen}

When the state is `completed`, in the {{site.data.keyword.cos_short}} bucket, a `trained_models` directory is created with logs for troubleshooting.


## What's in my {{site.data.keyword.cos_short}} bucket after training?
{: #model-bucket}

After training the model, your {{site.data.keyword.cos_short}} bucket contains a `trained models` directory with the following files. 

Artifacts
:   These files contain the Phase 1 and Phase 2 checkpoint data and the model for each epoch. 

Eval
:   These files contain the evaluation metrics for the `mmlu`, `mmlu_branch`, `mt_bench` and `mt_bench_branch` benchmarks.

Logs
:   These files contain the {{site.data.keyword.instructlab_short}} execution logs and system details.

Model
:   These files contain the final outputted model in `safetensors` format. The contents of this directory are used by the model. 



## What's next?
{: #next-model}

Optional: You can deploy the model to RHEL-AI on {{site.data.keyword.cloud_notm}}.

1. [Install RHEL-AI on {{site.data.keyword.cloud_notm}}](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.4/html/installing/installing_ibm_cloud).

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
    # Replace variable with the {{site.data.keyword.cos_short}} bucket name
    CUSTOMER_BUCKET="XXX"
    # Replace variable with the {{site.data.keyword.cos_short}} endpoint
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
