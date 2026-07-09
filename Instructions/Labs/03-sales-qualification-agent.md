---
lab:
    title: 'Lab 3 - Use the Sales Qualification Agent'
    description: 'Configure the Dynamics 365 Sales Qualification Agent to automatically research leads and hand off qualified prospects to sellers — reducing manual research time for Contoso Coffee.'
    duration: '40 minutes'
    level: 300
    islab: true
---

# Lab 3 - Use the Sales Qualification Agent

> [!NOTE]
> The Sales Qualification Agent requires a **Dynamics 365 Sales Premium** or **Microsoft 365 Copilot** license with Copilot Studio capacity. This feature may not be available in all trial environments. **This lab is self-contained** — no other lab depends on completing it. If the feature isn't available in your environment, review the steps to understand the configuration process and move on to Lab 04.

Contoso Coffee's reps are spending an average of three hours researching each prospect before their first call — looking up restaurant group locations, hotel brand footprints, and office campus sizes on LinkedIn, checking recent news, and reading through industry reviews. That's time that could be spent selling. Priya needs a better answer than "do it faster."

The **Sales Qualification Agent** is an AI agent built into Dynamics 365 Sales that automatically researches incoming leads, evaluates them against a target customer profile, drafts personalized outreach emails, and hands qualified leads to sellers — all without a rep lifting a finger.

In this lab, you'll configure the Sales Qualification Agent for Contoso Coffee's inbound leads.

This lab should take approximately **40** minutes to complete.

## Task 1: Verify prerequisites

The agent prerequisites are checked from within Sales Hub itself — the wizard walks you through each one when you first open the agent creation page.

1. In Sales Hub, select **App Settings** from the bottom of the left navigation.

1. Under **General settings**, select **Dynamics 365 AI hub**.

1. Select **Create and manage agents**.

1. A **Prerequisites** page opens listing all required items. All of these should have a **green check mark** next to them by default - that means that the setting is enabled and you don't need to take any extra action. If you do not see a green check mark, select **Set up** to enable these features. (Ask your instructor if you need help.)
   - **Microsoft Copilot Studio capacity**: Select **Set up** to open the Power Platform admin center and allocate Copilot Studio message capacity for your environment.
   - **Move data across regions**: Select **Accept terms** to open the Power Platform admin center and enable **Move data across regions** under **Generative AI features**.
   - **AI prompts**: Confirm that **AI prompts** is enabled in the same **Features** page.

1. Once all prerequisites have a green check mark, the **Create** button on the AI agents page becomes available. Select **Create**.

   > [!NOTE]
   > If any prerequisite can't be completed because the feature isn't available in your trial environment, this lab may not be fully supported. Review the remaining steps for learning purposes and proceed to Lab 04.

## Task 2: Select the agent type and create the app registration

1. On the agent type selection page, find the **Sales Qualification Agent** tile and select **Choose**.

1. On the mode selection screen, **Research** is selected by default. Leave it selected.

   > [!NOTE]
   > Research-only mode means the agent researches leads and prepares a summary and draft email for the seller, but it doesn't send emails autonomously. **Engage** mode enables full autonomous outreach, but requires an additional shared mailbox configuration and is typically reserved for high-volume scenarios.

1. Scroll down to view the Agent **Prerequisites** section.

1. The **Bing search** tile should already show a green check mark — no action needed.

1. On the **Create app in Azure** tile, select **Set up**.

    Azure opens directly to a new app registration form.

1. Fill in the registration details:
   - **Name**: Contoso Coffee Sales Qualification Agent
   - **Supported account types**: Single tenant only - Contoso

1. Select **Register**. Azure registers the app and may redirect you to the app overview page, or back to the App registrations list.

1. If you aren't already on the app overview page, select **Microsoft Entra ID** from the left navigation. Select the number next to **Applications**, then select the **All applications** tab. Select **Contoso Coffee Sales Qualification Agent** to open it.

1. Copy the **Application (client) ID** value and save it somewhere accessible (such as Notepad). You'll need this shortly.

## Task 3: Create the app user in Dataverse

1. Return to the Sales Hub browser tab. On the **Create app in Azure** tile, select the **Mark as done** checkbox.

1. On the **Create app user in Dataverse** tile, select **Set up**.

   The Power Platform admin center opens to the Application users page.

1. Select **+ New app user**.

1. In the **Create a new app user** pane, select **+ Add an app**.

1. Paste the **Application (client) ID** you copied earlier into the search box and select the **Contoso Coffee Sales Qualification Agent** app. (It may already appear in the list - you can go ahead and select it.) Select **Add**.

1. Set the **Business unit** to your root business unit.

1. Under **Security roles**, select the pencil icon and assign the **AIsalesperson** role.

1. Select **Save**, select **Save** again, then select **Create**.

1. Return to the Sales Hub tab and select **Mark as done** on the **Create app user in Dataverse** tile.

    All agent-specific prerequisites should now have check marks. Select **Continue** to proceed to the agent configuration page.

## Task 4: Configure the Sales Qualification Agent

You're now on the agent configuration page. Work through each section from top to bottom.

### Agent profile

1. Select **Manual setup** to configure the agent manually.

1. In the **Agent profile** section, fill in the following:
   - **Agent name**: Contoso Coffee Lead Research Agent
   - **What should this agent do**: Research inbound trade show leads, evaluate them against Contoso Coffee's target customer profile, and prepare research summaries and draft outreach emails for sellers.
   - **Agent user**: Select the **Contoso Coffee Sales Qualification Agent** app user you created in Task 3. (If it doesn't show up as an option, try refreshing your browser.)
   - **Agent language**: English

### Company info

1. In the **Company info** section, fill in the following:
   - **Company name**: Contoso Coffee
   - **Company website**: www.contoso.com

### Products

1. In the **Products** section, enter the following value proposition:

    `Contoso Coffee sells commercial espresso machines and coffee makers to businesses across the food service and hospitality industries, including restaurants, hotels, corporate offices, and convention centers. We serve organizations with 50 to 5,000 employees across North America. Our key offerings include commercial espresso machines, commercial batch brew coffee makers, 12- to 36-month equipment leases, and service and maintenance contracts.`

   > [!NOTE]
   > The Products description is used to auto-generate handoff criteria later. Be as specific as possible about your target customers and the problems you solve.

### Selection criteria

1. In the **Selection criteria** section, enter a name and description:
   - **Name**: FoodService Summit trade show leads
   - **Description**: Hot and warm leads captured at food service and hospitality trade shows, ready for AI-assisted research before seller handoff.

1. In the **Segment conditions** section, remove the default conditions by selecting the ellipsis **(...)** and then selecting **Delete**.

1. Then add the following conditions by selecting **+ Add** > **Add row**:
   - Lead Source | Equals | Trade Show
   - Rating | Equals | Hot, Warm

    This tells the agent to process trade show leads rated Hot or Warm. Cold leads are excluded.

### Email instructions

1. In the **Email instructions** section, under **Outreach emails**, leave the default option **AI-generated personalization** selected.

    This allows the agent to generate personalized email content for each lead using generative AI based on the research it produces.

### Email address validation

1. In the **Email address validation** section, confirm the default field **Email (emailaddress1)** is selected.

    This is the standard email field on the Lead table and matches the field used in the leads you imported. No change is needed.

### Handoff criteria

1. In the **Handoff criteria** section, select **Generate** to auto-generate the target customer profile based on the Products description you entered earlier.

    The agent suggests criteria such as industry, company size, decision-making roles, and revenue range based on your product value proposition. Review the generated criteria and adjust if needed.

### Assignment rules

1. In the **Assignment rules** section, configure how the agent assigns researched leads to sellers:
   - Make sure **Specific seller** is selected.
   - Set the seller to **Jordan Park**.
   - Under **Add supervisor**, select your administrator account.

### Research (knowledge sources)

1. In the **Research** section, review the default knowledge source configuration.

   > [!NOTE]
   > In a production environment, you'd add public URLs for your product pages, solution briefs, and competitive comparisons — and SharePoint documents such as pricing guides and objection-handling briefs. For this lab, skip adding sources and proceed.

### Agent emails

1. The **Agent emails** section is used in **Research and engage** mode to configure a shared mailbox for autonomous outreach. Since you selected **Research-only** mode, this section is not required. Skip it.

1. Select **Save** to save all your configuration changes.

1. Confirm all sections show a green check mark.

### Start agent

1. Select **Start agent** in the upper-right corner, and then select **Start agent** again to confirm.

1. Select **Go to agent list**.

   > [!NOTE]
   > Starting the agent may take several minutes. Wait for the status to change from **Saving** to **On** before proceeding.

## Task 5: View a lead being worked on by the agent

1. In the bottom-left corner of the screen, select the area selector that currently shows **App Settings** and switch it to **Sales**. Then select **Leads** from the left navigation.

1. Select **+ New** on the command bar to create a new lead for the agent to process.

1. Fill in the following fields:
   - **Topic**: Espresso machine inquiry
   - **First name**: Alex
   - **Last name**: Rivera
   - **Job Title**: General Manager
   - **Company**: Northgate Hospitality Group
   - **Email**: alex@northgatehospitality.com

1. In the header, fill in the following fields:
   - **Lead Source**: Trade Show
   - **Rating**: Hot

1. Select **Save**. The agent monitors for new leads matching your selection criteria (Trade Show + Hot or Warm) and will begin researching this lead automatically.

   > [!NOTE]
   > The agent processes new leads asynchronously. It may take several minutes before research results appear on the record. While the agent works, the lead's **Owner** changes to the **Contoso Coffee Sales Qualification Agent**, and the research findings appear in the **Leads handed over by AI agent** view. If you don't see them yet, wait a few minutes and then refresh the page.

1. Return to the **My Open Leads** view and select the dropdown next to the view name.

1. Select the **Leads handed over by AI Agent** view.

1. Confirm that the lead you just created appears in the view, which indicates the agent has picked it up for processing.

1. Select the lead to open the **Lead Research** page. Review the agent's findings, including the **Suggested action** (with a draft outreach email), **Key insights** (why the lead is rated hot, warm, or cold), and **Deeper insights** (company overview, finances, News, and Competitor Insights).

## Task 6: See agent insights

1. In the bottom-left corner, select the area selector and switch it to **App Settings**. Under **General settings**, select **Dynamics 365 AI hub**.

1. On the **AI optimization hub** tile, select **See insights**.

1. The insights for the **Sales Qualification Agent** will appear.

1. Review the dashboard metrics:
   - **Total leads researched** — how many leads the agent has evaluated
   - **AI agent lead handling rate** — the percentage of leads the agent handled end to end
   - **AI agent lead handoff rate** — the percentage of evaluated leads handed off to sellers
   - **Total leads disqualified** — leads the agent determined didn't match the target profile

   > [!NOTE]
   > Because your environment is new, the dashboard may show minimal data. This is expected. In a live environment, these metrics would populate within a few hours of activation.

1. In the upper-right corner of the dashboard, select the **View leads category** dropdown and choose **Leads disqualified by AI agent** to see any leads the agent has determined don't match Contoso Coffee's target customer profile.

You've successfully configured the Sales Qualification Agent. Contoso Coffee's reps will no longer spend three hours researching each lead manually — the agent does that automatically and delivers a research brief, a lead rating, and a draft email directly to the seller.
