---

copyright:
  years: 2024, 2025
lastupdated: "2025-03-28"

keywords: instructlab, ai, data, generate, default, settings

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Default service settings for {{site.data.keyword.short_name}}
{: #service-settings}

Review the default settings for {{site.data.keyword.short_name}}. These settings cannot be modified. 
{: shortdesc}

## Training settings
{: #training-defaults}

Training strategy
: Specifies the training strategy that is used. 
:  - `--strategy=lab-multiphase`

Base Model to be trained
: Specifies the base model to be trained
: - Version 1.4: `--model-path=granite-3.1-8b-starter-v1`
: - Version 1.3: `--model-path=granite-8b-starter`
: - Version 1.2: `--model-path=granite-7b-starter`

IBM Granite is provided under the Apache License 2.0. For more information, see the [Apache License documentation](https://www.apache.org/licenses/LICENSE-2.0){: external}
{: important}

MT-Bench judge 
:   Specifies the MT-Bench judge model. This parameter is the absolute path to the local judge model directory. If necessary, you can download the model by running `ilab model download`.
:   - Default judge model: `prometheus-8x7b-v2-0`
:   - Parameter (includes directory path): `--phased-mt-bench-judge=/instructlab/models/prometheus-8x7b-v2-0`; config: `train.phased_mt_bench_judge`

Training batch size per phase
:   Specifies the total size of a training batch over all GPUs, per phase. 
:   - Phase 1: `--phased-phase1-effective-batch-size=128`; config:`train.phased_phase1_effective_batch_size`,
:   - Phase 2: `--phased-phase2-effective-batch-size=3840`;  config:`train.phased_phase2_effective_batch_size`

Epochs per phase
:   Specifies the number of epochs to run for each phase of end-to-end training. 
:   - Knowledge: Phase 1: `--phased-phase1-num-epochs=6`; config: `train.phased_phase1_num_epochs`
:   - Skills: Phase 2: `--phased-phase2-num-epochs=10`; config: `train.phased_phase2_num_epochs`


Padding-free transformer
:   Specifies whether training is performed on a padding-free transformer. 
:   - `--is-padding-free=true`; config: `train.is_padding_free`

## Synthetic data generation (SDG) settings
{: #sdg-defaults} 

Teacher Model
:   Specifies the model used during synthetic data generation. 
:   - Default teacher model: `mixtral-8x7b-instruct-v0-1`
:   - Parameter (includes directory path): `--model=/instructlab/models/mixtral-8x7b-instruct-v0-1`; config: `generate.pipeline`

Instructions generated per seed example
:   Specifies the number of instructions to generate for each seed example. Each example maps to sample Q&A pairs for new skills. Examples are generated with both the same Q&A pairs and chunks of the knowledge document, so that the resulting data set is typically larger for a knowledge addition for the same value.
:   `--sdg-scale-factor=30`

Data generation pipeline
:   Specifies the data generation pipeline to use.
:   Pipeline: `agentic`
:   Parameter (includes directory path): `--pipeline=/instructlab/sdg/pipelines/agentic`; config: `generate.teacher.model_path`

## Model settings
{: #model-defaults}

Context window
:   Specifies the maximum amount of bytes that be can sent in a prompt. The content window size supported is 4096 bytes.
:   To find this setting, open `config.json` under `trained_models/$TRAINING_JOB_ID/model/` and locate the `max_position_embeddings` field, for example, `"max_position_embeddings": 4096`.
