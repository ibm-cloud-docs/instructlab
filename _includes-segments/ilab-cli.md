## Data
{: #ilab-data-cli}

Operations dealing with synthetic data.

```sh
ibmcloud ilab data --help
```


### `ibmcloud ilab data generate`
{: #ilab-cli-data-generate-command}

Generate synthetic data based on a specified taxonomy.

```sh
ibmcloud ilab data generate [--name NAME] [--taxonomy-id TAXONOMY-ID]
```


#### Command options
{: #ilab-data-generate-cli-options}

`--name` (string)
:   TODO.

`--taxonomy-id` (string)
:   TODO.

#### Example
{: #ilab-data-generate-examples}

```sh
ibmcloud ilab data generate \
    --name exampleString \
    --taxonomy-id exampleString
```
{: pre}

### `ibmcloud ilab data list`
{: #ilab-cli-data-list-command}

Get details about a collection of synthetic data sets.

```sh
ibmcloud ilab data list
```


#### Example
{: #ilab-data-list-examples}

```sh
ibmcloud ilab data list
```
{: pre}

### `ibmcloud ilab data status`
{: #ilab-cli-data-status-command}

Get details about a synthetic data resource, including the generation status.

```sh
ibmcloud ilab data status --id ID
```


#### Command options
{: #ilab-data-status-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-data-status-examples}

```sh
ibmcloud ilab data status \
    --id 66830e653724e36acaf47d65
```
{: pre}

### `ibmcloud ilab data delete`
{: #ilab-cli-data-delete-command}

Delete a synthetic data set. If the data is still being generated, the process will be canceled.

```sh
ibmcloud ilab data delete --id ID
```


#### Command options
{: #ilab-data-delete-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-data-delete-examples}

```sh
ibmcloud ilab data delete \
    --id 66830e653724e36acaf47d65
```
{: pre}

### `ibmcloud ilab data cancel`
{: #ilab-cli-data-cancel-command}

Cancel the ongoing generation of synthetic data. If generation is complete, this will return an error.

```sh
ibmcloud ilab data cancel --id ID
```


#### Command options
{: #ilab-data-cancel-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-data-cancel-examples}

```sh
ibmcloud ilab data cancel \
    --id 66830e653724e36acaf47d65
```
{: pre}

## Model
{: #ilab-model-cli}

Operations dealing with models.

```sh
ibmcloud ilab model --help
```


### `ibmcloud ilab model train`
{: #ilab-cli-model-train-command}

Train a model with a given set of synthetic data.

```sh
ibmcloud ilab model train [--name NAME] [--synthetic-data-id SYNTHETIC-DATA-ID]
```


#### Command options
{: #ilab-model-train-cli-options}

`--name` (string)
:   TODO.

`--synthetic-data-id` (string)
:   TODO - include a smart default may be used.

#### Example
{: #ilab-model-train-examples}

```sh
ibmcloud ilab model train \
    --name exampleString \
    --synthetic-data-id exampleString
```
{: pre}

### `ibmcloud ilab model list`
{: #ilab-cli-model-list-command}

Get details about a collection of models.

```sh
ibmcloud ilab model list
```


#### Example
{: #ilab-model-list-examples}

```sh
ibmcloud ilab model list
```
{: pre}

### `ibmcloud ilab model status`
{: #ilab-cli-model-status-command}

Get details about a model, including the training status.

```sh
ibmcloud ilab model status --id ID
```


#### Command options
{: #ilab-model-status-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-model-status-examples}

```sh
ibmcloud ilab model status \
    --id 66830e653724e36acaf47d69
```
{: pre}

### `ibmcloud ilab model delete`
{: #ilab-cli-model-delete-command}

Delete a model. If the model is still being trained, the process will be canceled.

```sh
ibmcloud ilab model delete --id ID
```


#### Command options
{: #ilab-model-delete-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-model-delete-examples}

```sh
ibmcloud ilab model delete \
    --id 66830e653724e36acaf47d69
```
{: pre}

### `ibmcloud ilab model cancel`
{: #ilab-cli-model-cancel-command}

Cancel the ongoing training of a model. If training is complete, this will return an error.

```sh
ibmcloud ilab model cancel --id ID
```


#### Command options
{: #ilab-model-cancel-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-model-cancel-examples}

```sh
ibmcloud ilab model cancel \
    --id 66830e653724e36acaf47d69
```
{: pre}

## Taxonomy
{: #ilab-taxonomy-cli}

Operations dealing with taxonomies.

```sh
ibmcloud ilab taxonomy --help
```


### `ibmcloud ilab taxonomy upload`
{: #ilab-cli-taxonomy-upload-command}

Upload a TAR file containing the taxonomy to store.

```sh
ibmcloud ilab taxonomy upload [--access-key-id ACCESS-KEY-ID] [--secret-access-key SECRET-ACCESS-KEY] [--bucket BUCKET] [--endpoint ENDPOINT] [--region REGION]
```


#### Command options
{: #ilab-taxonomy-upload-cli-options}

`--access-key-id` (string)
:   HMAC credentials to COS bucket.

`--secret-access-key` (string)
:   HMAC credentials to COS bucket.

`--bucket` (string)
:   Bucket the taxonomy lives in.

`--endpoint` (string)
:   Endpoint to COS bucket.

`--region` (string)
:   Region to COS bucket.

#### Example
{: #ilab-taxonomy-upload-examples}

```sh
ibmcloud ilab taxonomy upload \
    --access-key-id exampleString \
    --secret-access-key exampleString \
    --bucket exampleString \
    --endpoint exampleString \
    --region exampleString
```
{: pre}

### `ibmcloud ilab taxonomy list`
{: #ilab-cli-taxonomy-list-command}

Get details about a collection of taxonomies.

```sh
ibmcloud ilab taxonomy list
```


#### Example
{: #ilab-taxonomy-list-examples}

```sh
ibmcloud ilab taxonomy list
```
{: pre}

### `ibmcloud ilab taxonomy status`
{: #ilab-cli-taxonomy-status-command}

Get details about a taxonomy resource.

```sh
ibmcloud ilab taxonomy status --id ID
```


#### Command options
{: #ilab-taxonomy-status-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-taxonomy-status-examples}

```sh
ibmcloud ilab taxonomy status \
    --id 66830e653724e36acaf47d69
```
{: pre}

### `ibmcloud ilab taxonomy delete`
{: #ilab-cli-taxonomy-delete-command}

Delete a taxonomy.

```sh
ibmcloud ilab taxonomy delete --id ID
```


#### Command options
{: #ilab-taxonomy-delete-cli-options}

`--id` (string)
:   TODO. Required.

#### Example
{: #ilab-taxonomy-delete-examples}

```sh
ibmcloud ilab taxonomy delete \
    --id 66830e653724e36acaf47d69
```
{: pre}

