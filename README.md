# AD Connect Hybrid Identity Management

**Syncing On-Prem Active Directory with Microsoft Entra ID**

## For a detailed overview, check out my blog post:
[Azure AD Connect Hybrid Identity Management Blog](https://medium.com/@majameeljameey/azure-ad-connect-hybrid-identity-management-e3996e562ec9)

## Youtube Video 
https://youtu.be/2hWyBUtPB_8

This guide provides a comprehensive overview of setting up a hybrid identity management system using Azure AD Connect. It facilitates the synchronization of on-premises Active Directory (AD) with Microsoft Entra ID, ensuring a seamless transition to a cloud environment.

## Understanding the Components

Before we delve into the implementation, it’s crucial to understand the main players in our hybrid setup:

![On-Prem AD vs Entra ID](https://github.com/user-attachments/assets/12847d33-0878-4389-b3e2-c73943cd9e1b)

- **On-premises Active Directory (AD):** This is our traditional AD Domain Services running on a Windows Server, often referred to as "on-prem AD."
- **Microsoft Entra ID:** Formerly known as Azure AD, this is our cloud-based identity and access management service.
- **Azure AD Connect:** The vital tool that synchronizes identities between our on-premises AD and Entra ID.

Interestingly, Entra ID can also serve as an identity provider for your on-premises environment, showcasing its versatility.

![Sync Components](https://github.com/user-attachments/assets/b263dd50-99d7-4e3b-825d-ca2210416c30)

## The Problem We’re Solving

Our client is transitioning from an on-premises Microsoft AD to a cloud environment with Microsoft Entra ID. The challenge lies in migrating identities without disrupting operations or creating redundant user accounts. 

**Our solution?** Implement a hybrid identity management system that synchronizes existing on-premises identities with Entra ID.

## The Solution: Azure AD Connect

Azure AD Connect is our go-to tool for this project. It consists of two main components:

- **Azure AD Connect Sync component:** Installed in the on-premises environment.
- **Azure AD Connect Sync service:** Runs in Azure AD.

This setup allows users to access both on-premises and cloud resources using a single set of credentials, significantly simplifying identity management and enhancing overall security.

![Azure AD Connect Components](https://github.com/user-attachments/assets/08e3a939-9988-4e15-8f1e-fc1e1d9fdfdc)

## Prerequisites and Implementation Steps

Before diving into the implementation, we ensured the following prerequisites were in place:

- An Azure AD tenant.
- A verified domain in Azure AD.
- Windows Server 2012 Standard or better for the Azure AD Connect sync component.
- SQL Server database for storing identity data (Azure AD Connect installs SQL Server 2012 Express LocalDB by default).
- Azure AD Global Administrator account.
- Enterprise Administrator account for on-premises Active Directory.

We also ensured that the Azure AD Connect server had proper DNS resolution for both intranet and internet, allowing it to resolve names for both on-premises AD and Azure AD endpoints.

![Implementation Steps](https://github.com/user-attachments/assets/9f154299-2e93-4a51-bf44-08b1d9f4c264)

## Key Considerations

Throughout the implementation, we kept these important factors in mind:

- We used the **IdFix tool** to identify and resolve any errors, duplicates, or formatting issues in the on-premises directory before synchronization.
- The **Azure AD Connect sync component** was installed on a domain-joined server separate from the domain controller for best practices.
- We ensured all necessary accounts were properly set up and had the required permissions before beginning the synchronization process.

## Cloud Sync — How it works

Cloud sync is built on top of the Azure AD services and has two key components:

1. **Provisioning agent:** The Azure AD Connect cloud provisioning agent is the same agent as Workday inbound and built on the same server-side technology as app proxy and Pass Through Authentication. It requires an outbound connection only, and agents are auto-updated.

2. **Provisioning service:** This is the same provisioning service as outbound provisioning and Workday inbound provisioning, which uses a scheduler-based model. In the case of cloud sync, the changes are provisioned every 2 minutes.

For more details, refer to the official documentation:  
[How Cloud Sync Works](https://docs.microsoft.com/en-us/azure/active-directory/cloud-sync/concept-how-it-works)

## Synchronization Flow

![Synchronization Flow](https://github.com/user-attachments/assets/0f432e9a-4e42-4d25-b963-b73c6a04e071)

For a detailed overview, check out my blog post:  
[Azure AD Connect Hybrid Identity Management Blog](https://medium.com/@majameeljameey/azure-ad-connect-hybrid-identity-management-e3996e562ec9)

---

## Authentication Methods

![Cloud Sync](https://github.com/user-attachments/assets/9a9b8de9-baa2-4f7c-aec3-114c21e00630)
