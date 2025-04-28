---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-28"

keywords: knowledge documents, patterns, troubleshooting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# `Failed to find knowledge documents` error during data generation in {{site.data.keyword.short_name}}
{: #ts-knowledge-find}

When you try to generate data, you get the following error.
{: tsSymptoms}

```txt
Failed to find knowledge documents. See detailed logs in COS.
```
{: screen}

Given the information in the QNA files, no knowledge documents existed that matched the value in the `patterns` field. 
{: tsCauses}

When a taxonomy is uploaded, the file structure is validated. During data generation, additional validation is done to verify the content of the taxonomy.


Fix issues with the knowledge QNAs. Verify that the value in the `patterns` field matches some file names in the repository.
{: tsResolve}

```yaml
document:
repo: https://github.com/<organization>/<repository>
commit: <commit_sha>
patterns:
    - <folder>/<filename>.md
```
{: codeblock}


