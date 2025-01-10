---

copyright:
  years: 2024, 2025
lastupdated: "2025-01-09"

keywords: instructlab, ai, data, generate, default, settings

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Default service settings for InstructLab
{: #service-settings}

Review the default settings for InstructLab. These settings cannot be modified. 
{: shortdesc}

## Training settings
{: #training-defaults}

Training strategy
: Specifies the training strategy that is used. 
:  - `--strategy=lab-multiphase`

Base Model to be trained
: Specifies the base model to be trained
: - Version 1.3: `--model-path=granite-8b-starter`
: - Version 1.2: `--model-path=granite-7b-starter`

MT-Bench judge 
:   Specifies the MT-Bench judge model. This parameter is the absolute path to the local judge model directory. If necessary, you can download the model by running `ilab model download`.
:   - Default judge model: `prometheus-8x7b-v2-0`
:   - Parameter (includes directory path): `--phased-mt-bench-judge=/instructlab/models/prometheus-8x7b-v2-0`; config: `train.phased_mt_bench_judge`

Training batch size per phase
:   Specifies the total size of a training batch over all GPUs, per phase. 
:   - Phase 1: `--phased-phase1-effective-batch-size=128`; config:`train.phased_phase1_effective_batch_size`
:   - Phase 2: `--phased-phase2-effective-batch-size=3840`;  config:`train.phased_phase2_effective_batch_size`

Epochs per phase
:   Specifies the number of epochs to run for each phase of end-to-end training. 
:   - Phase 1: `--phased-phase1-num-epochs=6`; config: `train.phased_phase1_num_epochs`
:   - Phase 2: `--phased-phase2-num-epochs=10`; config: `train.phased_phase2_num_epochs`


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
