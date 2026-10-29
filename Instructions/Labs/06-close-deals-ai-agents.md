---
lab:
    title: 'Lab 6 - Close deals using the Sales Opportunity Agent'
    description: "Configure the Sales Opportunity Agent in Dynamics 365 Sales to research pipeline risk and suggest next actions for Contoso Coffee's opportunities."
    duration: '25 minutes'
    level: 300
    islab: true
---

# Lab 6 - Close deals using the Sales Opportunity Agent

> **Note**: The Sales Opportunity Agent is a **preview feature** that requires a Dynamics 365 Sales Premium license. This feature may not be fully available in all trial environments. **This lab is self-contained** — no other lab depends on completing it. If the required feature isn't available in your environment, review the steps to understand the configuration process and proceed to Lab 07.

Last quarter, three of Contoso Coffee's biggest deals stalled in the Proposal stage and were eventually lost. None of the reps were managing a bad pipeline — they were just overloaded. An equipment deal with multiple stakeholders can go quiet for two weeks, and by the time a rep notices, the prospect has moved on.

The **Sales Opportunity Agent** in Dynamics 365 Sales monitors your open pipeline, researches key accounts using Bing and CRM data, and surfaces risk signals and next-action suggestions on each rep's opportunity records.

In this lab, you'll configure the Sales Opportunity Agent for Contoso Coffee's pipeline.

This lab should take approximately **25** minutes to complete.

## Task 1: Access the Dynamics 365 AI Hub

Before you begin, confirm that you have the Power Platform administrator role, admin permissions in Dynamics 365 Sales, and a Copilot Studio license. The Sales Hub app must use the modern UI, and your organization's data policies must allow the Microsoft Copilot Studio, Direct Line channels in Copilot Studio, and Knowledge source with public websites and data connectors.

1. In Sales Hub, select the **Change area** at the bottom of the left navigation and select **App Settings**.

1. Go to **General** > **Overview** > **Dynamics 365 AI hub**.

1. In the **Agent manager** section, select **Create and manage agents**.

1. If the common **Prerequisites** page appears, review the following items:
   - **Microsoft Copilot Studio capacity**: Confirm that a green checkmark and **Done** appear.
   - **Move data across regions**: Confirm that a green checkmark and **Done** appear.
   - **AI prompts**: Confirm that a green checkmark appears. If it doesn't, select **Set up** and set the **AI prompts** toggle in **Settings** to **On**.

1. Return to the prerequisites page and select **Refresh**. Confirm that all common prerequisites are marked as **Done**. The **Create** option remains disabled until these prerequisites are complete.

## Task 2: Configure the Sales Opportunity Agent

The Sales Opportunity Agent researches open opportunities and surfaces risk signals for reps. It reads CRM records and public information but doesn't send email, so no Azure app registration or shared mailbox is needed.

### Open the agent creation flow

1. In Sales Hub, select **Change area** > **App Settings**.

1. Go to **General** > **Overview** > **Dynamics 365 AI hub** > **Create and manage agent**.

1. Select **Create**. In the **Create an AI agent** dialog, under **Sales Opportunity Agent**, select **Choose**.

   > [!TIP]
   > The agent settings also offer a **Setup assistant**, an AI-guided chat that walks you through configuration interactively. For this lab, you'll use the manual settings pages to understand each option individually.

### Configure prerequisites

1. On the **Prerequisites** page, configure the following:

   - **Bing search**: You should see a green checkmark already; if you don't, select **Accept terms** to open Power Platform admin center and accept the Bing search terms.
   - **Dataverse search**: The agent uses Dataverse Search to retrieve relevant records from Dynamics 365 Sales. If not already set up, select **Set up** to open the Power Platform admin center **Features** settings page. In the **Dataverse Search** section, enable the following options:
     - **Turn on search indexing to support Dataverse intelligence (Work IQ) in AI and agent experiences.**
     - **Show global search bar in all model driven apps and turn on search indexing to support search-only experiences.**

     After enabling these settings, select **Save**. Return to the agent configuration page and select **Refresh** to update the status of this prerequisite.
   - **Microsoft 365 Services** (optional but recommended): Allows the agent to read seller emails for engagement signals. If the **Mark as done** checkbox is available, select it to enable this feature. If the checkbox is grayed out or unavailable, skip this step and continue.

1. Select **Continue**.

### Configure the agent profile

1. In the **General** settings section, select **Agent profile**.

1. Fill in the following fields:
   - **Agent name**: Contoso Coffee Pipeline Watch
   - **Agent language**: English

### Configure company information

1. In the **General** settings section, select **Company info**.

1. Fill in the following fields:
   - **Company name**: Contoso Coffee
   - **Company website**: `https://www.contoso.com`
   - **Value proposition of what you sell to the selected opportunities**: `Commercial espresso machines and coffee equipment on flexible annual lease terms, with dedicated account management and same-day service response for multi-location hospitality and restaurant clients.`

   > [!NOTE]
   > The value proposition tells the agent what to look for when researching accounts. A specific, product-focused description produces more relevant insights than a generic one.

### Configure selection criteria

1. In the **General** section, select **Selection criteria**.

1. Fill in:
   - **Segment name**: Contoso Coffee Open Opportunities
   - **Description**: Open opportunities for commercial equipment leases over $10,000

1. Under **Filter conditions**, add the following:
   - **Status** equals **Open**
   - **Est. Revenue** is greater than or equal to **10000**

1. Select the **Consider opportunities created in the last** checkbox and enter **90** days to include recently created opportunities.

1. Select **Preview** and confirm that the sample contains opportunities you expect the agent to research. If no opportunities match, check that your sample records are open, have an estimated revenue of at least **10000**, and were created within the last **90** days.

### Configure refresh frequency

1. In the **Advanced** section, select **Refresh frequency**. Review the default setting. This controls how often the agent updates its research for each opportunity.

### Configure opportunity assessment

1. In the **Advanced** section, select **Opportunity assessment**.

1. Confirm the following fields are set to the correct columns from your opportunity records:
   - **Monetary value**: Est. revenue
   - **Estimated close date**: Est. close date

    These are the fields the agent uses to determine risk and importance for each opportunity. The defaults match the standard Dynamics 365 Sales opportunity fields — leave them as is unless your organization uses custom fields for these values.

### Configure knowledge sources

1. In the **Advanced** section, select **Research**.

1. Review the **Company research (Account overview, finances and news)** section. By default, the agent uses public web data (Bing search, company websites) to research accounts. No changes are needed for this section.

1. Expand the **Competitor research** section. Under **Key competitors**, select **+ Competitor** and add:
   - Fourth Coffee

   > [!NOTE]
   > This is the competitor you added to the Northwind Traders opportunity in Lab 05. The agent will use this list when no competitor is recorded on an opportunity record.

### Configure risk and importance criteria

1. In the **Advanced** section, select **Risk criteria**.

1. Expand **Default risk criteria**. Confirm that **Missing BANT info** is enabled under **Use in assessment**. This criterion flags deals missing Budget, Authority, Need, or Timeline information by the configured stage.

1. For **Stalled in stage**, turn on the **Use in assessment** toggle and configure the following:
   - **Opportunity is in**: **Propose**
   - **Stage for**: **14** days

    This criterion flags opportunities that remain in the Propose stage longer than the configured threshold. Leave the other risk criteria at their defaults.

1. Select **Importance criteria**. Review the six criteria and confirm that the following are enabled:

   | Criterion | Why it matters for Contoso Coffee |
   | --- | --- |
   | **Existing customer** | Multi-location clients with existing leases are higher-value renewal targets. |
   | **Large deal size** | Flags unusually large equipment orders compared to the account's past deals. |

    Leave all other criteria at their defaults.

### Save and start the agent

1. Before you save, review the left navigation panel and confirm that each section shows a green checkmark.

    If any section is missing a checkmark, select it and complete the required fields before continuing.

1. Select **Save**.

1. Select **Start agent** to activate the Sales Opportunity Agent. Confirm by selecting **Start agent** again.

   The agent begins processing opportunities that match your selection criteria. After research is available, reps can open it from the **Summary** section on an opportunity record by selecting **See full research**.

## Task 3: Review agent activity

1. In Sales Hub, select **Change area** > **Sales**, then select **Opportunities**.

1. From the views dropdown, select **My top opportunities from AI agent**. This view lists researched opportunities with high or medium importance. Open an opportunity that matches the selection criteria you configured.

   > **Note**: If the view is empty, the agent may not have completed its initial research, or no researched opportunities have high or medium importance. Return to a view of open opportunities and open a record that matched your selection criteria preview. If research isn't available yet, return after the agent processes the record.

1. In the **Summary** section at the top of the opportunity record, select **See full research**.

1. On the **Opportunity research** page, review the opportunity overview, importance and risk indicators, and available stakeholder, competitor, and account insights.

   > **Note**: If you enabled Microsoft 365 Services, a banner prompts the opportunity owner to grant permission for the agent to access their Microsoft 365 emails. Review the consent information before you grant permission. Email-based insights require relevant customer emails and may take additional time to appear.

You've configured the Sales Opportunity Agent to research Contoso Coffee's open opportunities and surface pipeline risks. Reps can use these insights to prioritize deals that need attention and plan their next actions.

