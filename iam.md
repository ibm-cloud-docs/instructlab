---

copyright:
  years: 2025, 2025
lastupdated: "2025-03-07"

keywords: iam, access, add users, instructlab

subcollection: instructlab

---

{{site.data.keyword.attribute-definition-list}}

# Managing IAM access for {{site.data.keyword.instructlab_full_notm}}
{: #iam-docs-template}

Access to {{site.data.keyword.instructlab_short}} service instances for users in your account is controlled by {{site.data.keyword.cloud}} Identity and Access Management (IAM). Every user that accesses the {{site.data.keyword.instructlab_short}} service in your account must be assigned an access policy with an IAM role. Review the following roles, actions, and more to help determine the best way to assign access to {{site.data.keyword.instructlab_short}}.
{: shortdesc}

The access policy that you assign users in your account determines what actions a user can perform within the context of the service or specific instance that you select. The allowable actions are customized and defined by the {{site.data.keyword.instructlab_short}} as operations that are allowed to be performed on the service. Each action is mapped to an IAM platform or service role that you can assign to a user.

If a specific role and its actions don't fit the use case that you're looking to address, you can [create a custom role](/docs/account?topic=account-custom-roles#custom-access-roles) and pick the actions to include.
{: tip}

IAM access policies enable access to be granted at different levels. Some options include the following:

* Access across all instances of the service in your account
* Access to an individual service instance in your account if this applies 


Review the following tables that outline what types of tasks each role allows for when you're working with the {{site.data.keyword.instructlab_short}} service. Platform management roles enable users to perform tasks on service resources at the platform level, for example, assign user access to the service, create or delete instances, and bind instances to applications. Service access roles enable users access to {{site.data.keyword.instructlab_short}} and the ability to call the {{site.data.keyword.instructlab_short}}'s API.

This is a high level view of what the platform roles allow users to do. Use a plain language description about what kind of tasks can be completed or the common jobs to be done that users can expect to accomplish when having each role assigned. 

Include any service-specific custom roles that your service has registered.
To find the `role_id` values, run the `ibmcloud iam roles` command or go to the **Manage** > **Access (IAM)** > **Roles** console page. Select your service, then use the List of Actions icon for the row of the role that you want to get the ID value for, and click Details. It is part of the CRN. For example, in `crn:v1:bluemix:public:iam::::serviceRole:Writer`, `Writer` is the ID value. 

| Platform role |  Description of actions |
|---------------|-------------------------|
| Reader | As a reader, you can perform read-only actions within a service such as viewing service-specific resources. |
| Writer | As a writer, you have permissions beyond the reader role, including creating and editing service-specific resources. |
| Manager | As a manager, you have permissions beyond the writer role to complete privileged actions as defined by the service. In addition, you can create and edit service-specific resources. |
| Service Configurator Reader | The ability to read services configuration for Governance management. |
| Key Manager | As an key manager, the service can perform platform actions required to manage resource keys, such as creating a new resource key for a resource instance. |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM platform roles" caption-side="bottom"}
{: #iamrolesplatform}
{: tab-title="Platform roles"}
{: tab-group="IAM"}

| Service role |  Description of actions |
|--------------|------------------------|
| Viewer | As a viewer, you can view service instances, but you can't modify them. |
| Operator |  As an operator, you can perform platform actions required to configure and operate service instances, such as viewing a service's dashboard. |
| Editor |  As an editor, you can perform all platform actions except for managing the account and assigning access policies. |
| Administrator | As an administrator, you can perform all platform actions based on the resource this role is being assigned, including assigning access policies to other users. |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM service access roles" caption-side="bottom"}
{: #iamrolesservice}
{: tab-title="Service roles"}
{: tab-group="IAM"}

## Assigning access to {{site.data.keyword.instructlab_short}} in the console
{: #assign-access-console}
{: ui}

There are two common ways to assign access in the console:

Access policies per user.
:   You can manage access policies per user from the **Manage** > **Access (IAM)** > **Users** page in the console. For information about the steps to assign IAM access, see [Managing access to resources in the console](/docs/account?topic=account-assign-access-resources&interface=ui#access-resources-console).

Access groups.
:   Access groups are used to streamline access management by assigning access to a group once, then you can add or remove users as needed from the group to control their access. You manage access groups and their access from the **Manage** > **Access (IAM)** > **Access groups** page in the console. For more information, see [Assigning access to a group in the console](/docs/account?topic=account-groups&interface=ui#access_ag).


## Assigning access to {{site.data.keyword.instructlab_short}} in the CLI
{: #assign-access-cli}
{: cli}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the CLI](/docs/account?topic=account-assign-access-resources&interface=cli#access-resources-cli). The following example shows a command for assigning the `Writer` role for `instructlab`:

Use `instructlab` for the service name. Also, use quotations around role names that are more than one word like the example here.
{: tip}


The `instructlab` in the note above is important to include because the service name in the UI often doesn't match the service name that should be used to make an API call or run a CLI command.

Tailor this example to your service 

```bash
ibmcloud iam user-policy-create USER@EXAMPLE.COM --service-name instructlab --roles "Writer"
```
{: pre}

## Assigning access to {{site.data.keyword.instructlab_short}} by using the API
{: #assign-access-api}
{: api}

For step-by-step instructions for assigning, removing, and reviewing access, see [Assigning access to resources by using the API](/docs/account?topic=account-assign-access-resources&interface=api) or the [Create a policy API docs](/apidocs/iam-policy-management#create-policy). Role cloud resource names (CRN) in the following table are used to assign access with the API.


| Role name | Role CRN |
|---------------|-----------------|
| Viewer                 | `crn:v1:bluemix:public:iam::::serviceRole:Viewer`        |
| Operator               | `crn:v1:bluemix:public:iam::::serviceRole:Operator`      |
| Editor                 | `crn:v1:bluemix:public:iam::::serviceRole:Editor`        |
| Administrator          | `crn:v1:bluemix:public:iam::::serviceRole:Administrator` |
| Reader         | `crn:v1:bluemix:public:iam::::serviceRole:Reader`        |
| Writer         | `crn:v1:bluemix:public:iam::::serviceRole:Writer`        |
| Manager        | `crn:v1:bluemix:public:iam::::serviceRole:Manager`       |
| Service Key Configurator        | `crn:v1:bluemix:public:iam::::serviceRole:ConfigReader`       |
| Key Manager        | `crn:v1:bluemix:public:iam::::serviceRole:KeyManager`       |
{: caption="Role ID values for API use" caption-side="bottom"}

Tailor this example to your service 

The following example is for assigning the `Writer` role for `instructlab`:

Use `instructlab` for the service name, and refer to the Role ID values table to ensure that you're using the correct value for the CRN.
{: tip}


The `instructlab` in the note above is important to include because the service name in the UI often doesn't match the service name that should be used to make an API call.

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


```python
policy_subjects = PolicySubject(
  attributes=[SubjectAttribute(name='iam_id', value='IBMid-123453user')])
policy_roles = PolicyRole(
  role_id='crn:v1:bluemix:public:iam::::serviceRole:Writer')
account_id_resource_attribute = ResourceAttribute(
  name='accountId', value='ACCOUNT_ID')
service_name_resource_attribute = ResourceAttribute(
  name='serviceName', value='instructlab')
policy_resources = PolicyResource(
  attributes=[account_id_resource_attribute,
        service_name_resource_attribute])

policy = iam_policy_management_service.create_policy(
  type='access',
  subjects=[policy_subjects],
  roles=[policy_roles],
  resources=[policy_resources]
).get_result()

print(json.dumps(policy, indent=2))
```
{: python}
{: codeblock}

```go
subjectAttribute := &iampolicymanagementv1.SubjectAttribute{
  Name:  core.StringPtr("iam_id"),
  Value: core.StringPtr("IBMid-123453user"),
}
policySubjects := &iampolicymanagementv1.PolicySubject{
  Attributes: []iampolicymanagementv1.SubjectAttribute{*subjectAttribute},
}
policyRoles := &iampolicymanagementv1.PolicyRole{
  RoleID: core.StringPtr("crn:v1:bluemix:public:iam::::serviceRole:Writer"),
}
accountIDResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("accountId"),
  Value:    core.StringPtr("ACCOUNT_ID"),
  Operator: core.StringPtr("stringEquals"),
}
serviceNameResourceAttribute := &iampolicymanagementv1.ResourceAttribute{
  Name:     core.StringPtr("serviceName"),
  Value:    core.StringPtr("instructlab"),
  Operator: core.StringPtr("stringEquals"),
}
policyResources := &iampolicymanagementv1.PolicyResource{
  Attributes: []iampolicymanagementv1.ResourceAttribute{
    *accountIDResourceAttribute, *serviceNameResourceAttribute}
}

options := iamPolicyManagementService.NewCreatePolicyOptions(
  "access",
  []iampolicymanagementv1.PolicySubject{*policySubjects},
  []iampolicymanagementv1.PolicyRole{*policyRoles},
  []iampolicymanagementv1.PolicyResource{*policyResources},
)

policy, response, err := iamPolicyManagementService.CreatePolicy(options)
if err != nil {
  panic(err)
}
b, _ := json.MarshalIndent(policy, "", "  ")
fmt.Println(string(b))
```
{: go}
{: codeblock}
