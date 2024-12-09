---
title: What's New
geekdocCollapseSection: true
weight: 09
---

For the latest updates, visit the [Releases](https://github.com/Azure/azure-monitor-baseline-alerts/releases) page.

To update your deployment with the latest release, refer to the [Update to new releases](../../HowTo/UpdateToNewReleases) guide.

## 2024-11-01

### New Features

- Introduced a new policy definition to audit/update Recovery Vault ASR Health Alerting to Azure Monitor alerts.
- **Script Consolidation**: The scripts *Remove-AMBADeployments.ps1*, *Remove-AMBANotificationAssets.ps1*, *Start-AMBACleanup.ps1*, *Start-AMBAOldArpCleanup.ps1*, and *Start-AMBAPolicyInitiativesAndAssignmentsCleanup.ps1* have been merged into a single script named [***Start-AMBA-ALZ-Maintenance.ps1***](https://github.com/Azure/azure-monitor-baseline-alerts/blob/main/patterns/alz/scripts/Start-AMBA-ALZ-Maintenance.ps1) [[#352](https://github.com/Azure/azure-monitor-baseline-alerts/pull/352): Consolidate maintenance scripts]. This enhancement allows the removal of alerts for deleted resources (orphaned alerts).

### Bug Fixes

- Resolved [[#323](https://github.com/Azure/azure-monitor-baseline-alerts/pull/323)]: Ensured the -WhatIf parameter is honored by all script commands and fixed the hybrid disconnected alert bug.
- Resolved [[#342](https://github.com/Azure/azure-monitor-baseline-alerts/pull/342)]: Fixed GitHub issue link and Management Subscription ID.
- Resolved [[#346](https://github.com/Azure/azure-monitor-baseline-alerts/pull/346)]: Updated useCommonSchema to useCommonAlertSchema in Deploy_ServiceHealth_ActionGroups and Deploy_Suppression_AlertProcessing_Rule Policy Definitions.
- Resolved [[#357](https://github.com/Azure/azure-monitor-baseline-alerts/pull/357)]: Fixed the ExpressRoute QoS remediation issue.
- Resolved [[#362](https://github.com/Azure/azure-monitor-baseline-alerts/pull/362)]: Standardized parameter usage for failingPeriods and evaluationPeriods.
- Resolved [[#381](https://github.com/Azure/azure-monitor-baseline-alerts/pull/381)]: Fixed Connectivity policy initiative, tag name case consistency, and updated tag override documentation.

### Documentation Updates

- Improved clarity on the 'Update to new releases' page.
- Added examples using the new consolidated maintenance script to the 'Update to new releases' page: [Updating to release 2024-09-02](../../HowTo/UpdateToNewReleases#2024-09-02), [Updating to release 2024-03-01](../../HowTo/UpdateToNewReleases#2024-03-01).
- Clarified identification of the pseudoRootManagementGroup as the parent of the Platform and Landing Zones management groups.
- Updated AMBA diagrams in the [Introduction to deploying the ALZ Pattern](../../HowTo/deploy/Introduction-to-deploying-the-ALZ-Pattern) section.
- Added remediation command for the ***Deploy Azure Monitor Baseline Alerts for Recovery Services*** policy initiative to the [Remediate Policies](../../HowTo/deploy/Remediate-Policies) list.

### Tools

- **Automation:**
  - Removed the previous workflow that automated the creation of ARM templates for Azure Policies/PolicySets due to a security issue.
  - Introduced a new workflow to ensure policy updates and verify the Bicep build has been run by the contributor.

## 2024-09-02

### New Features

- **AMBA Portal Accelerator**: Launched the Azure Monitor Baseline Alerts Accelerator in preview, enabling quick and confident alert deployment through the Azure Portal UI. For detailed instructions, see [Deploy via the Azure Portal (Preview)](../../HowTo/deploy/Deploy-via-Azure-Portal-UI).
- **Modular Initiatives**: Deprecated the former Landing Zone Initiative in favor of a modular approach with distinct components. For more details, visit [Policy Initiatives](../../Getting-started/Policy-Initiatives).

  - Key Management
  - Load Balancing
  - Network Changes
  - Recovery Services
  - Storage
  - VM
  - Web

- **Threshold Override**: Allows adjustment of alert thresholds for specific resources using a tag. This feature is available for metrics and log alerts. Learn more: [Alert Threshold Override](../../HowTo/Threshold-Override).

- **Custom Tags to Disable Monitoring**: Specify a tag name and values to disable monitoring for certain resources.

- Added new alert rules for Azure Key Vault Managed HSM, included in Identity and Key Management initiatives.
- Added a new Daily Cap threshold alert for Log Analytics workspace, included in the Management initiative.
- Added a new Application Insight Throttling alert, included in the Web initiative.
- Added a new ActivityLog Alert for deleting Application Insight, included in the Web initiative.
- Enabled changing Application Gateway dynamic alert sensitivity.

- **Deprecated** the Landing Zone Initiative.

### Bug Fixes

- Resolved [[#280](https://github.com/Azure/azure-monitor-baseline-alerts/issues/280)]: Fixed AGW Compute Units Alert and AGW Unhealthy Host Count Alert non-compliance after remediation.
- Resolved [[#278](https://github.com/Azure/azure-monitor-baseline-alerts/issues/278)]: Fixed Deploy VNetG ExpressRoute CPU Utilization Alert remediation failure.
- Resolved [[#284](https://github.com/Azure/azure-monitor-baseline-alerts/issues/284)]: Fixed missing AMBA policy ALZ_ServiceHealth_ActionGroups during remediation.
- Resolved [[#253](https://github.com/Azure/azure-monitor-baseline-alerts/issues/253)]: Updated older version used in documentation.
- Resolved [[#261](https://github.com/Azure/azure-monitor-baseline-alerts/issues/261)]: Corrected display name VMLowOSDisk(Write/Read)LatencyAlert to VMHighOSDisk(Write/Read)LatencyAlert.
- Resolved [[#260](https://github.com/Azure/azure-monitor-baseline-alerts/issues/260)]: Added threshold parameter for ALZ alerts ALZ_WSFMemoryPercentage, ALZ_WSFCPUPercentage.
- Fixed casing in metadata and policies.
- Fixed default values for multiple parameters in VM and Hybrid initiatives.

### Documentation Updates

- Added new policies for ExpressRoute Ports to the Connectivity table. [Policy Initiatives](../../Getting-started/Policy-Initiatives).
- Updated documentation on unsupported/unrecommended Tenant Root Group deployment. [FAQ](../../Resources/FAQ).
- Provided new guidance for bringing your own Managed Identity. [Bring Your Own User Assigned Managed Identity](../../HowTo/Bring-Your-Own-User-Assigned-Managed-Identity).
- Updated Policy Initiatives documentation to include Policy Reference ID and display names. [Policy Initiatives](../../Getting-started/Policy-Initiatives).

### Tools

- **Automation**: Introduced a new workflow to automate ARM template creation for Azure Policies/PolicySets, triggered by pull request events.

## 2024-06-05

### New Features

- Added new PIDs for additional deployment methods. See [Disable telemetry tracking](../../HowTo/Telemetry) for more information.
- Introduced a new initiative to monitor Azure Arc-enabled Virtual Machines. [Alerting-HybridVM](https://github.com/Azure/azure-monitor-baseline-alerts/blob/main/patterns/alz/policySetDefinitions/Deploy-HybridVM-Alerts.json).

### Bug Fixes

- Changed minFailingPeriodsToAlert and numberOfEvaluationPeriods in existenceCondition from 2 to 4 to fix compliance evaluation.
- Changed timeAggregation to Average for AGW BackendLastByteResponseTime and AGW ApplicationGatewayTotalTime policies. [Issue #194](https://github.com/Azure/azure-monitor-baseline-alerts/issues/194).
- Fixed case-sensitive parameters [Issue #185](https://github.com/Azure/azure-monitor-baseline-alerts/issues/185).

### Documentation Updates

- Updated Deploy only Service Health Alert documentation for json-strings in cloud shell.

## 2024-04-12

### New Features

- Updated Existence Condition to detect and remediate configuration drift. The following parameters were added to the Existence Condition of the policies:

  - Static alerts: EvaluationFrequency, WindowSize, Threshold, Severity, Operator, autoMitigate

  - Dynamic alerts: alertSensitivity, numberOfEvaluationPeriods, minFailingPeriodsToAlert

- Added suppression Alert Processing Rule in notification Assets policy. See [Temporarily disabling notifications](../../HowTo/Temporarily-disabling-notifications) for details.
- Email address for Action Group is no longer mandatory.
- Bring your own Action Group and/or Alert Processing Rules. See [Bring Your Own Notifications (BYON)](../../HowTo/Bring-your-own-Notifications) for details.

### Bug Fixes

- Fixed operator for `SNATPortUtilization` for Azure Firewall.
- Corrected name for Deploy Activity Log Storage Account Delete Policy.

### Documentation Updates

- Updated deployment documentation to use the latest release.
- Updated Deploy only Service Health Alert documentation.
- Updated AMBA-ALZ Diagrams to include new notification assets initiative and Action group options. [AMBA-Diagram](../../media/AMBA-Diagrams.vsdx).

## 2024-03-01

### New Features

- Enhanced action group for more notification and action choices:
  - Email Azure Resource Manager Role
  - Azure Function
  - Event Hubs
  - Logic App
  - Webhook
- Service health initiative now has its own Action Group.
- Added [Notification Assets](https://raw.githubusercontent.com/Azure/azure-monitor-baseline-alerts/main/patterns/alz/policySetDefinitions/Deploy-Notification-Assets.json) initiative.
- Introduced a new policy for Storage Account Deletion. [Issue #76](https://github.com/Azure/azure-monitor-baseline-alerts/issues/76).
- Updated remediation script for better experience with the new action group for Service Health.

### Bug Fixes

- Resolved: unable to deploy via pipeline using ubuntu-latest. [Issue #64](https://github.com/Azure/azure-monitor-baseline-alerts/issues/64).
- Fixed PIP VIP alert existence condition to check only for standard SKU. [Issue #80](https://github.com/Azure/azure-monitor-baseline-alerts/issues/80).

### Documentation Updates

- Updated [Deploy with GitHub Actions](../../HowTo/deploy/Deploy-with-GitHub-Actions) addressing [Issue #102](https://github.com/Azure/azure-monitor-baseline-alerts/issues/102).
- Updated guidance for AMA in [Monitoring and Alerting](../../Getting-started/Monitoring-and-Alerting).

## 2023-11-14

### New Features

- Service Health Policy Set Definition now includes parameters to set Policy Effect. Default value is "deployIfNotExists".
- Added alert rules in Landing Zone Policy Set Definition:
  - Front door (Microsoft.Cdn/profiles)
  - Front door classic (Microsoft.Network/frontdoors)
  - Traffic Manager (Microsoft.Network/trafficmanagerprofiles)
  - App Service (Microsoft.Web/serverfarms)

### Bug Fixes

- Updated path in sample-workflow [Issue #30](https://github.com/Azure/azure-monitor-baseline-alerts/issues/30).
- Updated sample commands in Start-AMBARemediation.ps1 [Pull #49](https://github.com/Azure/azure-monitor-baseline-alerts/pull/49).
- Fixed Role Assignment cleanup script [Issue #42](https://github.com/Azure/azure-monitor-baseline-alerts/issues/42).
- Fixed VSCode template validation error [Issue #43](https://github.com/Azure/azure-monitor-baseline-alerts/issues/43).

### Documentation Updates

- How to modify individual policies - [How to modify individual policies](../../HowTo/deploy/Introduction-to-deploying-the-ALZ-Pattern/#how-to-modify-individual-policies).
- Added guidance for Server Health alert rules - [Deploy only Service Health Alerts](../../HowTo/deploy/Deploy-only-Service-Health-Alerts).
- New documentation on updating to a new release - [Update to new releases](../../HowTo/UpdateToNewReleases).
- FAQ Updates - [Frequently Asked Questions](../../Resources/FAQ).

