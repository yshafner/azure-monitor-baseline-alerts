---
title: FAQ
geekdocCollapseSection: true
weight: 80
---

## Do I need to have Azure Landing zones deployed for this to work?

> No, Azure Landing Zones are not required. However, you must use Azure Management Groups. Currently, our focus is on resources commonly deployed as part of Azure Landing Zone implementations.

## Can I deploy to the Tenant Root Group?

> Although it is recommended to implement the alert policies and initiatives within an Azure Landing Zone (ALZ) Management Group hierarchy, it is not a technical requirement. However, avoid assigning policies to the Tenant Root Group to minimize the complexity of debugging inherited policies at lower-level management groups. For more information, refer to the [CAF documentation](https://learn.microsoft.com/en-us/azure/cloud-adoption-framework/ready/landing-zone/design-area/resource-org-management-groups).

## Do I need to deploy to each region that I want to monitor?

> No, deployment to multiple regions is not required. The definitions and assignments are scoped at the management group level and are not specific to any region.

## Do I need to use the thresholds defined as default values in the metric rule alerts?

> The provided thresholds are intended as a starting point, based on Microsoft's recommendations and field experience. You may need to adjust these thresholds to suit your specific environment. Monitor the alerts and adjust the thresholds accordingly: increase the threshold if the alerts are too frequent, or decrease it if the alerts are not triggering when they should. Once you have determined an appropriate threshold, consider sharing your findings with us for broader use.

## Why are the availability alert thresholds lower than 100% in this solution when the product group documentation recommends 100%?

> Setting a threshold of 100% can sometimes result in false alerts, creating unnecessary noise. By lowering the threshold slightly below 100%, this issue can be mitigated while still ensuring alerts for service availability. If the default threshold is not stringent enough, you are encouraged to adjust it upwards. Additionally, you can provide feedback by filing an issue in our GitHub repository: [GitHub Issue](https://github.com/Azure/azure-monitor-baseline-alerts/issues).

## Do I need to use these metrics or can they be replaced with ones more suited to my environment?

> The metric rules provided are based on Microsoft's recommendations and field experience. Your usage of Azure resources may vary, so it is advisable to customize the alerts to meet your specific requirements. The primary objective of this project is to facilitate scalable Azure Monitor alerts. You are encouraged to create new rules with your own thresholds. We welcome feedback on your custom rules, so please share your findings with us.

## Can I disable the alerts being deployed for a resource or subscription?

> Yes, you can disable the alerts for a specific resource or subscription. For detailed instructions, please refer to the [Disabling Policies](../../HowTo/Disabling-Policies) documentation.

## How much does it cost to run the ALZ Baseline solution?

> The cost of running the ALZ Baseline solution varies based on several factors, including the number of alert rules deployed, the number of subscriptions inheriting the baseline policies, and the resources within each subscription that match the policy rules. Each alert rule costs approximately $0.1 per month<sup>1</sup>.
>
> - Alert rules are charged based on the number of evaluations.
> - If the alert rule evaluates data continuously throughout the month, the cost is approximately $0.1<sup>1</sup>.
> - If the rule evaluates data intermittently (e.g., due to the monitored resource being down and not sending telemetry), the cost is prorated based on the time the rule was actively evaluating data.
> - Using Dynamic Thresholds doubles the cost of the alert rule, resulting in a total cost of approximately $0.2 per month<sup>1</sup>.
> - The solution configures an email address as part of the Action Groups deployment (one per subscription), with a charge of approximately $2 per month for every 1,000 emails<sup>1</sup>.
>
> {{< hint type=Note >}} It is advisable to evaluate the costs in a non-production environment before full deployment to ensure a clear understanding of the potential expenses.{{< /hint >}}
>
> For detailed cost estimates related to your deployment, please refer to the [Azure Monitor Pricing](https://azure.microsoft.com/en-us/pricing/details/monitor/) page. Additionally, you can collaborate with your local Microsoft account team to develop a rough order of magnitude (RoM) cost estimate.
> <sup>1</sup> Note that costs may vary slightly depending on the deployment region. The costs mentioned are based on pricing as of April 2023.

## Can I access the Visio diagrams displayed in the documentation?

> Yes, you can access the Visio diagrams in the [media](https://github.com/Azure/azure-monitor-baseline-alerts/tree/main/docs/content/patterns/alz/media) folder.

## Can I use AMBA-ALZ without cloning/forking a GitHub repository

> <p> Yes, as long as the ARM templates are publicly accessible. This solution includes several linked templates that must be accessible publicly. When the top-level ARM template is submitted to Azure Resource Manager, the linked templates are not automatically uploaded and need to be pulled in at deploy time from Azure. Therefore, they must be referenced using a URL accessible from Azure (e.g., via a public GitHub repository). <p>
>
> <p> Alternatively, you can use Template specs. Instead of maintaining your linked templates at an accessible endpoint, you can create a template spec that packages the main template and its linked templates into a single entity for deployment. The template spec is a resource in your Azure subscription, making it easy to securely share the template with users in your organization. You can use Azure role-based access control (Azure RBAC) to grant access to the template spec. This feature is currently in preview.<p>
>
> References:
>
> - [Template specs](https://learn.microsoft.com/en-us/azure/azure-resource-manager/templates/linked-templates?>tabs=azure-powershell#template-specs)
> - [ARM Private deployment](https://github.com/Azure/ARM-private-deployment)

## Can I deploy a local template by using -TemplateFile

> No, using the `-TemplateFile` parameter is not feasible because the ARM template includes linked templates. When referencing a linked template, the URI value cannot be a local file or a file accessible only on your local network. Azure Resource Manager must have access to the template, which requires the templates to be referenced using a URL accessible from Azure (e.g., a public GitHub repository).

## What characters can I use when creating Azure resources or renaming Azure subscriptions?

> Not all characters are allowed when creating Azure resources or renaming Azure subscriptions. For a comprehensive list of supported characters, refer to the [Naming rules and restrictions for Azure resources](https://learn.microsoft.com/en-us/azure/azure-resource-manager/management/resource-name-rules) documentation. For example, alert suppression rules permit only alphanumeric characters, underscores, and hyphens.
>
> - **_a_** through **_z_** (lowercase letters)
> - **_A_** through **_Z_** (uppercase letters)
> - **_0_** through **_9_** (numbers)
>
> Using unsupported characters when creating an Azure resource or renaming a subscription can lead to the following issues:
>
> - Resource creation will fail.
> - Deployment of action groups and/or alert processing rules will fail. For AMBA-specific issues, refer to the [Failed to deploy action group(s) and/or alert processing rule(s)](../Known-Issues#failed-to-deploy-action-groups-andor-alert-processing-rules) section in the [Known Issues](../Known-Issues) documentation.
> - Editing action groups will result in an Azure portal page error. For AMBA-specific issues, refer to the [Failed to edit action group(s)](../Known-Issues#failed-to-edit-action-groups) section in the [Known Issues](../Known-Issues) documentation.
