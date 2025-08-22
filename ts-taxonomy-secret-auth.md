---

copyright:
  years: 2025, 2025
lastupdated: "2025-08-22"

keywords: secrets, authorization, troubleshooting

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# `Failed to read secret data from secrets manager` error when adding taxonomies in {{site.data.keyword.short_name}}
{: #ts-taxonomy-secret-auth}


When you try to add a taxonomy and include the {{site.data.keyword.secrets-manager_short}} authorization information, you get the following error.
{: tsSymptoms}

```txt
Failed to read secret data from secrets manager. Double check the authorization policy and that the secret exists.
```
{: screen}

Either the secret ID that was specified with the `--secrets-manager-git-id` option is invalid or the authorization policy for the secret might have been revoked or removed.
{: tsCauses}


Verify that you are including a valid ID for the secret and that the ID has valid authorization policies set for it. To set up an authorization policy, see [Authorizing an IBM Cloud service to access {{site.data.keyword.secrets-manager_short}}](/docs/secrets-manager?topic=secrets-manager-integrations#create-authorization).
{: tsResolve}
