## Data
{: #ilab-data-cli}

Operations dealing with data.

```sh
ibmcloud ilab data --help
```


### `ibmcloud ilab data generate`
{: #ilab-cli-data-generate-command}

Generate data based on a specified taxonomy.

```sh
ibmcloud ilab data generate [--name NAME] [--taxonomy-id TAXONOMY-ID]
```


#### Command options
{: #ilab-data-generate-cli-options}

`--name` (string)
:   Name to give the data run.

`--taxonomy-id` (string)
:   Taxonomy ID that the data will be ran against.

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

Get details about a collection of data sets.

```sh
ibmcloud ilab data list
```


#### Example
{: #ilab-data-list-examples}

```sh
ibmcloud ilab data list
```
{: pre}

### `ibmcloud ilab data get`
{: #ilab-cli-data-get-command}

Get details about a data resource, including the generation details.

```sh
ibmcloud ilab data get --id ID
```


#### Command options
{: #ilab-data-get-cli-options}

`--id` (string)
:   Unique Identifier to data run. Required.

#### Example
{: #ilab-data-get-examples}

```sh
ibmcloud ilab data get \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
```
{: pre}

### `ibmcloud ilab data delete`
{: #ilab-cli-data-delete-command}

Delete a data set. If the data is still being generated, the process will be canceled.

```sh
ibmcloud ilab data delete --id ID
```


#### Command options
{: #ilab-data-delete-cli-options}

`--id` (string)
:   Unique Identifier to data run. Required.

#### Example
{: #ilab-data-delete-examples}

```sh
ibmcloud ilab data delete \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
```
{: pre}

### `ibmcloud ilab data cancel`
{: #ilab-cli-data-cancel-command}

Cancel the ongoing generation of data. If generation is complete, this will return an error.

```sh
ibmcloud ilab data cancel --id ID
```


#### Command options
{: #ilab-data-cancel-cli-options}

`--id` (string)
:   Unique Identifier to data run. Required.

#### Example
{: #ilab-data-cancel-examples}

```sh
ibmcloud ilab data cancel \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
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

Train a model with a given set of data.

```sh
ibmcloud ilab model train [--name NAME] [--data-id DATA-ID]
```


#### Command options
{: #ilab-model-train-cli-options}

`--name` (string)
:   Name to give the model train run.

`--data-id` (string)
:   Data ID that the model train run will be ran against.

#### Example
{: #ilab-model-train-examples}

```sh
ibmcloud ilab model train \
    --name exampleString \
    --data-id exampleString
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

### `ibmcloud ilab model get`
{: #ilab-cli-model-get-command}

Get details about a model, including the training details.

```sh
ibmcloud ilab model get --id ID
```


#### Command options
{: #ilab-model-get-cli-options}

`--id` (string)
:   Unique Identifier to a model training run. Required.

#### Example
{: #ilab-model-get-examples}

```sh
ibmcloud ilab model get \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
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
:   Unique Identifier to a model training run. Required.

#### Example
{: #ilab-model-delete-examples}

```sh
ibmcloud ilab model delete \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
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
:   Unique Identifier to a model training run. Required.

#### Example
{: #ilab-model-cancel-examples}

```sh
ibmcloud ilab model cancel \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
```
{: pre}

## Taxonomy
{: #ilab-taxonomy-cli}

Operations dealing with taxonomies.

```sh
ibmcloud ilab taxonomy --help
```


### `ibmcloud ilab taxonomy add`
{: #ilab-cli-taxonomy-add-command}

TARs and adds a taxonomy to COS.

```sh
ibmcloud ilab taxonomy add [--name NAME] [--taxonomy-path TAXONOMY-PATH] [--taxonomy-path-cos TAXONOMY-PATH-COS] [--cos-bucket-information COS-BUCKET-INFORMATION | --cos-bucket-information-access-key-id COS-BUCKET-INFORMATION-ACCESS-KEY-ID --cos-bucket-information-secret-access-key COS-BUCKET-INFORMATION-SECRET-ACCESS-KEY --cos-bucket-information-bucket COS-BUCKET-INFORMATION-BUCKET --cos-bucket-information-endpoint COS-BUCKET-INFORMATION-ENDPOINT --cos-bucket-information-region COS-BUCKET-INFORMATION-REGION]
```


#### Command options
{: #ilab-taxonomy-add-cli-options}

`--name` (string)
:   Name to give the taxonomy resource.

`--taxonomy-path` (string)
:   An absolute or relative path to the taxonomy locally.

`--taxonomy-path-cos` (string)
:   Taxonomy path to be stored in COS. For example taxonomy.tar.gz. Defaults to taxonomies/taxonomy-$epochtime.tar.gz.

`--cos-bucket-information` ([`COSBucketInformation`](#cli-cos-bucket-information-example-schema))
:   Information needed to identify a specific COS bucket. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--cos-bucket-information=@path/to/file.json`.

`--cos-bucket-information-access-key-id` (string)
:   HMAC credentials to COS bucket. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`--cos-bucket-information-secret-access-key` (string)
:   HMAC credentials to COS bucket. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`--cos-bucket-information-bucket` (string)
:   Bucket the taxonomy lives in. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`--cos-bucket-information-endpoint` (string)
:   Endpoint to COS bucket. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`--cos-bucket-information-region` (string)
:   Region to COS bucket. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

#### Examples
{: #ilab-taxonomy-add-examples}

```sh
ibmcloud ilab taxonomy add \
    --name exampleString \
    --taxonomy-path exampleString \
    --taxonomy-path-cos exampleString \
    --cos-bucket-information '{"access_key_id": "exampleString", "secret_access_key": "exampleString", "bucket": "exampleString", "endpoint": "exampleString", "region": "exampleString"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud ilab taxonomy add \
    --name exampleString \
    --taxonomy-path exampleString \
    --taxonomy-path-cos exampleString \
    --cos-bucket-information-access-key-id exampleString \
    --cos-bucket-information-secret-access-key exampleString \
    --cos-bucket-information-bucket exampleString \
    --cos-bucket-information-endpoint exampleString \
    --cos-bucket-information-region exampleString
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

### `ibmcloud ilab taxonomy get`
{: #ilab-cli-taxonomy-get-command}

Get details about a taxonomy resource.

```sh
ibmcloud ilab taxonomy get --id ID
```


#### Command options
{: #ilab-taxonomy-get-cli-options}

`--id` (string)
:   Unique Identifier to a taxonomy. Required.

#### Example
{: #ilab-taxonomy-get-examples}

```sh
ibmcloud ilab taxonomy get \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
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
:   Unique Identifier to a taxonomy. Required.

#### Example
{: #ilab-taxonomy-delete-examples}

```sh
ibmcloud ilab taxonomy delete \
    --id 817bc95a-fef0-4039-b936-e0b6fb17b723
```
{: pre}

## Schema examples
{: #ilab-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

### COSBucketInformation
{: #cli-cos-bucket-information-example-schema}

The following example shows the format of the COSBucketInformation object.

```json

{
  "access_key_id" : "exampleString",
  "secret_access_key" : "exampleString",
  "bucket" : "exampleString",
  "endpoint" : "exampleString",
  "region" : "exampleString"
}
```
{: codeblock}
