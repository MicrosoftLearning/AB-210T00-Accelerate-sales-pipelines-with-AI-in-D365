---
lab:
    title: 'Lab 6 - Close deals using AI agents'
    description: "Configure the Sales Opportunity Agent and Sales Close Agent in Dynamics 365 Sales to automatically research pipeline risk and send follow-up emails on Contoso Coffee's behalf."
    duration: '45 minutes'
    level: 300
    islab: true
---

# Lab 6 - Close deals using AI agents

> [!NOTE]
> The Sales Opportunity Agent and Sales Close Agent are **preview features** that require a Dynamics 365 Sales Premium license. The Sales Close Agent additionally requires Microsoft Entra Application Developer permissions and Exchange Administrator access to complete the prerequisite setup. These features may not be fully available in all trial environments. **This lab is self-contained** — no other lab depends on completing it. If the required features aren't available in your environment, review the steps to understand the configuration process and proceed to Lab 07.

Last quarter, three of Contoso Coffee's biggest deals stalled in the Proposal stage and were eventually lost. None of the reps were managing a bad pipeline — they were just overloaded. An equipment deal with multiple stakeholders can go quiet for two weeks, and by the time a rep notices, the prospect has moved on.

Dynamics 365 Sales includes two AI agents designed to fix this:

- The **Sales Opportunity Agent** monitors your open pipeline, researches key accounts using Bing and CRM data, and surfaces risk signals and next-action suggestions on each rep's opportunity records.
- The **Sales Close Agent** goes further: it autonomously sends personalized follow-up emails from a shared mailbox on behalf of the seller, monitors replies, and escalates to the rep when a human response is needed.

In this lab, you'll configure both agents for Contoso Coffee's pipeline.

This lab should take approximately **45** minutes to complete.

## Task 1: Access the Dynamics 365 AI Hub

1. In Sales Hub, under **Change area** at the bottom of the left navigation, select **App Settings**.

1. Go to **General settings** > **Dynamics 365 AI hub**.

1. In the **Agent manager** section, select **Create and manage agents**.

## Task 2: Configure the Sales Opportunity Agent

The Sales Opportunity Agent researches open opportunities and surfaces risk signals for reps. It has lighter infrastructure requirements than the Sales Close Agent — it reads CRM records and public information but doesn't send email, so no Azure app registration or shared mailbox is needed.

### Open the agent creation flow

1. In Sales Hub, select **Change area** > **App Settings**.

1. Go to **General settings** > **Dynamics 365 AI hub** > **Create and manage agent**.

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

1. In the **General** settings section, select **Agent profile**. (It should open here by default.)

1. Fill in the following fields:
   - **Agent name**: Contoso Coffee Pipeline Watch
   - **Agent language**: English

### Configure company information

1. In the **General** settings section, select **Company info**.

1. Fill in the following fields:
   - **Company name**: Contoso Coffee
   - **Company website**: `https://www.contoso.com`
   - **Value proposition**: Commercial espresso machines and coffee equipment on flexible annual lease terms, with dedicated account management and same-day service response for multi-location hospitality and restaurant clients.

   > [!NOTE]
   > The value proposition tells the agent what to look for when researching accounts. A specific, product-focused description produces more relevant insights than a generic one.

### Configure selection criteria

1. In the **Guidance** section, select **Selection criteria**.

1. Fill in:
   - **Segment name**: Contoso Coffee Open Opportunities
   - **Description**: Open opportunities for commercial equipment leases over $10,000

1. Under **Filter conditions**, add the following:
   - **Status** equals **Open**
   - **Est. Revenue** is greater than or equal to **10000**

1. Select the **Consider opportunities created in the last** checkbox and enter **90** days to include recently created opportunities.

### Configure refresh frequency

1. In the **Advanced** section, select **Refresh frequency**. Review the default settings — this controls how often the agent updates its research for each opportunity.

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

1. Review the list of risk criteria by expanding the **Default risk criteria** section — all are enabled by default. Each criterion has a configurable threshold. For Contoso Coffee, review the following and adjust if needed:

   | Criterion | Default action |
   | --- | --- |
   | **No recent engagement** | Keep enabled. Equipment lease deals often go quiet — this surfaces deals with no contact for the default window. |
   | **Stalled in stage** | Keep enabled. Consider reducing the threshold (for example, 14 days) to catch deals that stall in the Propose stage. |
   | **Missing BANT info** | Keep enabled. Flags deals missing Budget, Authority, Need, and Timeline information. |

1. Select **Importance criteria**. Review the six criteria and confirm that the following are enabled:

   | Criterion | Why it matters for Contoso Coffee |
   | --- | --- |
   | **Existing customer** | Multi-location clients with existing leases are higher-value renewal targets. |
   | **Large deal size** | Flags unusually large equipment orders compared to the account's past deals. |

    Leave all other criteria at their defaults.

### Save and start the agent

1. Before saving, review the left navigation panel and confirm that each section shows a green checkmark:
   - **General**: Agent profile, Company info, Selection criteria
   - **Advanced**: Refresh frequency, Opportunity assessment, Research, Risk criteria, Importance criteria, Connected skills

    If any section is missing a checkmark, select it and complete the required fields before continuing.

1. Select **Save**.

1. Select **Start agent** to activate the Sales Opportunity Agent. Confirm by selecting **Start agent** again.

   The agent is now active. Reps will see an **Opportunity research** section on their opportunity records, populated with account news, stakeholder research, and engagement risk signals.

1. It may take a while for your agent to start. In the meantime, select **Go to agent list** and continue to Task 3.

## Task 3: Set up prerequisites for the Sales Close Agent

The Sales Close Agent sends emails on behalf of sellers, so it requires a dedicated Azure identity, a shared Exchange mailbox, and server-side synchronization. All four prerequisites are managed from within the agent settings page — each has a **Set up** button that launches the correct tool, and a **Mark as done** checkbox to confirm completion before proceeding.

### Open the Sales Close Agent settings

1. In **App Settings**, select **Dynamics 365 AI hub**, then select **Create and manage agents**.

1. Select **Create**. Under **Sales Close Agent**, select **Choose**.

    The **Prerequisites** page opens with four required steps.

### Create the Azure app registration

1. In the **Create app in Azure** section, select **Set up**.

   This opens the app registration page in Microsoft Entra ID.

1. Select **+ New registration** and fill in:
   - **Name**: Contoso Coffee Sales Close Agent
   - **Supported account types**: Single tenant only - Contoso

1. Select **Register**. Azure registers the app and may redirect you to the app overview page, or back to the App registrations list.

1. If you aren't already on the app overview page, select **Microsoft Entra ID** from the left navigation. Select the number next to **Applications**, then select the **All applications** tab. Select **Contoso Coffee Sales Close Agent** to open it.

1. Copy the **Application (client) ID** value and save it somewhere accessible (such as Notepad). You'll need this shortly.

1. Return to the **Prerequisites** page in Sales Hub and select the **Mark as done** checkbox for **Create app in Azure**.

### Create a shared mailbox

1. In the **Create shared mailbox** section, select **Set up**.

   This opens the Exchange admin center.

1. Go to **Recipients** > **Mailboxes** and select **+ Add a shared mailbox**.

1. Fill in the following fields:
   - **Display name**: Contoso Coffee Sales Agent
   - **Email address**: `sales-agent@<your-domain>`

1. Select **Create**.

1. Return to the **Prerequisites** page and select **Mark as done** for **Create shared mailbox**.

### Create an app user in Dataverse

1. In the **Create an app user in Dataverse** section, select **Set up**.

   This opens the Power Platform admin center.

1. Select your environment, then go to **Settings** > **Users + permissions** > **Application users**.

1. Select **+ New app user**. In the **Create a new app user** pane:
   - Select **+ Add an app** and enter the **Application (client) ID** you copied from Azure. (If you see the app in the list, you can select it there.) Select **Add**.
   - Set the business unit to the root business unit.
   - Select the pencil icon to add a security role. Set the security role to **AISalesPerson** and select **Save**, then **Save** again to confirm the role assignment.

1. Select **Create**.

1. Return to the **Prerequisites** page and select **Mark as done** for **Create app user in Dataverse**.

### Configure server-side synchronization

1. In the **Configure server side sync** section, select **Set up**.

   This opens the **My Active Mailboxes** view in Dynamics 365 Advanced Settings.

1. Change the view to **All Mailboxes** and open the mailbox for the app user you just created (**Contoso Coffee Sales Close Agent**).

1. Replace the email address with the shared mailbox address.

1. Select **Save**, then select **Approve Email**. Select **OK** to confirm.

1. Select **Test & Enable Mailbox** and select **OK** to start the test.

1. Wait for the configuration status to show **Success** for both incoming and outgoing email.

1. Return to the **Prerequisites** page and select **Mark as done** for **Configure server side sync**.

1. Select **Continue**.

## Task 4: Configure and start the Sales Close Agent

With all prerequisites complete, configure the agent's behavior.

### Agent profile and products

1. In the **General** settings section, select **Agent profile** and fill in:
   - **Agent name**: Contoso Coffee Follow-up Agent
   - **Agent user**: Select the app user you created in Task 3 (**Contoso Coffee Sales Close Agent**). If it isn't showing up, return to the Agent manager and refresh - it may take a few minutes.
   - **Agent language**: English
   - **Email signature**: Select **Modify signature**. Edit the default signature in the editor to reflect Contoso Coffee's brand, and select **Save & Close** when done:

     ```
     Contoso Coffee — Fueling Great Workdays
     Commercial Espresso & Coffee Equipment | Annual Lease Programs
     Questions? We'd love to chat over coffee. https://www.contoso.com
     ```

   - **AI Disclaimer**: Replace the default disclaimer to match Contoso's brand by entering the following text:

     `P.S. This message was brewed by an AI assistant — no caffeine required. A real human from the Contoso Coffee team is always happy to chat if you'd prefer.`

1. In the **General** settings section, select **Products** and configure the following:

   - **Products**: Select the following four products from the dropdown (created in Lab 04):
     - Batch Brew Coffee Maker
     - Espresso Machine - Pro
     - Espresso Machine - Standard
     - Equipment Service Contract

     After selecting the products, they'll appear in red — the agent requires a product page URL for each one, which wasn't configured in Lab 04. Select **Add missing info** and fill in the following URLs:

     | Product | URL |
     | --- | --- |
     | Batch Brew Coffee Maker | `http://www.contoso.com/batch` |
     | Espresso Machine - Pro | `http://www.contoso.com/pro` |
     | Espresso Machine - Standard | `http://www.contoso.com/standard` |
     | Equipment Service Contract | `http://www.contoso.com/service` |

     Select **Update** to save the changes.

   > [!NOTE]
   > These URLs use http://contoso.com, which redirects safely to microsoft.com in a trial environment — they serve as placeholder product page links for the agent to include in outreach emails.

   - **Value proposition of your product**: Enter a value proposition that explains why a customer should choose Contoso Coffee's equipment:

     `Commercial-grade espresso machines built for high-volume hospitality environments. Available on flexible annual lease terms with same-day service response and dedicated account management.`

   - **What should we use to search your product knowledge?**: Select up to three fields the agent uses to match relevant product documentation. Select **Product** and **Description**.

   - **Where do you store customer friendly product name?**: Select **Name**.

### Configure target customers

1. In the **Guidance** section, select **Target customer**.

1. For **Record type**, select **Opportunity**.

1. Under **Filter conditions**, add:
   - **Status** equals **Open**
   - **Est. revenue** is greater than or equal to **10000**
   - **Email Address** **contains data** (required — the agent can only contact customers with a valid email address)

1. Select **Preview** to confirm the agent is targeting the right records.

### Configure email delivery

1. In the **Guidance** section, select **Email delivery**.

1. Review the compliance profile. The default profile is sufficient for most environments.

### Configure email content

1. In the **Guidance** section, select **Email content**.

1. Under **Outreach email templates**, select **Choose template** to pick an existing email template.

1. Select **Meeting for product demo requests - introductory email**. (If it isn't available in your environment, you can pick any available template.)

1. Under **Tone for emails**, enter the following prompt:

    `Professional and helpful. Reference the customer's commercial coffee equipment needs. Don't be pushy. Close with a single clear call to action — a meeting or a product demo.`

1. Select **Save**.

### Configure knowledge sources

1. In the **Knowledge** section, select **Knowledge sources**.

1. Review the **Agent playbook** section. The **Default Agent Playbook** is already uploaded and configured — no changes are needed.

1. In the **Product documentation** section, select **Manage**.

   This opens Microsoft Copilot Studio in a new browser tab. If you're prompted to select a Team, select **start trial** and follow the wizard to create a trial. If prompted for your phone number, you can enter `1234567891`. If you already have a license for Microsoft Copilot Studio, navigate to **https://copilotstudio.microsoft.com/**, select the environment picker in the upper-right and confirm that **Sales Trial** environment is selected.
   
   > [!NOTE]
   > If Copilot Studio doesn't load in a new tab, go to the Power Platform admin center and open the **Sales Trial** environment. Copy the **Environment ID** and then append it to the Copilot Studio URL in the following format: `https://copilotstudio.microsoft.com/environments/<Environment ID>`. Replace `<Environment ID>` with the ID of your Sales Trial environment.

1. Select **Agents** in the left navigation, then select **Sales Close Agent**.

1. In the agent's **knowledge** section, select **+ Add knowledge**, then select **Public websites**.

1. Enter `https://contoso.com` and select **Add**.

1. Select **Add to agent**.

1. Select **Publish**, then select **Publish** again to apply the changes.

   > [!NOTE]
   > You must publish in Copilot Studio for the knowledge source to take effect. The agent cannot start until at least one product documentation source is published.

1. Return to the Sales Close Agent **Knowledge sources** tab in Sales Hub and select **Save**.

1. When you're satisfied with the configuration, select **Start agent**. On the confirmation dialog, select **Start agent** again.

1. Select **Go to agent list** to return to the agent list.

   The Sales Close Agent is now active. It selects opportunities matching your target criteria, sends personalized outreach emails from the shared mailbox, monitors replies, and escalates to the rep when a human response is needed.

## Task 5: Review agent activity

1. In Sales Hub, at the bottom of the left navigation, select **Sales**, navigate to **Opportunities**, and open any open opportunity.

1. Scroll to the **Opportunity research** section. This is where the Sales Opportunity Agent surfaces account research, recent news, and engagement risk signals for each deal.

1. Under **Customers**, select **Contacts**.

1. From the view selector, choose **Contacts from Sales Close Agent**.

1. Open a contact that has been processed by the Sales Close Agent.

1. Review the **Timeline** to view the actions performed by the Sales Close Agent on the contact record.

   > [!NOTE]
   > In a trial environment, the agents might not have processed any records yet. Agent-generated insights and processed records appear only after the agents complete their scheduled runs. If no records are available in the Contacts from Sales Close Agent view, return later after the agents have had time to process customer records.

You've configured two AI agents that address Contoso Coffee's pipeline risk problem. The Sales Opportunity Agent ensures no deal goes unresearched. The Sales Close Agent ensures no follow-up falls through the cracks — without adding to the rep's workload.

