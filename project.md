---

copyright:
  years: 2025, 2025
lastupdated: "2025-04-17"

keywords: instructlab, ai, project

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}


# Creating projects for {{site.data.keyword.short_name}}
{: #project}

Complete the following steps to create an {{site.data.keyword.short_name}} project.
{: shortdesc}

## Creating projects in the console for {{site.data.keyword.short_name}}
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



## Creating projects from the CLI for {{site.data.keyword.short_name}}
{: #project-create-cli}
{: cli}

To log in:
{{_include-segments/login.md}}

To create a project in the {{site.data.keyword.short_name}} instance, run the following command.

```sh
ibmcloud resource service-instance-create <project_name> instructlab instructlab-pricing-plan us-east
```
{: pre}


## What's next?
{: #whats-next-projects}

After creating your project, review the following links for next steps.

- [Assign users in your account access to your project](/docs/instructlab?topic=instructlab-project).
- [Learn how taxonomies are structured](/docs/instructlab?topic=instructlab-taxonomy-overview).
- [Prepare your taxonomy and upload it to Object Storage](https://cloud.ibm.com/docs/instructlab?topic=instructlab-taxonomy-prep).

 
