---

copyright:
  years: 2025
lastupdated: "2025-03-13"

keywords: instructlab, cli, plugin

---

{{site.data.keyword.attribute-definition-list}}

# InstructLab CLI
{: #ilab-cli}

## Globals
{: #ilab-globals}

### Options
{: #ilab-global-options}

`--project-id` (string)
:   The InstructLab project ID.

`--output` (string)
:   Choose an output format - can be 'json', 'yaml', or 'table'. Defaults to 'table'.

`-j`, `--jmes-query` (string)
:   Provide a JMESPath query to customize output.

`-q`, `--quiet`
:   Suppresses verbose messages.

`-v`, `--version`
:   Prints the plug-in version.

#### Example
{: #ilab-global-options-example}

```sh
ibmcloud ilab
    --project-id=project_id \
    --output=json \
    --jmes-query="[:10]" \
    --quiet
```
{: pre}

Note: This example only demonstrates the global options available to all sub-commands and is not a valid command itself.

### `ibmcloud ilab config`
{: #ilab-cli-config-command}

Global parameters can also be stored in persistent configuration so that they do not need to be manually specified each time the plug-in is invoked. Each parameter can be configured with the `config` command and its subcommands.

```sh
ibmcloud ilab config
```

### `ibmcloud ilab config set`
{: #ilab-cli-config-set-command}

Set a new config value for a specific option. Each subcommand of the `set` command maps to a global option. Each subcommand accepts a single argument, the string representation of the value to store for the option.

```sh
ibmcloud ilab config set <option> <value>
```

#### Examples
{: #ilab-config-set-command-examples}

### `ibmcloud ilab config get`
{: #ilab-cli-config-get-command}

Print out the currently set value for a specific option. Each subcommand of the `get` command maps to a global option.

```sh
ibmcloud ilab config get <option>
```

#### Examples
{: #ilab-config-get-command-examples}

### `ibmcloud ilab config unset`
{: #ilab-cli-config-unset-command}

Unset the currently set value for a specific option. Each subcommand of the `unset` command maps to a global option.

The subcommands available for this service are: .

```sh
ibmcloud ilab config unset <option>
```

#### Examples
{: #ilab-config-unset-command-examples}

### `ibmcloud ilab config list`
{: #ilab-cli-config-list-command}

List out all of the currently set config values.

```sh
ibmcloud ilab config list
```

#### Examples
{: #ilab-config-list-command-examples}

```sh
ibmcloud ilab config list
```
{: pre}

## Taxonomy
{: #ilab-taxonomy-cli}

Operations to manage taxonomies.

```sh
ibmcloud ilab taxonomy --help
```


### `ibmcloud ilab taxonomy add`
{: #ilab-cli-taxonomy-add-command}

Adds a taxonomy resource to a Cloud Object Storage bucket.

If you are using Windows or another non-Unix system, additional steps are required to add a taxonomy. Follow the steps in this [troubleshooting document](/docs/instructlab?topic=ts-no-new-leaf-nodes).
{: important}

```sh
ibmcloud ilab taxonomy add --name NAME --taxonomy-path-cos TAXONOMY-PATH-COS [--taxonomy-path TAXONOMY-PATH] [--cos-bucket-information COS-BUCKET-INFORMATION | --cos-id COS-ID --cos-bucket COS-BUCKET --cos-endpoint COS-ENDPOINT] [--secrets-manager-config SECRETS-MANAGER-CONFIG | --secrets-manager-git-url SECRETS-MANAGER-GIT-URL --secrets-manager-git-id SECRETS-MANAGER-GIT-ID]
```


#### Command options
{: #ilab-taxonomy-add-cli-options}

`--name` (string)
:   The name to give a taxonomy resource. Required.

`--taxonomy-path-cos` (string)
:   The path to store the taxonomy resource in the Cloud Object Storage bucket. Required.

`--taxonomy-path` (string)
:   The absolute or relative path to a local taxonomy resource.

`--cos-bucket-information` ([`CosBucketInformation`](#cli-cos-bucket-information-example-schema))
:   COS bucket information. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--cos-bucket-information=@path/to/file.json`.

`--secrets-manager-config` ([`SecretsManagerConfig`](#cli-secrets-manager-config-example-schema))
:   Secrets Manager Configuration object. This JSON option can instead be provided by setting individual fields with other options. It is mutually exclusive with those options.

    Provide a JSON string option or specify a JSON file to read from by providing a filepath option that begins with a `@`, e.g. `--secrets-manager-config=@path/to/file.json`.

`--cos-id` (string)
:   The service instance ID of the Cloud Object Storage instance. Only needed when auto-creating a Cloud Object Storage bucket. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`-b`, `--cos-bucket` (string)
:   The Cloud Object Storage bucket where the taxonomy resource will be stored. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`-e`, `--cos-endpoint` (string)
:   The endpoint to the Cloud Object Storage bucket. This option provides a value for a sub-field of the JSON option 'cos-bucket-information'. It is mutually exclusive with that option.

`--secrets-manager-git-url` (string)
:   The URL to a Secrets Manager instance to retrieve user-defined secrets. This option provides a value for a sub-field of the JSON option 'secrets-manager-config'. It is mutually exclusive with that option.

`--secrets-manager-git-id` (string)
:   The Secrets Manager ID that points to a git personal authorization token and git URL in JSON format. This option provides a value for a sub-field of the JSON option 'secrets-manager-config'. It is mutually exclusive with that option.

#### Examples
{: #ilab-taxonomy-add-examples}

```sh
ibmcloud ilab taxonomy add \
    --name example-taxonomy-1 \
    --taxonomy-path-cos taxonomies/taxonomy.tar.gz \
    --taxonomy-path exampleString \
    --cos-bucket-information '{"service_instance_id": "628e4348-2183-42fa-a03a-6f0f78453530", "bucket": "example-bucket-1", "endpoint": "https://s3.us-east.cloud-object-storage.appdomain.cloud"}' \
    --secrets-manager-config '{"url": "https://12345678-abcd-1234-5678-abcdefghijkl.us-east.secrets-manager.appdomain.cloud", "git_id": "d9428888-122b-11e1-b85c-61cd3cbb3210"}'
```
{: pre}

Alternatively, granular options are available for the sub-fields of JSON string options:
```sh
ibmcloud ilab taxonomy add \
    --name example-taxonomy-1 \
    --taxonomy-path-cos taxonomies/taxonomy.tar.gz \
    --taxonomy-path exampleString \
    --cos-id 628e4348-2183-42fa-a03a-6f0f78453530 \
    --cos-bucket example-bucket-1 \
    --cos-endpoint https://s3.us-east.cloud-object-storage.appdomain.cloud \
    --secrets-manager-git-url https://12345678-abcd-1234-5678-abcdefghijkl.us-east.secrets-manager.appdomain.cloud \
    --secrets-manager-git-id d9428888-122b-11e1-b85c-61cd3cbb3210
```
{: pre}

### `ibmcloud ilab taxonomy list`
{: #ilab-cli-taxonomy-list-command}

Lists the details of a collection of taxonomy resources.

```sh
ibmcloud ilab taxonomy list
```


#### Example
{: #ilab-taxonomy-list-examples}

```sh
ibmcloud ilab taxonomy list
```
{: pre}

#### Default JMESPath
{: #ilab-taxonomy-list-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `taxonomies[*]` |
| Error | Default | - |
|  | Table | - |
| All pages | Default | - |
|  | Table | - |
{: caption="Table 1. Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud ilab taxonomy get`
{: #ilab-cli-taxonomy-get-command}

Gets the details of a taxonomy resource.

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

Deletes a taxonomy resource.

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

## Data
{: #ilab-data-cli}

Operations to manage data.

```sh
ibmcloud ilab data --help
```


### `ibmcloud ilab data generate`
{: #ilab-cli-data-generate-command}

Generates data against a specified taxonomy resource.

```sh
ibmcloud ilab data generate --name NAME --taxonomy-id TAXONOMY-ID
```


#### Command options
{: #ilab-data-generate-cli-options}

`--name` (string)
:   The name to give a data resource. Required.

`-t`, `--taxonomy-id` (string)
:   The taxonomy ID to generate a data resource against. Required.

#### Example
{: #ilab-data-generate-examples}

```sh
ibmcloud ilab data generate \
    --name example-data-1 \
    --taxonomy-id 202a03c4-dcf1-432a-82b7-abecb2e019f7
```
{: pre}

### `ibmcloud ilab data list`
{: #ilab-cli-data-list-command}

Lists the details of a collection of data resources.

```sh
ibmcloud ilab data list
```


#### Example
{: #ilab-data-list-examples}

```sh
ibmcloud ilab data list
```
{: pre}

#### Default JMESPath
{: #ilab-data-list-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `data[*]` |
| Error | Default | - |
|  | Table | - |
| All pages | Default | - |
|  | Table | - |
{: caption="Table 1. Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud ilab data get`
{: #ilab-cli-data-get-command}

Gets the details of a data resource.

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

#### Default JMESPath
{: #ilab-data-get-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{id:id,name:name,state:state,status:status,created_at:created_at,completed_at:completed_at,taxonomy_id:taxonomy_id}` |
| Error | Default | - |
|  | Table | - |
| All pages | Default | - |
|  | Table | - |
{: caption="Table 1. Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud ilab data delete`
{: #ilab-cli-data-delete-command}

Deletes a data resource.

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

Cancels the generation of a data resource.

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

Operations to manage models.

```sh
ibmcloud ilab model --help
```


### `ibmcloud ilab model train`
{: #ilab-cli-model-train-command}

Trains a model resource against a specified data resource.

```sh
ibmcloud ilab model train --name NAME --data-id DATA-ID
```


#### Command options
{: #ilab-model-train-cli-options}

`--name` (string)
:   The name to give a model resource. Required.

`-d`, `--data-id` (string)
:   The data ID to train a model against. Required.

#### Example
{: #ilab-model-train-examples}

```sh
ibmcloud ilab model train \
    --name example-model-1 \
    --data-id add785e6-a8c3-4f5f-ab89-c506a3f115da
```
{: pre}

### `ibmcloud ilab model list`
{: #ilab-cli-model-list-command}

Lists the details of a collection of model resources.

```sh
ibmcloud ilab model list
```


#### Example
{: #ilab-model-list-examples}

```sh
ibmcloud ilab model list
```
{: pre}

#### Default JMESPath
{: #ilab-model-list-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `models[*]` |
| Error | Default | - |
|  | Table | - |
| All pages | Default | - |
|  | Table | - |
{: caption="Table 1. Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud ilab model get`
{: #ilab-cli-model-get-command}

Gets the details of a model resource.

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

#### Default JMESPath
{: #ilab-model-get-default-jmespath}

A JMESPath query will be applied to this output of this command by default, if one is not provided by the user. The exact query will depend on the scenario and the output format requested.
You can see the condition for each default JMESPath query in the following table:

| Response | Output | Query |
| -------- | ------ | ----- |
| Success | Default | - |
|  | Table | `{base_model:base_model,created_at:created_at,completed_at:completed_at,data_id:data_id,id:id,name:name,state:state,status:status,taxonomy_id:taxonomy_id}` |
| Error | Default | - |
|  | Table | - |
| All pages | Default | - |
|  | Table | - |
{: caption="Table 1. Default JMESPath" caption-side="bottom"}

If a custom JMESPath query is provided, it will replace any of the JMESPath in the table above.

### `ibmcloud ilab model delete`
{: #ilab-cli-model-delete-command}

Delete a model resource.

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

Cancels the training of a model resource.

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

## Schema examples
{: #ilab-schema-examples}

The following schema examples represent the data that you need to specify for a command option. These examples model the data structure and include placeholder values for the expected value type. When you run a command, replace these values with the values that apply to your environment as appropriate.

### CosBucketInformation
{: #cli-cos-bucket-information-example-schema}

The following example shows the format of the CosBucketInformation object.

```json

{
  "service_instance_id" : "628e4348-2183-42fa-a03a-6f0f78453530",
  "bucket" : "example-bucket-1",
  "endpoint" : "https://s3.us-east.cloud-object-storage.appdomain.cloud"
}
```
{: codeblock}

### SecretsManagerConfig
{: #cli-secrets-manager-config-example-schema}

The following example shows the format of the SecretsManagerConfig object.

```json

{
  "url" : "https://12345678-abcd-1234-5678-abcdefghijkl.us-east.secrets-manager.appdomain.cloud",
  "git_id" : "d9428888-122b-11e1-b85c-61cd3cbb3210"
}
```
{: codeblock}
