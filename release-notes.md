---

copyright: 
  years: 2024, 2025
lastupdated: "2025-09-25"

keywords: release notes

subcollection: instructlab

content-type: release-note

---

{{site.data.keyword.attribute-definition-list}}


# Release notes for {{site.data.keyword.short_name}}
{: #release-notes}

Use the release notes to learn about the latest changes to the documentation that are grouped by month.
{: shortdesc}

Looking for {{site.data.keyword.cloud_notm}} status, platform announcements, security bulletins, or maintenance notifications? See [{{site.data.keyword.cloud_notm}} status](https://cloud.ibm.com/status?selected=status).
{: tip}

## September 2025
{: #sept25}


### 23 September 2025
{: #23aug25}
{: release-note}

Version 1.5 of {{site.data.keyword.product_name}} is available
:   For the best results, run training on newly generated synthetic data with version 1.5. Review the updated [service settings](/docs/instructlab?topic=instructlab-service-settings) in 1.5.
:   For more information, see the [RHEL AI documentation](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.5/html/release_notes/rhelai_release_notes#rhelai_release_notes){: external} and the [known issues](https://issues.redhat.com/browse/RHELAI-3604){: external}

New base model
:   {{site.data.keyword.product_name}} now uses the `granite-3.1-8b-starter-v2.1` model. For more information, see the [model specifications](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux_ai/1.5/html/building_and_maintaining_your_environment/download_models){: external}.


## August 2025
{: #aug25}


### 22 August 2025
{: #2aug25}
{: release-note}

New! Import your own training data
:   You can now import your own training data for training models. When you import your own training data, you can specify previously generated data IDs, or add knowledge and skills files to a data generation job by uploading files from {{site.data.keyword.cos_short}} or your local machine. For more information, see [Generating data](/docs/instructlab?topic=instructlab-data-generate).

New! Taxonomy validation
:   When you upload a taxonomy to {{site.data.keyword.short_name}}, it's now checked for formatting and syntax errors. Also, if you reference external knowledge documents in your `qna.yaml` files, {{site.data.keyword.short_name}} checks for access to those files. Additionally, {{site.data.keyword.short_name}} checks for the proper service authorizations for services like {{site.data.keyword.cos_short}} and {{site.data.keyword.secrets-manager_short}}.

{{site.data.keyword.short_name}} CLI plug-in version `0.0.24`
:   Version `0.0.24` of the plug-in adds support for importing your own training data to the `data generate` command. For more information, see [Generating data](/docs/instructlab?topic=instructlab-data-generate) or run `ibmcloud ilab data generate --help` to see the new options.

## May 2025
{: #may25}


### 09 May 2025
{: #09may25}
{: release-note}


New! Private repo support
:   You can now use {{site.data.keyword.secrets-manager_short}} to give {{site.data.keyword.short_name}} access to your taxonomy knowledge documents in private repositories or GitHub Enterprise repositories. You can enable private repository access when uploading your taxonomy in the console or by using the CLI. For information, see [Getting started with {{site.data.keyword.short_name}}](/docs/instructlab?topic=instructlab-getting-started&interface=ui).



## April 2025
{: #apr25}


### 24 April 2025
{: #24apr25}
{: release-note}


Introducing {{site.data.keyword.instructlab_full_notm}}!
:   Get ready to dive into AI! InstructLab is an open source project created by IBM and Red Hat to be a cost-effective entry point into the world of machine learning.
