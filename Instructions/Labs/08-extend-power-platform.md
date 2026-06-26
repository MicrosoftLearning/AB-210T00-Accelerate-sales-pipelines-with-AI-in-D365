---
lab:
    title: 'Lab 8 - Extend Dynamics 365 Sales with Power Platform'
    description: 'Use Power Automate and Copilot Studio to extend Dynamics 365 Sales with automated workflows and an AI-powered sales coaching agent for Contoso Coffee.'
    duration: '35 minutes'
    level: 200
    islab: true
---

# Lab 8 - Extend Dynamics 365 Sales with Power Platform

Marcus Webb, Contoso Coffee's sales operations manager, has a running list of manual tasks that cost the team hours every week:

- Every time a high-value opportunity is created above a certain revenue threshold, Marcus manually emails the VP of Sales so they can prioritize follow-up.
- When a deal closes as won, someone has to update a SharePoint list that the finance team uses for billing.
- Sellers frequently ask Marcus how to handle objections or what the standard pitch is for a particular product — and he answers the same questions over and over.

None of these problems require a developer. They all require Power Platform.

In this lab, you'll build a Power Automate flow that triggers automatically when an opportunity reaches the Propose stage, and you'll set up a Copilot Studio agent that answers sellers' common questions directly inside Sales Hub.

This lab should take approximately **35** minutes to complete.

## Before you start

You need to be signed in to Sales Hub. You'll also need to access **Power Automate** at `https://make.powerautomate.com` and **Copilot Studio** at `https://copilotstudio.microsoft.com`. Use the same lab credentials for all three.

## Task 1: Create a Power Automate flow from an opportunity

You'll create a flow that sends Marcus an email notification whenever a new opportunity is created with an estimated revenue above $50,000. This replaces the manual check-in.

1. Open a new browser tab and go to `https://make.powerautomate.com`.

1. Sign in with your lab credentials.

1. Select **Create** in the left navigation.

1. Select **Automated cloud flow**.

1. In the **Flow name** field, enter: `Notify Marcus - High-Value New Opportunity`

1. In the **Choose your flow's trigger** search box, type `When a row is added` and select **When a row is added, modified or deleted** (Microsoft Dataverse).

1. Select **Create**.

1. In the trigger card, configure the following:
   - **Change type**: **Added**
   - **Table name**: **Opportunities**
   - **Scope**: **Organization**

1. Select **+** under the trigger card to add a condition.

1. Search for and select **Condition** (Control).

1. In the condition:
   - **Value (left side)**: Select the lightning bolt icon to use dynamic content and choose **Est. Revenue**
   - **Operator**: **is greater than**
   - **Value (right side)**: `50000`

1. In the **True** branch (when the condition is true), select **+** to add an action.

1. Search for and select **Send an email (V2)** from the **Office 365 Outlook** connector. (You may be prompted to sign in - select **Sign in** and follow the prompts to sign in with your credentials.)

1. Fill in the email details:
    - **To**: Enter your lab user's email address (to simulate Marcus receiving the notification). This will likely start with MOD, so you can start typing MOD and select it when it appears.
    - **Subject**: `High-value opportunity created: [Topic]`
    
      To insert the opportunity name dynamically, select the field and add dynamic content: **Topic**.

    - **Body**: 
      ```
      Hi Marcus,

      A new high-value opportunity has been created and may need your attention.

      Opportunity: [Topic]
      Estimated Revenue: [Est. Revenue]
      Estimated Close Date: [Est. Close Date]

      Please review and assign this opportunity as appropriate.

      This notification was sent automatically by Dynamics 365 Sales.
      ```
      
      Replace the bracketed placeholders with the corresponding dynamic content fields.

1. Select **Save** in the top-right corner of Power Automate.

## Task 2: Test the flow

1. In the Power Automate designer, select **Test** in the top-right corner.

1. In the **Test Flow** pane, select **Manually**, then select **Test**.

   Power Automate puts the flow into listening mode and displays a message telling you to perform the trigger action.

1. Switch to your Sales Hub browser tab, select **Opportunities** in the left navigation, and select **+ New**.

1. Fill in the following fields:
   - **Topic**: `Test - High-Value Flow Trigger`
   - **Est. Revenue**: `75000` (you'll find this field in the header)
   - **Est. Close Date**: any future date (this is also in the header)

1. Select **Save** on the opportunity record.

1. Return to the Power Automate tab. The flow detects the new record and begins running automatically. Watch each step — a green checkmark appears on each card as it succeeds.

1. When the run completes, select **Done**, then close the Power Automate tab.

1. Open a new browser tab and go to `https://outlook.office.com` to confirm you received an email with the subject line `High-value opportunity created:` followed by the opportunity name.

    > **Note**: If any step shows a red X, select it to expand the error details. A common issue is a missing Outlook connection — reconnect by selecting **Sign in** in the action card.

## Task 3: Configure a Copilot Studio agent for sales coaching

Marcus answers the same questions from sellers every week: "What's our lease pitch for a hotel with 20 locations?" "How do we handle the pricing objection?" "What's covered under the service contract?"

You'll create a lightweight Copilot Studio agent that sellers can ask these questions to directly inside Dynamics 365 Sales.

1. Open a new browser tab and go to `https://copilotstudio.microsoft.com`.

1. Sign in with your lab credentials.

1. On the **Home** page, select **Agent** under **Start building from scratch**.

1. Name the agent `Contoso Sales Coach` and select **Create.**

1. In the **Instructions** section, enter:
   `You are a sales coaching assistant for Contoso Coffee. You help sellers with product pitches, objection handling, competitive comparisons, and pricing guidance. Answer questions about commercial espresso machines, coffee makers, equipment leases, and service contracts. Be concise, friendly, and specific. Always tailor your advice to the customer's industry or location count if that information is provided.`

1. Select **Save.**

1. Select the **Topics** tab in the top navigation to add specific response scenarios.

1. Select **+ Add topic** > **From blank**.

1. Name the topic: `Espresso machine lease pitch`.

1. In the **Describe what this topic does** field, enter:
   `Use this topic when a seller asks for help pitching an equipment lease, asks for espresso machine talking points, or wants to know what to say when discussing leasing options with a customer.`

1. Select **+** and select **Send a message**. In the **Message** node that appears in the conversation designer, enter:

    ```
    Here's Contoso Coffee's standard equipment lease pitch:

    Lead with the outcome: "We help businesses like yours serve better coffee without a large upfront investment — a 36-month lease means no capital expenditure and predictable monthly costs."

    Address the pain point: Ask "What does your current equipment situation look like? Most clients we work with are dealing with aging machines and expensive reactive repairs."

    Handle the risk concern: "Every lease includes our monthly service contract — two preventive maintenance visits a year and unlimited on-call support during business hours. If it breaks, we fix it."

    Close with proof: "We recently leased 12 Espresso Machine - Pro units to a restaurant group in the Southwest. Their beverage revenue went up 18% in the first quarter after installation — happy to share their feedback."
    ```

1. Select **Save**.

1. Select **back** to return to the list of tpics.

1. Add one more topic. Select **+ Add topic** > **From blank**.

1. Name it `Pricing objection`.

1. In the **Describe what this topic does** field, enter:
   `Use this topic when a seller asks how to respond to a pricing objection, price pushback, or a customer who says the product is too expensive.`

1. In the message node, enter:

    ```
    When a prospect pushes back on price, try this:

    1. Acknowledge: "I hear you — budget is always a consideration."
    2. Reframe to value: "Let me make sure we're comparing the right things. What are you currently paying for equipment repairs and downtime? Most clients find reactive maintenance costs more than a lease with a service contract included."
    3. Highlight the total cost of the alternative: "A single emergency equipment repair can run $500–$1,200. With our lease, that's covered. You're paying for certainty, not just hardware."
    4. Offer a smaller entry point: "We could also start with leasing machines for your highest-volume locations this quarter and expand to the remaining locations in Q3 — that keeps the initial commitment manageable."

    Do not discount on the first pushback. Escalate to Marcus if the prospect requests more than 10% off.
    ```

1. Select **Save**.

1. In the test panel, type `how do I pitch a lease` and confirm the agent responds with the espresso machine lease pitch you defined.

1. Type `they said it's too expensive` and confirm the pricing objection response appears.

## Task 4: Publish and test the agent

1. Select **Settings** in the top navigation bar.

1. Select **Security**, then select **Authentication**.

1. Select **No authentication**, then select **Save** and select **Save** again.

   > **Note**: This setting allows the Demo Website channel to work in a trial environment without requiring end-user sign-in. For production deployments, you would configure an appropriate authentication provider.

1. Close the Settings panel and select **Publish** in the top navigation bar.

1. Select **Publish** to publish the current version of your agent.

1. Wait for the publish confirmation message.

    > **Note**: Embedding a custom Copilot Studio agent directly in the Dynamics 365 Sales Hub sidebar requires environment-level admin configuration that is outside the scope of this lab. 

**Congratulations!** You've worked through all nine of Contoso Coffee's requirements. Starting from a blank Dynamics 365 environment, you:

- Configured territories, numbering, and Copilot summarization
- Imported and qualified leads from a food service trade show
- Set up AI-powered lead research (optional Premium feature)
- Built a centralized product catalog with consistent pricing and volume discounts
- Managed a multi-location equipment opportunity from creation to a won close
- Deployed AI agents to monitor pipeline risk and automate outreach (optional Premium feature)
- Extended the platform with Power Automate workflows and a Copilot Studio coaching agent

Priya now has a sales system that works the way Contoso does — and you have the hands-on experience to build one like it anywhere.
