---

copyright:
  years: 2024, 2025
lastupdated: "2025-09-26"

keywords: instructlab, ai, data, generate, default, settings

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Default service settings for {{site.data.keyword.short_name}}
{: #service-settings}

{{site.data.keyword.instructlab_full_notm}} includes predefined settings to optimize model training, data generation, and more. By configuring these settings, {{site.data.keyword.instructlab_full_notm}} allows you to focus on improving your model. Review the default settings for {{site.data.keyword.short_name}}. These settings can't be modified.
{: shortdesc}

IBM Granite is provided under the Apache License 2.0. For more information, see the [Apache License documentation](https://www.apache.org/licenses/LICENSE-2.0){: external}
{: important}

## Training settings
{: #training-defaults}

| Setting | Description | Value |
| --- | --- | --- |
| Training strategy | Specifies the training strategy that is used. | `--strategy=lab-multiphase` |
| Base Model | Specifies the base model to be trained. | `--model-path=granite-3.1-8b-starter-v2.1` |
| MT-Bench judge  | Specifies the MT-Bench judge model. This parameter is the absolute path to the local judge model directory. If necessary, you can download the model by running `ilab model download`. | - Default judge model: `prometheus-8x7b-v2-0`  \n - Parameter (includes directory path): `--phased-mt-bench-judge=/instructlab/models/prometheus-8x7b-v2-0`; config: `train.phased_mt_bench_judge` |
| Epochs per phase | Specifies the number of epochs to run for each phase of end-to-end training. | - Knowledge: Phase 1: `--phased-phase1-num-epochs=7`; config: `train.phased_phase1_num_epochs`  \n - Skills: Phase 2: `--phased-phase2-num-epochs=7`; config: `train.phased_phase2_num_epochs` |
| Padding-free transformer | Specifies whether training is performed on a padding-free transformer. | `--is-padding-free=false`; config: `train.is_padding_free` |
| Use dolomite | Specifies whether to use dolomite. | `--use-dolomite=false` |
| Learning rate | Specifies the learning rate for each phase. | - `--phased_phase_1_learning_rate=2e-5`  \n - `--phased_phase_2_learning_rate=2e-5` |
| Max batch length | Specifies the max batch length. | 45k |
| Max sequence length | Specifies the max sequence length. | 42k |
| Replay buffer filter | The replay buffer is filtered for samples larger than 10k to keep training within the expected alignment times. | 10k |
| Replay buffer | Specifies the size of the replay buffer. | 6.9 GB |
{: caption="Training settings for {{site.data.keyword.instructlab_short}}" caption-side="bottom"}

## Synthetic data generation (SDG) settings
{: #sdg-defaults} 

| Setting | Description | Value |
| --- | --- | --- |
| Teacher Model | Specifies the model used during synthetic data generation. | - Default teacher model: `mixtral-8x7b-instruct-v0-1`.  \n - Parameter (includes directory path): `--model=/instructlab/models/mixtral-8x7b-instruct-v0-1`; config: `generate.pipeline` |
| Instructions generated per seed example | Specifies the number of instructions to generate for each seed example. Each example maps to sample Q&A pairs for new skills. Examples are generated with both the same Q&A pairs and chunks of the knowledge document, so that the resulting data set is typically larger for a knowledge addition for the same value. | `--sdg-scale-factor=30` |
| Data generation pipeline | Specifies the data generation pipeline to use. | - Pipeline: `agentic`.  \n - Parameter (includes directory path): `--pipeline=/instructlab/sdg/pipelines/agentic`; config: `generate.teacher.model_path` |
| Batch size | Specifies the batch size. | 32 |
| CPUs | Specifies the number of CPUs. | 4 |
{: caption="SDG settings for {{site.data.keyword.instructlab_short}}" caption-side="bottom"}

## Model settings
{: #model-defaults}


| Setting | Description | Value |
| --- | --- | --- |
| Context window | Specifies the maximum amount of bytes that be can sent in a prompt. To find this setting, open `config.json` under `trained_models/$TRAINING_JOB_ID/model/` and locate the `max_position_embeddings` field, for example, `"max_position_embeddings": 4096`. | The content window size supported is 4096 bytes. |
| Model size | Specifies the size of the model | 32 GB |
| Safetensors files | Specifies the number of Safetensors files. | 7 |
{: caption="Model settings for {{site.data.keyword.instructlab_short}}" caption-side="bottom"}
