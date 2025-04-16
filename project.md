---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-16"

keywords: instructlab, ai, project

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Creating a project for {{site.data.keyword.short_name}}
{: #project}

Complete the following steps to create an {{site.data.keyword.short_name}} project.
{: shortdesc}

## Creating a project in the console
{: #project-create-ui}
{: ui}

1. Navigate to [{{site.data.keyword.short_name}} in the console](https://cloud.ibm.com/catalog/services/instructlab).

1. Review the pricing plan.

1. In the **Configure resource** section, enter the following details.

    Service name
    :   Give your InstructLab project a name.

    Select a resource group
    :   Select the resource group where you want to create your project.

    Tags and Access management tags
    :   Enter any tags or access management tags that you want to use. Tags can help you organize your resources.

1. Accept the license agreement and click **Create**.

After your project is created, the project details page is shown.



## Creating a project from the CLI
{: #project-create-cli}
{: cli}

{{_include-segments/login.md}}
1. Create a project in the {{site.data.keyword.short_name}} instance.
    ```sh
    ibmcloud resource service-instance-create <project_name> instructlab instructlab-pricing-plan us-east
    ```
    {: pre}
