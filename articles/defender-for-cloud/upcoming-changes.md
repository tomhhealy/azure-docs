---
title: Important changes coming to Microsoft Defender for Cloud
description: Upcoming changes to Microsoft Defender for Cloud that you might need to be aware of and for which you might need to plan 
ms.topic: overview
ms.date: 08/10/2022
---

# Important upcoming changes to Microsoft Defender for Cloud

> [!IMPORTANT]
> The information on this page relates to pre-release products or features, which may be substantially modified before they are commercially released, if ever. Microsoft makes no commitments or warranties, express or implied, with respect to the information provided here.

On this page, you'll learn about changes that are planned for Defender for Cloud. It describes planned modifications to the product that might impact things like your secure score or workflows.

If you're looking for the latest release notes, you'll find them in the [What's new in Microsoft Defender for Cloud](release-notes.md).

## Planned changes

| Planned change | Estimated date for change |
|--|--|
| [Deprecating three VM alerts](#deprecating-three-vm-alerts) | June 2022|
| [Deprecate API App policies for App Service](#deprecate-api-app-policies-for-app-service) | July 2022 |
| [Change in pricing of Runtime protection for Arc-enabled Kubernetes clusters](#change-in-pricing-of-runtime-protection-for-arc-enabled-kubernetes-clusters) | August 2022 |
| [Multiple changes to identity recommendations](#multiple-changes-to-identity-recommendations) | September 2022 |
| [Removing security alerts for machines reporting to cross tenant Log Analytics workspaces](#removing-security-alerts-for-machines-reporting-to-cross-tenant-log-analytics-workspaces) | September 2022 |
| [Legacy Assessments APIs deprecation](#legacy-assessments-apis-deprecation) | September 2022 |

### Deprecating three VM alerts

**Estimated date for change:** June 2022

The following table lists the alerts that will be deprecated during June 2022.

| Alert name | Description | Tactics | Severity |
|--|--|--|--|
| **Docker build operation detected on a Kubernetes node** <br>(VM_ImageBuildOnNode) | Machine logs indicate a build operation of a container image on a Kubernetes node. While this behavior might be legitimate, attackers might build their malicious images locally to avoid detection. | Defense Evasion | Low |
| **Suspicious request to Kubernetes API** <br>(VM_KubernetesAPI) | Machine logs indicate that a suspicious request was made to the Kubernetes API. The request was sent from a Kubernetes node, possibly from one of the containers running in the node. Although this behavior can be intentional, it might indicate that the node is running a compromised container. | LateralMovement | Medium |
| **SSH server is running inside a container** <br>(VM_ContainerSSH) | Machine logs indicate that an SSH server is running inside a Docker container. While this behavior can be intentional, it frequently indicates that a container is misconfigured or breached. | Execution | Medium |

These alerts are used to notify a user about suspicious activity connected to a Kubernetes cluster. The alerts will be replaced with matching alerts that are part of the Microsoft Defender for Cloud Container alerts (`K8S.NODE_ImageBuildOnNode`, `K8S.NODE_ KubernetesAPI` and `K8S.NODE_ ContainerSSH`) which will provide improved fidelity and comprehensive context to investigate and act on the alerts. Learn more about alerts for [Kubernetes Clusters](alerts-reference.md).

### Deprecate API App policies for App Service

**Estimated date for change:** July 2022

We will be deprecating the following policies to corresponding policies that already exist to include API apps:

| To be deprecated | Changing to |
|--|--|
|`Ensure API app has 'Client Certificates (Incoming client certificates)' set to 'On'` | `App Service apps should have 'Client Certificates (Incoming client certificates)' enabled` | 
| `Ensure that 'Python version' is the latest, if used as a part of the API app` | `App Service apps that use Python should use the latest 'Python version` |
| `CORS should not allow every resource to access your API App` | `App Service apps should not have CORS configured to allow every resource to access your apps` |
| `Managed identity should be used in your API App` | `App Service apps should use managed identity` |
| `Remote debugging should be turned off for API Apps` | `App Service apps should have remote debugging turned off` |
| `Ensure that 'PHP version' is the latest, if used as a part of the API app` | `App Service apps that use PHP should use the latest 'PHP version'`|
| `FTPS only should be required in your API App` | `App Service apps should require FTPS only` |
| `Ensure that 'Java version' is the latest, if used as a part of the API app` | `App Service apps that use Java should use the latest 'Java version` |
| `Latest TLS version should be used in your API App` | `App Service apps should use the latest TLS version` |

### Change in pricing of runtime protection for Arc-enabled Kubernetes clusters

**Estimated date for change:** August 2022

Runtime protection is currently a preview feature for Arc-enabled Kubernetes clusters. In August, Arc-enabled Kubernetes clusters will be charged for runtime protection. You can view pricing details on the [pricing page](https://azure.microsoft.com/pricing/details/defender-for-cloud/). Subscriptions with Kubernetes clusters already onboarded to Arc, will begin to incur charges in August.

### Multiple changes to identity recommendations

**Estimated date for change:** September 2022

Defender for Cloud includes multiple recommendations for improving the management of users and accounts. In June, we'll be making the changes outlined below.

#### New recommendations in preview

The new release will bring the following capabilities:

- **Extended evaluation scope** – Improved coverage to identity accounts without MFA and external accounts on Azure resources (instead of subscriptions only) allowing security admins to view role assignments per account.

- **Improved freshness interval** - Currently, the identity recommendations have a freshness interval of 24 hours. This update will reduce that interval to 12 hours.

- **Account exemption capability** - Defender for Cloud has many features you can use to customize your experience and ensure that your secure score reflects your organization's security priorities. For example, you can [exempt resources and recommendations from your secure score](exempt-resource.md).

    This update will allow you to exempt specific accounts from evaluation with the six recommendations listed in the following table.

    Typically, you'd exempt emergency “break glass” accounts from MFA recommendations, because such accounts are often deliberately excluded from an organization's MFA requirements. Alternatively, you might have external accounts that you'd like to permit access to but which don't have MFA enabled.

    > [!TIP]
    > When you exempt an account, it won't be shown as unhealthy and also won't cause a subscription to appear  unhealthy.

    |Recommendation| Assessment key|
    |--|--|
    |Accounts with owner permissions on Azure resources should be MFA enabled|6240402e-f77c-46fa-9060-a7ce53997754|
    |Accounts with write permissions on Azure resources should be MFA enabled|c0cb17b2-0607-48a7-b0e0-903ed22de39b|
    |Accounts with read permissions on Azure resources should be MFA enabled|dabc9bc4-b8a8-45bd-9a5a-43000df8aa1c|
    |Guest accounts with owner permissions on Azure resources should be removed|20606e75-05c4-48c0-9d97-add6daa2109a|
    |Guest accounts with write permissions on Azure resources should be removed|0354476c-a12a-4fcc-a79d-f0ab7ffffdbb|
    |Guest accounts with read permissions on Azure resources should be removed|fde1c0c9-0fd2-4ecc-87b5-98956cbc1095|
    |Blocked accounts with owner permissions on Azure resources should be removed|050ac097-3dda-4d24-ab6d-82568e7a50cf|
    |Blocked accounts with read and write permissions on Azure resources should be removed| 1ff0b4c9-ed56-4de6-be9c-d7ab39645926 |

### Removing security alerts for machines reporting to cross-tenant Log Analytics workspaces 

**Estimated date for change:** September 2022

Defender for Cloud lets you choose the workspace that your Log Analytics agents report to. When a machine belongs to one tenant (“Tenant A”) but its Log Analytics agent reports to a workspace in a different tenant (“Tenant B”), security alerts about the machine are reported to the first tenant (“Tenant A”).

With this change, alerts on machines connected to Log Analytics workspace in a different tenant will no longer appear in Defender for Cloud.

If you want to continue receiving the alerts in Defender for Cloud, connect the Log Analytics agent of the relevant machines to the workspace in the same tenant as the machine.

### Legacy Assessments APIs deprecation

The following APIs are set to be deprecated:

- Security Tasks
- Security Statuses
- Security Summaries

These three APIs exposed old formats of assessments and will be replaced by the [Assessments APIs](/rest/api/securitycenter/assessments) and [SubAssessments APIs](/rest/api/securitycenter/sub-assessments). All data that is exposed by these legacy APIs will also be available in the new APIs.

## Next steps

For all recent changes to Defender for Cloud, see [What's new in Microsoft Defender for Cloud?](release-notes.md)
