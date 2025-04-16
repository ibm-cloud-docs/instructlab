---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-16"

keywords: instructlab, ai, about, cli, ilab

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# Installing the {{site.data.keyword.product_name}} CLI
{: #cli-install}


You can use the `ilab` CLI plug-in to manage your {{site.data.keyword.short_name}} resources.
{: shortdesc}


{{../cli/index.md#step1-install-idt}}

{{../cli/index.md#step2-verify-idt}}

{{../cli/index.md#step3-install-idt-manually}}

- To install the `ilab` plug-in, run the following command.

    ```sh
    ibmcloud plugin install ilab
    ```
    {: pre}

- To install the `cos` plug-in, run the following command.

    ```sh
    ibmcloud plugin install cos
    ```
    {: pre}

- To install the `secrets-manager` plug-in, run the following command.

    ```sh
    ibmcloud plugin install secrets-manager
    ```
    {: pre}

- Optional: Install the [Git CLI](https://docs.github.com/en/get-started/git-basics/set-up-git) to store and manage your taxonomies.



{{../cli/reference/ibmcloud/download_cli.md#update-ibmcloud-cli}}

{{../cli/reference/ibmcloud/extend_cli.md#cli-update-plugin}}


## Logging in to the CLI
{: #cli-login}

{{_include-segments/login.md}}
