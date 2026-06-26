---
lab:
    title: 'Build a sales dashboard'
    description: 'Create a personal sales dashboard in Dynamics 365 Sales so Contoso leadership can track pipeline health, revenue, and deal activity in real time — no spreadsheet required.'
    duration: '25 minutes'
    level: 200
    islab: true
---

# Build a sales dashboard

Every Monday at 9 AM, Priya chairs the weekly pipeline review. Until now, someone on Marcus Webb's sales ops team has spent Sunday evening pulling data from individual rep spreadsheets, copying numbers into a shared deck, and praying nothing changed overnight.

Last week, a rep forgot to update their spreadsheet. The number Priya quoted to the VP of Sales was wrong by $400,000.

Dynamics 365 Sales has had all of this data all along — it just wasn't surfaced anywhere visible. In this lab, you'll build a personal sales dashboard for Priya that shows the live pipeline at a glance: deals by stage, revenue by territory, and activity this week. The moment a rep updates an opportunity, the dashboard reflects it.

No more Sunday spreadsheets.

This lab should take approximately **25** minutes to complete.

## Before you start

You need to be signed in to Sales Hub. The dashboard you build will be most useful if you've completed Labs 01–06, since those labs created the leads, opportunities, and products that will appear in your charts. If you're starting fresh, the dashboard will still work; it'll just show less data.

## Task 1: Explore the default system dashboards

Before building a custom dashboard, take a look at what Dynamics 365 Sales includes out of the box.

1. In Sales Hub, select **Dashboards** in the left navigation.

1. In the dashboard view, select the **Dashboard** dropdown at the top of the page to see the list of available system dashboards.

1. Select **Sales Activity Social Dashboard** and review what's displayed. Notice that it shows recent activities, leads, and opportunities in a social-style feed.

1. Select the dropdown again and choose **Sales Performance Dashboard**. This view shows charts focused on opportunity pipeline, win rates, and revenue.

1. Take a moment to explore the charts. Select one of the chart segments (for example, a pipeline stage in the funnel chart) to see how Dynamics 365 filters the underlying records when you interact with a dashboard.

    > **Note**: System dashboards are shared across your organization and can't be edited by individual users. In the next task, you'll create your own personal dashboard that you can fully customize.

## Task 2: Create a personal dashboard

1. On the **Dashboards** page, select **New** on the command bar and choose **Dynamics 365 Dashboard** from the dropdown. 

1. In the layout picker, select the **2-Column Regular Dashboard** layout, then select **Create**.

1. A blank dashboard canvas opens with a 2-column, 3-row layout. At the top, replace the default name by selecting the title field and entering: `Contoso Weekly Pipeline - Priya`.

1. You'll now add components to fill the dashboard. Start by selecting the **Insert Chart** icon in the first tile (upper-left).

1. In the **Add Component** dialog:
   - **Row Type**: **Opportunity**
   - **View**: **Open Opportunities**
   - **Chart**: **Top Opportunities**

1. Select **Add**.

    This bar chart shows the highest-value open opportunities at a glance — exactly what Priya needs to open the Monday meeting.

## Task 3: Add more charts and lists

1. Select the **Insert Chart** icon in the next tile (upper-right).

1. Add a second chart:
   - **Row Type**: **Opportunity**
   - **View**: **Open Opportunities**
   - **Chart**: **Sales Pipeline**

1. Select **Add**.

1. In the middle-left tile, select **Insert Chart** again and add:
   - **Row Type**: **Lead**
   - **View**: **All Leads**
   - **Chart**: **Leads by Source**

1. Select **Add**.

    This chart shows which lead sources — trade shows, web forms, email campaigns — are generating the most leads for Contoso Coffee. Priya can use this to justify budget for next year's FoodService Summit booth.

1. In the middle-right tile, select **Insert List** (the list icon, rather than the chart icon).

1. Configure the list:
   - **Row Type**: **Opportunities**
   - **View**: **Opportunities Closing Next Month**

1. Select **Add**.

    This list gives Priya a live view of every deal that should close before the end of the next month — sorted by close date.


1. Select **Save** on the command bar to save the dashboard.

1. Select **Close** to exit edit mode.

    Your dashboard now displays live data from Dynamics 365 Sales. Every chart and list updates automatically as reps add leads, move opportunities through stages, and log activities.

## Task 4: Set the dashboard as your default

1. On the dashboard page, confirm your **Contoso Weekly Pipeline - Priya** dashboard is displayed.

1. Select **Set as Default** on the command bar.

    Now every time Priya signs in to Sales Hub, this dashboard is the first thing she sees. The Monday pipeline review just got a lot less stressful.

## Task 5: Interact with the dashboard

Dashboards in Dynamics 365 Sales aren't static — they're interactive. Selecting a chart segment filters the entire dashboard to show only the related records.

1. On your dashboard, navigate to the **Top opportunities** chart.

1. Select **View records** in the upper right corner of the chart.

1. You'll now see a new dashboard that drills deeper into your Top opportunities, including a pipeline view and a list of the opportunity records.

    This interactivity means Priya can use the dashboard not just to monitor the business, but to quickly investigate a question — "Which deals are closest to closing?" — without navigating away to a separate view.

Priya now has a live, interactive view of Contoso Coffee's sales pipeline — and Marcus's team gets their Sunday evenings back. This dashboard directly addresses requirement seven from Lab 00: giving leadership real-time pipeline visibility without relying on anyone to update a spreadsheet.
