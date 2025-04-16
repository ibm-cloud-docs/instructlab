1. Log in to your {{site.data.keyword.cloud_notm}} account from the CLI.
    ```sh
    ibmcloud login -a https://cloud.ibm.com --sso -r us-east
    ```
    {: pre}

1. If you plan to allow {{site.data.keyword.short_name}} to create {{site.data.keyword.cos_full}} Instance resources for you, target a resource group.
    ```sh
    ibmcloud target -g <resource_group>
    ```
    {: pre}

    Example:
    ```sh
    ibmcloud target -g Default
    ```
    {: pre}
