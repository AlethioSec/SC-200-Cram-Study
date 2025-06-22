# Copilot

>[!Note]
>You can use copilot as a standalone and embedded experience

## Natural language processing (NLP)

Copilot is built using **Azure OpenAI Services** and designed to integrate with existing security tools and processes. Azure OpenAI Services provides REST API access to OpenAI's powerful large language models (LLMs) for natural language processing (NLP), while providing security capabilities of Microsoft Azure.

## Use cases

- Investigate and remediate security threats, gain context for incidents to quickly triage and remediate with step-by-step response.
- Build KQL queries or analyze suspicious scripts
- Understand risks and manage security posture of the organization
- Define and manage security policies, define a new policy, cross-reference it with others for conflicts, and summarize existing policies to manage complex organizational context quickly and easily
- Configure secure lifecycle workflows - build groups and set access parameters with step-by-step guidance to ensure a seamless configuration to prevent security vulnerabilities
- Develop reports for stakeholders 

## Terminology

- Session – A particular conversation within Copilot. Copilot maintains context within a session.
- Prompt – A specific statement or question within a session. A user enters a prompt in the prompt bar.
- Capability – A function Copilot uses to solve part of a problem. A capability may sometimes be referred to as a skill.
- Plugin – A collection of capabilities by a particular resource.
- Workspace - Copilot workspaces are separate Copilot work environments within the tenant in which your Copilot instance is operating.
- Agents - Microsoft Security Copilot agents are AI-powered tools that autonomously manage security and IT tasks, enhancing threat response, reducing manual workloads, and improving efficiency across cybersecurity operations at scale.
- Orchestrator – Copilot’s system for composing capabilities together to answer a user’s prompt.
## Set Up copilot

### 👔 Set role permissions

Before users can start using Copilot, admins need to provision and allocate capacity. 

To provision capacity:

- You must have an Azure subscription.
- You need to be an **Azure owner or Azure contributor**, at a resource group level, as a minimum.

Once you're assigned the User Access Administrator role in Azure, you can assign a user the necessary access to provision SCUs for Copilot. 

Enable Access management for Azure resources. 
Assign yourself the Owner role for the Azure subscription.
As an owner to the Azure subscription, you'll now be able to provision capacity within Copilot.

In order to start using Security Copilot, you must provision the capacity, which is defined in terms of security compute units. There are two options for provisioning capacity:

- Provision capacity within Security Copilot (recommended)
- Provision capacity through Azure

## SCUs 

**Security Compute Units (SCUs)** are the currency of computational power—they determine how much processing capacity your Copilot environment can use.

### 🧠 What SCUs Do:

- **Power AI-driven tasks**: Every time you run a prompt, analyze an incident, or use a plugin, SCUs are consumed based on the complexity and data volume.
- **Enable automation**: SCUs fuel automated workflows like incident triage playbooks or summarization tasks.
- **Control cost and scale**: You provision SCUs based on expected workload, and optionally allow _overage SCUs_ to handle spikes without over-provisioning.

### 🔄 Two Types of SCU Usage:

|**Type**|**Billing**|**Use Case**|
|---|---|---|
|**Provisioned**|Billed hourly (per SCU)|Regular, predictable workloads|
|**Overage**|Billed per use (to 0.1 SCU)|Spikes in demand or unexpected usage bursts|

### 📊 Why It Matters:

- Helps **optimize cost** by scaling compute based on real usage.
- Ensures **performance** during high-demand scenarios.
- Gives **visibility** into how much compute each action consumes, aiding in capacity planning.

## Workspaces

Copilot workspaces are separate Copilot work environments within the tenant.

A workspace is a scoped, tenant-bound environment where users, automations, and agents operate. All user interaction happens within the context of a workspace. It helps provide a boundary for user access and resource allocation.

### 🧰 Create a new workspace

1. Select the **Menu** icon, select **Manage workspaces**. 
2. Select **+ New workspace**
    1. Workspace name, Once you pick a workspace name, you won't be able to change it.
    2. Capacity: When you create a workspace, you can assign an available capacity or create a new capacity.
    3. Data storage location: Your customer data is stored in the location you select.
    4. For the two items with toggle switches, select any combination.
    5. Select the box next to the statement, I acknowledge that I have read, understood, and agree to the Terms and Conditions.
    6. Select Create.


## Role permissions

To ensure that the users can access the features of Copilot, they need to have the appropriate role permissions. Role permissions are configured per workspace.

Permissions can be assigned using Microsoft Entra ID roles or Security Copilot roles. As a best practice, provide the least privileged role applicable for each user.

The Microsoft Entra ID roles are:

- Global administrator
- Security administrator
- Security operator
- Security reader

Although these Microsoft Entra ID roles grant users varying levels of access to Copilot, the scope of these roles extends beyond Copilot. For this reason, Security Copilot introduces two roles that function like access groups but aren't Microsoft Entra ID roles. Instead, they only control access to the capabilities of the Security Copilot platform.

The Microsoft Security Copilot roles are:

- Copilot owner
- Copilot contributor

| **Role Name**               | **Primary Function**                                                                                             | **Key Permissions / Capabilities**                                                                                                                                                                                                                                                                                                                 | **Inherited Access (from Microsoft Entra roles)**                                   |
| --------------------------- | ---------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------- |
| **Copilot Owner** 🧭        | Provides administrative control over Microsoft Security Copilot instance and its underlying capacity.            | - Manage all platform settings<br>- Provision, scale, and delete Security Compute Units (SCUs) and monitor usage<br>- Configure data sharing preferences<br>- Manage personal custom plugins<br>- Allow contributors to publish custom plugins for the tenant<br>- Assign/remove Copilot Owner and Contributor roles<br>- Create and view sessions | - Global Administrator<br>- Security Administrator                                  |
| **Copilot Contributor** 🛠️ | Enables users to interact with the Microsoft Security Copilot platform for security analysis and investigations. | - Create and work within Copilot sessions<br>- View sessions<br>- Share session links<br>- Interact with plugins to gather security data and insights (access to underlying data requires separate security roles like Sentinel Reader, Defender XDR roles, etc.)<br>- View personal custom plugins (but not manage or publish by default)         | - Security Operator<br>- Security Reader<br>- By default, "Everyone" in the tenant. |


In Microsoft Security Copilot, admins or owners can assign the **Contributor** role to a special group called **Recommended Microsoft Security roles**. This group is unique to Security Copilot and acts as a shortcut—it bundles together several Microsoft Entra roles commonly used by security teams.

By assigning this group to the Contributor role:

- Anyone who already holds one of the included Entra roles **automatically gains access to use Security Copilot**.
- It simplifies access management by avoiding manual, individual assignments.
- It ensures secure access, since only users who already have permissions to view the underlying security data (via Microsoft plugins) are granted Copilot access.

### 🔐 The Entra roles included in this group are:

|**Microsoft Entra Role**|**Purpose**|
|---|---|
|**Global Administrator**|Full access to all Microsoft 365 and Azure services|
|**Security Administrator**|Manage security settings and alerts across Microsoft Defender and Entra|
|**Security Reader**|View-only access to security dashboards and reports|
|**Global Reader**|View-only access across all Microsoft 365 services|
|**Compliance Administrator**|Manage compliance features like DLP, eDiscovery, and retention policies|
|**Compliance Data Administrator**|Access to compliance data and reports|

This setup provides a **fast, secure, and scalable way** to onboard the right users into Security Copilot—especially those already working with Microsoft Defender, Sentinel, or Purview.


## Copilot plugins

Your role controls what activities you have access to, such as configuring settings, assigning permissions, or performing tasks. Copilot doesn't go beyond the access you have. Additionally, individual Microsoft plugins may have their own role requirements for accessing the service and data it represents. 

>[!note]
If a Copilot owner limits access to certain plugins, those plugins will appear **greyed out and marked as restricted** for users who aren’t allowed to use them.


An analyst that has been assigned a security operator role or a Copilot workspace contributor role is able to access the Copilot portal and create sessions, but to utilize the Microsoft Sentinel plugin would need an appropriate role like **Microsoft Sentinel Reader** to access incidents in the workspace. To access the devices, privileges, and policies available through the Microsoft Intune plugin, that same analyst would need another service-specific role like the Intune Endpoint Security Manager role.

Microsoft plugins in Copilot use the **OBO** (on behalf of) model – meaning that Copilot knows that a customer has licenses to specific products and is automatically signed into those products. Copilot can then access the specific products when the plugin is enabled and, where applicable, parameters are configured. Some Microsoft plugins that require setup may include configurable parameters that are used for authentication in-lieu of the OBO model.

Enabling of individual plugins and configuration of plugins is done per workspace.

|**Plugin**|**Purpose**|
|---|---|
|**Microsoft Defender XDR**|Investigate and respond to incidents across Defender for Endpoint, Identity, Office, and Cloud Apps|
|**Microsoft Defender Threat Intelligence**|Enrich investigations with threat intel on domains, IPs, and file hashes|
|**Microsoft Defender External Attack Surface Management**|Discover and monitor your organization’s external-facing assets|
|**Microsoft Sentinel (Preview)**|Query logs, incidents, and analytics from Sentinel workspaces|
|**Microsoft Entra**|Access identity-related data like sign-ins, risky users, and audit logs|
|**Microsoft Intune**|Retrieve device compliance and configuration data|
|**Microsoft Purview**|Access compliance and data governance insights|
|**Azure Firewall (Preview)**|Analyze firewall logs and policies|
|**Azure Web Application Firewall (Preview)**|Investigate WAF alerts and configurations|
|**Azure AI Search (Preview)**|Perform semantic search across indexed content|
|**Natural Language to KQL for Microsoft Sentinel**|Translate plain language into KQL queries for Sentinel|
|**Natural Language to KQL for Microsoft Defender XDR**|Translate plain language into KQL queries for Defender XDR|

These plugins are preinstalled and can be toggled on or off depending on your organization’s configuration and licensing.

### 🧵 Custom plugin

The Microsoft Security Copilot platform enables developers and users to write their own plugins that can be invoked to perform specialized tasks.

Non-Microsoft plugins are categorized as:

- Other: Give Copilot access to information and capabilities from services beyond Microsoft that your organization uses.
- Websites: Gives Copilot access to industry information from the public web. Currently, the public web plugin is supported.
- Custom: Enables developers and users to write their own plugins that can be invoked to perform specialized tasks.

You start by checking the owner settings for who can add and manage their own custom plugins and who can add and manage custom plugins for everyone in the organization. Once you configure the owner settings, you upload the file for your custom plugin. Uploading the files adds the plugin capability to Copilot. Once the plugin is added, you validate that is shows up as a system capability and start using it.


There are two types of custom plugins:

- Custom Copilot plugins that you develop
- Custom plugins developed with OpenAI’s API.

>[!Note]
>Every Copilot plugin requires a YAML or JSON formatted manifest file (for example: plugin.yaml or plugin.json) which describes metadata about the skill set and how to invoke the skills.

Owner settings, described in a previous unit, determines who can add and manage their own custom plugins and who can add and manage custom plugins for everyone in the organization. For Copilot users with the contributor role, availability of the option to set "Who can use this plugin" is dependent on how the owner settings for custom plugins are configured.


## knowledge base

Integrate a knowledge base into copilot, using file upload and then you do some basic testing with prompts that pull information from that knowledge base.

Disable by default, the user with the Copilot owner role, needs to enable file uploads.

If not enable:

1. Select the **Home** menu icon (hamburger icon).
2. Select **Owner settings**.
3. Scroll-down to **Files**. Select the drop-down and set it to **Contributors and owners can upload files**.
## Shared sessions

Copilot contributor role is the only requirement for sharing a session link or viewing it from that tenant.

When you share a session link, consider these access implications:

- Security Copilot needs to access a plugin's service and data to generate a response, but that same access isn't evaluated when viewing the shared session. For example, if you have access to devices and policies in Intune, and the Intune plugin is utilized to generate a response that you share, the recipient of the shared session link doesn't need Intune access to view the full results of the session.
- A shared session contains all the prompts and responses included in the session, whether it was shared after the first prompt or the last.
- Only the user that creates a session controls which Copilot users can access that session. If you receive a link for a shared session from the session creator, you have access. If you forward that link to someone else, it doesn't grant them access.
- Shared sessions are read-only.
- Sessions can only be shared with users in the same tenant that have access to Copilot.
- Some regions don't support session sharing via email.
    - `SouthAfricaNorth`
    - `UAENorth`

>[!Note]
>When you share a Microsoft Security Copilot session, you're sharing the **responses you received**, not the process or plugin access used to generate them. So even if you used data from Intune, Entra, or Sentinel—which typically require specific permissions—the recipient **can still view the full results of that session** as long as:
>1. They're in the same tenant.
>2. They've been explicitly granted access to the shared session by you (the session owner).
>3. They have a Copilot license or access provisioned.

## Manage promptbooks

Promptbook creation is available to all roles, including the ability to publish a custom promptbook for the tenant. Choose whether to publish a promptbook for yourself or the tenant at the time of creation.

Promptbooks in Microsoft Security Copilot contain one or more prompts that were together to accomplish specific security-related tasks. They run one prompt after another, building on previous responses.

You can create your own promptbook with the promptbook builder to automate investigation flows and optimize repetitive steps in Copilot that’s customized to your needs and requirements. Check if you have appropriate access and permissions to create promptbooks.

You can also share the promptbooks you’ve created with other users like your team mates so they can also benefit from your work.

>[!Tip]
>If you share a promptbook with a user who has different roles, permissions, or level of access to services or plugins than you do, the user might receive a different response from Copilot. The promptbook runs the prompts in the user’s session and Copilot reasons over data that is available to the currently signed in user.

## Create a custom promptbook

Create a custom promptbook from an **existing session** and then run that promptbook.
As part of the process, you templatize one of the prompts by editing the prompt with an input parameter, and then add a new prompt.
   
The Create a promptbook window opens. Here you populate the name, tags, and description fields for the promptbook, you configure an input parameter, and add a prompt. 
1. Name
2. Tags
3. Description
4. Select who can use this promptbook. Select the drop-down to view the options or **Just me**.

---
[SC-200: Mitigate threats using Microsoft Security Copilot - Training | Microsoft Learn](https://learn.microsoft.com/en-us/training/paths/sc-200-mitigate-threats-using-microsoft-copilot-for-security/)
