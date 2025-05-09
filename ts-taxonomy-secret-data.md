---

copyright:
  years: 2025, 2025
lastupdated: "2025-05-09"

keywords: secrets, data, troubleshooting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# `Failed to parse secrets manager secret data` error when adding taxonomies in {{site.data.keyword.short_name}}
{: #ts-taxonomy-secret-data}


When you try to add a taxonomy and include the Secrets Manager configuration information, you get the following error.
{: tsSymptoms}

```txt
Failed to parse secrets manager secret data. Improper format.
```
{: screen}


The `data` content of the secret is not valid JSON.
{: tsCauses}


Verify that the JSON `data` is valid within the secret.
{: tsResolve}

Make sure the `github_url` and `github_pat` values are correct.

`github_pat`
:   Your personal access token (PAT).

`github_url`
:   This URL is the same URL that you used in the repo section of the your taxonomy document reference. Make sure you include `https://`. For more information, see [secret creation](/docs/secrets-manager?topic=secrets-manager-secrets-manager-cli#secrets-manager-cli-secret-create-command).
