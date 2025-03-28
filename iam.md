---

copyright:
  years: 2025, 2025
lastupdated: "2025-03-28"

keywords: iam, access, add users, instructlab

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# Managing IAM access for {{site.data.keyword.instructlab_full_notm}}
{: #iam}

Access to {{site.data.keyword.instructlab_short}} projects for users in your account is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.instructlab_short}} service in your account must be assigned an access policy with an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.instructlab_short}}.
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific project that you select. The allowable actions are customized and defined by the {{site.data.keyword.instructlab_short}} as operations that are allowed to be performed on the service. Each action is mapped to an IAM platform or service role that you can assign to a user.

Make sure you also have the Viewer role for the resource groups you want to use.
{: tip}

IAM access policies enable access at different levels. Some options include the following:


- Giving Reader or Writer access to a specific project.
- Giving Reader or Writer access to a specific resource group where there could be many projects.
- Giving Reader or Writer access to the entire account where there could be many resource groups with many projects.
- Giving Viewer access to the {{site.data.keyword.short_name}} project(s) within a resource group and the account level.
- Giving creation access to create {{site.data.keyword.short_name}} project(s) within a resource group and the account level.

If a specific role and its actions don't fit the use case that you're looking to address, you can [create a custom role](/docs/account?topic=account-custom-roles#custom-access-roles) and pick the actions to include.
{: tip}

Review the following tables that outline what types of tasks each role allows for when you're working with the {{site.data.keyword.instructlab_short}} service. Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access to the service, create or delete projects, and bind projects to applications. Service access roles enable users access to {{site.data.keyword.instructlab_short}} and the ability to call the {{site.data.keyword.instructlab_short}}'s API.

This is a high level view of what the platform roles allow users to do. Use a plain language description about what kind of tasks can be completed or the common jobs that users can expect to do when having each role assigned.


| Platform role | Role ID | Description |
| --- | --- |
| Viewer | As a viewer, you can view projects, but you can't modify them. |
| Operator |  As an operator, you can perform platform actions required to configure and operate projects, such as viewing a service's dashboard. |
| Editor |  As an editor, you can perform all platform actions except for managing the account and assigning access policies. |
| Administrator | As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. |
| Service Configurator Reader | The ability to read services configuration for Governance management. |
| Key Manager | As an key manager, the service can perform platform actions required to manage resource keys, such as creating a new resource key. |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM platform roles" caption-side="bottom"}
{: #iamrolesplatform}
{: tab-title="Platform roles"}
{: tab-group="IAM"}

| Service role | Description |
| --- | --- |
| Reader | As a reader, you can perform read-only actions within a service such as viewing service-specific resources. |
| Writer | As a writer, you have permissions beyond the reader role, including creating and editing service-specific resources. |
| Manager | As a manager, you have permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM service access roles" caption-side="bottom"}
{: #iamrolesservice}
{: tab-title="Service roles"}
{: tab-group="IAM"}

## Assigning access to {{site.data.keyword.short_name}} in the console
{: #assign-access-console}
{: ui}

There are two common ways to assign access in the console:

Access policies per user.
:   You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources in the console](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).

Access groups.
:   Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).

{{../account/iam-mng-access.md#access-resources-console}}

{{../account/iam-mng-access.md#access-to-resources-console}}

{{../account/iam-mng-access.md#access-to-resource-group}}


## Assigning access to {{site.data.keyword.short_name}} in the CLI
{: #assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli). The following example shows a command for assigning the `Writer` role for `instructlab`:

Use `instructlab` for the service name. To find the role IDs, run the `ibmcloud iam roles` command. Also, use quotations around role names that are more than one word. For example `"Service Configuration Reader"`.
{: tip}

Example command to give a user the Viewer role for a specific {{site.data.keyword.short_name}} project in the account.

```sh
ibmcloud iam user-policy-create name@example.com --roles Viewer --service-name instructlab --attributes "projectId=1b111111-1ef1-11f1-1111-111bae11111a"
```
{: pre}

Example command to give a user the Key Manager role for a specific Instructlab project in the account.

```sh
ibmcloud iam user-policy-create name@email.com --roles "Key Manager" --service-name instructlab
```

Example command to give a user the Writer role for all {{site.data.keyword.short_name}} projects in the account.

```sh
ibmcloud iam user-policy-create USER@EXAMPLE.COM --service-name instructlab --roles Writer
```
{: pre}

Example command to assign the Administrator role for all instances of {{site.data.keyword.short_name}} service in the account.

```sh
ibmcloud iam user-policy-create name@example.com --roles Administrator --service-name instructlab
```
{: pre}

Example command to assign the Viewer role to all resource groups in the account.

```sh
ibmcloud iam user-policy-create name@example.com --roles Viewer --resource-type resource-group
```
{: pre}

Example command to assign the Viewer role to all users in a specific resource group.

```sh
ibmcloud iam user-policy-create name@example.com --roles Viewer --resource-type resource-group
```
{: pre}

Example command to get a resource group the Administrator role.

```sh
ibmcloud iam service-policy-create test --roles Administrator --resource-group-name sample-resource-group
```
{: pre}


## Assigning access to {{site.data.keyword.short_name}} by using the API
{: #assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api) or the [Create a policy API docs](/apidocs/iam-policy-management#create-policy). Role cloud resource names (CRN) in the following table are used to assign access with the API.

Use `instructlab` for the service name, and refer to the Role CRN values table to ensure that you're using the correct value for the role. Review the following list of role CRNs.
{: tip}

| Role | CRN |
| --- | --- |
| Reader | `crn:v1:bluemix:public:iam::::serviceRole:Reader` |
| Writer | `crn:v1:bluemix:public:iam::::serviceRole:Writer` |
| Manager | `crn:v1:bluemix:public:iam::::serviceRole:Manager` |
| Viewer | `crn:v1:bluemix:public:iam::::serviceRole:Viewer` |
| Operator | `crn:v1:bluemix:public:iam::::serviceRole:Operator` |
| Editor | `crn:v1:bluemix:public:iam::::serviceRole:Editor` |
| Administrator | `crn:v1:bluemix:public:iam::::serviceRole:Administrator` |
| Service Configurator Reader | `crn:v1:bluemix:public:iam::::serviceRole:ConfigReader` |
| Key Manager | `crn:v1:bluemix:public:iam::::serviceRole:KeyManager` |
{: caption="IAM role CRNs" caption-side="bottom"}


The following example assigns the `Writer` role for `instructlab`.

```curl
curl -X POST 'https://iam.cloud.ibm.com/v1/policies' -H 'Authorization: Bearer $TOKEN' -H 'Content-Type: application/json' -d '{
  "type": "access",
  "description": "Writer role for InstructLab",
  "subjects": [
    {
      "attributes": [
        {
          "name": "iam_id",
          "value": "IBMid-123453user"
        }
      ]
    }'
  ],
  "roles":[
    {
      "role_id": "crn:v1:bluemix:public:iam::::serviceRole:Writer"
    }
  ],
  "resources":[
    {
      "attributes": [
        {
          "name": "accountId",
          "value": "$ACCOUNT_ID"
        },
        {
          "name": "serviceName",
          "value": "instructlab"
        }
      ]
    }
  ]
}
```
{: curl}
{: codeblock}




{{../account/iam-mng-access.md#access-resources-api}}

{{../account/iam-mng-access.md#access-resourcegroups-api}}
