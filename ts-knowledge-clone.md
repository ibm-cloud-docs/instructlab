---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-28"

keywords: knowledge documents, clone, taxonomy, troubleshooting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# `Failed to clone knowledge document repository` error during data generation in {{site.data.keyword.short_name}}
{: #ts-knowledge-clone}


When you try to generate data, you get the following error.
{: tsSymptoms}

```txt
Failed to clone knowledge document repository.  See detailed logs in COS.
```
{: screen}


The repository (`repo`) specified in the QNA was not accessible. 
{: tsCauses}

When a taxonomy is uploaded, the file structure is validated. During data generation, additional validation is done to verify the content of the taxonomy.


Fix issues with the knowledge QNA files.
{: tsResolve}

1. In the `document` section, verify that the `repo` value is valid.
    ```yaml
    document:
    repo: https://github.com/<organization>/<repository>
    commit: <commit_sha>
    patterns:
        - <folder>/<filename>.md
    ```
    {: codeblock}

2. Ensure the repo exists already.

3. Ensure that valid authorization was granted in the repository. 

