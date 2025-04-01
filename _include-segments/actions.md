## IAM roles and actions
{: #iam-roles-and-actions}

| Platform role | Description |
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

| Actions | Description | Roles |
| --- | --- | --- |
| `instructlab.dashboard.view` | View InstructLab dashboards. | Operator, Administrator, Editor |
| `instructlab.taxonomy.read` | Read details of a taxonomy. | Reader, Writer, Manager |
| `instructlab.taxonomy.create` | Create taxonomies | Writer, Manager |
| `instructlab.taxonomy.list` | List taxonomies. | Reader, Writer, Manager |
| `instructlab.taxonomy.delete` | Delete taxonomies. | Writer, Manager |
| `instructlab.sdgdata.read` | Read details of a data generation run. | Reader, Writer, Manager |
| `instructlab.sdgdata.list` | List data generation runs. | Reader, Writer, Manager |
| `instructlab.sdgdata.create` | Create a data generation run. | Writer, Manager |
| `instructlab.sdgdata.delete` | Delete a data generation run. | Writer, Manager |
| `instructlab.sdgdata.stop` | Stop a data generation run. | Writer, Manager |
| `instructlab.sdgdata.stop` | Stop a data generation run. | Writer, Manager |
| `instructlab.model.read` | Read details of a model training run.| Reader, Writer, Manager |
| `instructlab.model.list` | List model training runs. | Reader, Writer, Manager |
| `instructlab.model.create` | Create a model training run. | Writer, Manager |
| `instructlab.model.delete` | Delete a model training run. | Writer, Manager |
| `instructlab.model.stop` | Stop a model training run. | Writer, Manager |
{: row-headers}
{: class="simple-tab-table"}
{: caption="IAM actions" caption-side="bottom"}
{: #iamactions}
{: tab-title="Actions"}
{: tab-group="IAM"}
