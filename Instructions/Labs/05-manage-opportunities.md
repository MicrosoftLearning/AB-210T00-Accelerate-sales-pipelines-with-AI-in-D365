---
lab:
    title: 'Lab 5 - Manage opportunities in Dynamics 365 Sales'
    description: 'Track a complex enterprise deal end-to-end in Dynamics 365 Sales — adding products, stakeholders, and competitor data — then close it as won.'
    duration: '40 minutes'
    level: 200
    islab: true
---

# Lab 5 - Manage opportunities in Dynamics 365 Sales

In Lab 02, you qualified Maya Torres's lead and Dynamics 365 automatically created an opportunity for Northwind Traders' commercial espresso machine lease. But qualifying a lead is just the beginning. A 12-location deal with a Director of Operations involves multiple people, a real decision-making process, competitors, and a negotiation.

Jordan Park needs to manage this deal properly — not in a spreadsheet, not in their head, and not in a long email thread with their manager. In Dynamics 365 Sales, an opportunity record is the single source of truth for everything related to a deal: the products, the stakeholders, the close date, and the story of how the deal got won (or lost).

In this lab, you'll open the Northwind Traders opportunity, add the products from Contoso Coffee's catalog, identify the stakeholders and a competitor, move the deal through the sales process, and then close it as won.

This lab should take approximately **40** minutes to complete.

## Before you start

You need to be signed in to Sales Hub. This lab builds on data from earlier labs:
- The **Maya Torres** opportunity from Lab 02 (Qualify a lead)
- The **Contoso Coffee North America - USD** price list and products from Lab 04

If you don't have the Maya Torres opportunity, you can create a new opportunity manually:

1. Go to **Sales**, under **Sales**, select **Opportunities**.

1. Select **+ New**.

1. Add the following opportunity details:
    - **Topic**: Commercial espresso machine lease - 12 locations
    - **Contact**: Maya Torres
    - **Estimated Close Date**: 60 days from today

1. Select **Save**.

1. In the **My Open Opportunities** view, select the opportunity you just created and make sure the **Potential Customer** is set to **Northwind Traders**. If **Northwind Traders** isn't added, select the **Potential Customer** field, search for **Northwind Traders**, and then select it.

## Task 1: Open and review the opportunity

1. In Sales Hub, select **Opportunities** in the left navigation.

1. Find and open the **Commercial espresso machine lease - 12 locations** opportunity for **Northwind Traders**. Hover over the **Topic** name and select the **Go to main form** icon to open the record.

1. Review the **Business process flow** bar at the top of the form. You should see four stages: **Qualify**, **Develop**, **Propose**, and **Close**.

    The **Qualify** stage should show a checkmark indicating it's complete, and the opportunity should currently be in the **Develop** stage. You'll move it through the remaining stages as you work through this lab. If you created the opportunity manually in the previous steps, it starts in the **Qualify** stage. Select the **Qualify** stage, then select **Next Stage** to advance the opportunity to **Develop** before continuing.

1. Review the key fields on the opportunity header and update any that are blank:
   - **Account**: Northwind Traders
   - **Est. Close Date**: Set this to approximately 60 days from today
   - **Est. Revenue**: Blank for now — this will populate after you add products in Task 2
   - **Owner**: Your current user
   - **Contact**: Maya Torres

## Task 2: Add products to the opportunity

Jordan quoted this deal verbally as "around $300 a month." Let's replace that guess with actual line items from the product catalog.

1. On the opportunity record, select the **Products** tab.

1. In the **Price list** field, select or search for **Contoso Coffee North America - USD**.

1. Change the **Revenue** field to **System Calculated**. This tells Dynamics 365 to compute the opportunity value automatically based on the products you add.

1. Select **+ Add products**.

1. In the product selection panel, change the Unit of **Espresso Machine - Pro** to **Year (lease)**.

1. Set the **Quantity** to 12.

1. Select **Add** and then select **Save to Opportunity**.

1. Review the **Extended amount** — it should show **$34,344.00**. Because you set up the Equipment Lease Volume Discount in Lab 04, Dynamics 365 automatically applies the **10% discount** for 12 units, so the discounted annual total appears immediately.

1. Select **+ Add products** again to add a second line item.

1. Set the following values on **Equipment Service Contract**:
    - **Unit**: Year (flat rate)
    - **Quantity**: 12
    - **Price per unit**: $1,068.00

1. Select **Add** and then select **Save to Opportunity**.

1. Scroll back up to the opportunity header and confirm the **Estimated Revenue** field has updated to reflect the total of your product lines **($47,160.00)**.

## Task 3: Add stakeholders and a competitor

The Northwind Traders deal isn't just Maya Torres's decision. Jordan discovered during a discovery call that the General Manager needs to sign off on any equipment contract over $5,000, and Facilities is involved in the installation logistics. Plus, they're currently talking to a competitor.

1. Return to the **Summary** tab on the Opportunity record. Scroll to the **Stakeholders** section.

1. Select the ellipsis and select **+ New Connection**.

1. In the contact search, select **+ New** to create a new contact.

1. Fill in the quick create form:
   - **First Name**: Robert
   - **Last Name**: Ngo
   - **Job Title**: General Manager
   - **Account Name**: Northwind Traders
   - **Email**: robert@northwindtraders.com

1. Select **Save and Close** and then select **Add**.

1. Add a third stakeholder using the same process:
    - **First Name**: Patricia
    - **Last Name**: Chen
    - **Job Title**: Facilities Manager
    - **Account Name**: Northwind Traders
    - **Email**: patricia@northwindtraders.com

   > [!NOTE]
   > If the stakeholders you created don't appear in the **Stakeholders** grid, select each contact in the **Lookup Records** pane and select **Add**. If necessary, select the ellipsis **(...)**, and then select **+ New Connection** to return to the **Lookup Records** pane.

1. Scroll to the **Competitors** section and select the ellipsis. Select **Add Existing Competitor** to log a competitor.

1. In the competitor search, type `Fourth Coffee` and select it from the results.

1. Select **Add**.

   > [!NOTE]
   > Tracking competitors isn't just for optics — it feeds Dynamics 365's win/loss analysis. When deals are closed, the competitor data helps Priya understand where Contoso Coffee is winning and losing at a product and competitor level.

## Task 4: Progress through the sales stages

The business process flow guides Jordan through the stages of Contoso's sales cycle. You'll advance the deal step by step.

1. In the **Business process flow** at the top of the form, select the **Qualify** stage (the first bubble) to review it.

1. Notice the fields that were captured when you qualified Maya Torres's lead in Lab 02. These are already complete. Select **(X)** to close it.

1. Select the **Develop** stage bubble. Fill in the following fields:
   - **Customer need**: Replace aging coffee equipment across all 12 restaurant locations with commercial-grade espresso machines to improve beverage quality and reduce maintenance downtime.
   - **Proposed Solution**: Annual lease of 12 Espresso Machine - Pro units with an annual service and maintenance contract covering all locations.
   - **Identify stakeholders**: Set to **completed**.
   - **Identify competitors**: Set to **completed**.

1. Select **Next Stage** to advance to the **Propose** stage. Select **(X)** to close it.

1. Log an activity to represent the proposal:
   - Scroll to the **Timeline** section
   - Select **+** > **Task**
   - **Subject**: Send formal proposal to Maya Torres and Robert Ngo
   - **Due Date**: Tomorrow's date
   - Select **Save and Close**

1. Select the **Propose** stage bubble and mark all four fields as **Completed**:
   - **Identify Sales Team**
   - **Develop Proposal**
   - **Complete Internal Review**
   - **Present Proposal**

1. Select **Next Stage** to advance to the **Close** stage.

   The deal is now in the Close stage. This is where Jordan will finalize negotiation and either win or lose.

## Task 5: Review the Copilot summary

As you've been adding products, stakeholders, and competitor data, Dynamics 365 Copilot has been building a summary of this opportunity. Before closing the deal, take a moment to see what it generated.

1. On the opportunity record, find the Copilot **Summary** section.

1. Expand the **Copilot** section if it isn't already open.

1. Review the three sections of the summary:
   - **Key info**: High-level opportunity details — account, estimated revenue, close date, and owner.
   - **Product insights**: A summary of the products on this deal, including the espresso machine lease and service contract.
   - **Competitor insights**: Notes about Fourth Coffee as a tracked competitor.

   > [!NOTE]
   > The Copilot summary updates as the opportunity data changes. Sales managers like Priya can use this to quickly get up to speed on a deal without reading through every note and activity in the timeline.

1. Select the **Copilot** button in the top navigation bar to open the Copilot chat pane.

1. In the Copilot pane, select the **sparkle** button to view prefilled prompts. Under **Get info**, select **Get latest news for account** prompt and submit it.

1. Review the news results for Northwind Traders. Copilot pulls recent news about the account directly into the pane, so Jordan can stay informed about what's happening at a customer's organization without leaving Dynamics 365.

   > [!NOTE]
   > Account news is powered by Bing and surfaces publicly available news about the company. It's a quick way for a sales rep to spot relevant context — a new executive hire, an acquisition, or an industry shift — before reaching out.

## Task 6: Close the opportunity as won

After two weeks of back-and-forth, Northwind Traders has signed the contract. Time to log the win.

1. On the opportunity record, select **Close as won** on the command bar.

1. In the **Opportunity Close** form, fill in:
   - **Actual Revenue**: $47,160.00
   - **Close Date**: Today's date
   - **Description**: Signed annual equipment lease for 12 Espresso Machine - Pro units with annual service contracts. General Manager Robert Ngo signed on 06/24/2026. Equipment installation across all 12 locations scheduled for August 2026.

1. Select **OK**.

   The opportunity status changes to **Won**. Dynamics 365 records the close date, the actual revenue, and the competitor involved — all of which feed into Contoso Coffee's pipeline analytics and win/loss reporting.

1. Return to the **Opportunities** list and confirm the Northwind Traders deal appears under the **Closed Opportunities** view with a **Won** status.

   > [!NOTE]
   > Closed opportunities aren't deleted — they're archived. Priya can run reports that compare estimated vs. actual revenue, measure time-to-close by territory, and analyze win rates by competitor.

You've managed a realistic enterprise opportunity from creation to close — with products, stakeholders, competitor tracking, and a structured sales process. Jordan Park now has a complete deal record, and Priya has the data she needs to analyze performance and forecast revenue. That's requirements five and six: complete.
