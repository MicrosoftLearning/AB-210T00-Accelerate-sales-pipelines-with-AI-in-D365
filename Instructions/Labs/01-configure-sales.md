---
lab:
    title: 'Lab 1 - Configure Dynamics 365 Sales'
    description: 'Set up the foundational configuration for Contoso Coffee, including creating sales team users, sales territories, auto-numbering, and Copilot summarization.'
    duration: '50 minutes'
    level: 200
    islab: true
---

# Lab 1 - Configure Dynamics 365 Sales

Contoso Coffee has a brand-new Dynamics 365 Sales environment, and right now, it's a blank slate. Before any seller can open a lead or close a deal, the system needs to reflect how Contoso actually operates: four regional teams, consistent record numbering, and AI-powered summaries that save reps time on every record they open.

In this lab, you'll configure those foundations. You'll create user accounts for Contoso Coffee's sales team and assign security roles, set up Contoso Coffee's four sales territories, define auto-numbering prefixes that match Contoso's naming conventions, and configure Copilot to summarize leads and opportunities the way Contoso's sellers need.

This lab should take approximately **50** minutes to complete.

## Before you start

You need to be signed in to your Dynamics 365 Sales environment and have the **Sales Hub** app open. If you haven't completed Lab 00, do that first.

This lab also uses two admin portals. Open each in a separate browser tab before you begin:

- **Microsoft 365 admin center** (`https://admin.cloud.microsoft/`) — for creating users and assigning licenses
- **Power Platform admin center** (`https://admin.powerplatform.microsoft.com`) — for environment settings and data management

Sign in to both with the same credentials you used in Lab 00.

## Task 1: Create Contoso Coffee's sales team users

Before configuring territories, you need user accounts for Contoso Coffee's regional sales managers and sales representative. You'll create five users in the Microsoft 365 admin center, assign them Dynamics 365 Sales licenses, and then assign them security roles in Dynamics 365 Sales.

1. Open a new browser tab (if you haven't already) and go to `https://admin.cloud.microsoft/`.

1. In the left navigation, select **Users**, then select **Active users**.

1. Select **Add a user** on the command bar.

1. On the **Set up the basics** page, enter the following details:
   - **First name**: `Andy`
   - **Last name**: `Kim`
   - **Display name**: `Andy Kim`
   - **Username**: `andykim`

1. Leave the following options at their defaults:
   - **Automatically create a password** — checked. The admin center generates a temporary password for the new user.
   - **Require this user to change their password when they first sign in** — checked. The user must set their own password on first sign-in.

   > [!NOTE]
   > In a production environment, you might uncheck automatic password creation to set a password yourself, or share the generated password securely with the new user.

1. Select **Next**.

1. On the **Assign product licenses** page, under **Select location**, select your location, then select the **Dynamics 365 Sales Premium Viral Trial** checkbox to assign the license.

1. Select **Next**, select **Next** again to skip optional settings, select **Finish adding**, and then select **Close**.

1. Repeat steps 3–8 to create the following four users, assigning each the **Dynamics 365 Sales** license:

   | First name | Last name | Display name | Username|
   |------------|-----------|-------------|-------------|
   | Maria | Reyes | Maria Reyes | mariareyes |
   | David | Osei | David Osei | davidosei |
   | Rachel | Sato | Rachel Sato | rachelsato |
   | Jordan | Park | Jordan Park | jordanpark |

1. Confirm that all five users appear in the **Active users** list.

## Task 2: Assign security roles in Dynamics 365 Sales

Next, assign security roles to define the privileges and access levels that these new users receive. You'll do this in the **Power Platform admin center**, which is where administrators manage environment-level settings including user access. You'll use two out-of-the-box security roles: **Salesperson** for Jordan Park and **Sales Manager** for the four regional managers.

1. Open a new browser tab and go to `https://admin.powerplatform.microsoft.com`.

1. In the left navigation, select **Manage**, then select **Environments**.

1. Select your Dynamics 365 **Sales Trial** environment from the list.

1. Select **Settings** on the command bar.

1. Expand the **Users + permissions** section and select **Users**.

1. Select **+ Add user** on the command bar.

1. In the search box, type `Andy Kim`, then select the user from the results.

   > [!NOTE]
   > Newly created users may take a few minutes to sync from Microsoft 365 to Dynamics 365. If you don't see a user yet, wait a moment and refresh the page.

1. Select **Add**.

1. In the **Manage security roles** pane, select the **Sales Manager** security role.

1. Select **Save** and **Save** again to confirm the role assignment.

1. Repeat steps 6–10 to add **Maria Reyes**, **David Osei**, and **Rachel Sato**, assigning each the **Sales Manager** role.

1. Repeat steps 6–10 to add **Jordan Park**, assigning the **Salesperson** role.

You now have a realistic set of Contoso users ready to assign throughout the labs.

## Task 3: Create sales territories

Contoso's sales team is organized into four regions. You'll create a territory for each one in Dynamics 365 Sales.

1. Go to the **Sales Hub** and select **App Settings** from the bottom of the left navigation.

1. In the **App Settings** area, select **Show all settings** and expand the **Sales Administration** section, then select **Sales territories**.

1. Select **+ New** on the command bar to create the first territory.

1. In the **Territory Name** field, enter `Northeast`.

1. In the **Manager** field, search for and select **Andy Kim**.

1. Select **Save & close** on the command bar.

1. Repeat steps 3–6 to create three more territories, assigning the manager shown:

   | Territory | Manager |
   |-----------|---------|
   | Southeast | Maria Reyes |
   | Central | David Osei |
   | West | Rachel Sato |

1. Confirm that all four territories appear in the list: **Northeast**, **Southeast**, **Central**, and **West**.

    Contoso's regional structure is now reflected in the system. Sellers and managers will be able to filter pipeline views, reports, and forecasts by territory.

## Task 4: Configure auto-numbering prefixes

Contoso wants all records to have consistent, recognizable identifiers so that quotes and orders are easy to trace across systems. You'll update the auto-numbering prefixes for two record types: Quotes and Orders.

1. Open a new browser tab and go to `https://admin.powerplatform.microsoft.com`.

1. In the left navigation, select **Manage** and then select **Environments**.

1. Select your Dynamics 365 **Sales Trial** environment from the list.

1. Select **Settings** on the command bar.

1. Expand the **Data management** section, then select **Auto-numbering**.

1. In the auto-numbering settings, find the **Quotes** row.

1. Change the **Prefix** value to **CCQ** (Contoso Coffee Quote).

1. Confirm the **Suffix length** is set to **6**.

1. Find the **Orders** row and change the **Prefix** to **CCO** (Contoso Coffee Order).

1. Select **Save** to apply the changes.

  > [!NOTE]
  > Auto-numbering changes apply to new records only. Existing records keep their original numbers.

<!--
## Task 5: Set up duplicate detection for leads

Contoso generates leads from multiple sources, like trade shows, web forms, email campaigns. Without duplicate detection, the same contact could end up as multiple lead records, wasting a rep's time and creating conflicting data.

In this task, you'll create a rule that flags two leads as potential duplicates when they share the same first five characters of the **Company Name** field. This catches common variations — like "Northwind Traders" and "Northwind Trading Co." — before they create conflicting records in the pipeline.

1. Return to the **Power Platform admin center** tab.

1. In the environment settings, expand the **Data management** section and select **Duplicate detection rules**.

1. Select **+ New** on the command bar.

1. Fill in the rule details:
   - **Name**: `Duplicate leads by company name`
   - **Description**: `Flags leads as potential duplicates when they share the same first five characters of the Company Name field.`
   - **Base record type**: **Lead**
   - **Matching record type**: **Lead**

1. In the criteria section, select **+ Add** to add a matching field.

1. From the **Field** dropdown, select **Company Name**.

    > [!NOTE]
    > You may notice an **Account** field on lead records as well. Account is a lookup that links to an existing Account record, but most inbound leads arrive before any Account exists, so that field is usually empty. **Company Name** is the plain-text field where the company name is captured at the point of entry, making it the right choice for catching duplicates from web forms, trade show scans, and CSV imports.

1. Set **Criteria** to **Same first characters**, and set the **Number of characters** to `5`.

1. Select **Save and close**.

1. On the rules list, find your new rule and select **Publish** to activate it. Select **OK** to confirm.

    > [!NOTE]
    > Duplicate detection rules only run when a user saves a record or during data imports. They don't retroactively flag existing records.
-->

## Task 6: Configure Copilot record summarization

One of the biggest time-savers in Dynamics 365 Sales is Copilot's ability to summarize a record when a seller opens it. Instead of scanning through every field and note, a rep gets a concise AI-generated snapshot. You'll configure what goes into those summaries for leads and opportunities.

1. Return to the **Sales Hub** browser tab.

1. Select **App Settings** from the bottom of the left navigation.

1. Under **General settings**, select **Copilot**.

1. Select the **Setup** tab.

1. Under **All apps**, confirm the dropdown list is set to **On**. If it's set to **Custom**, change it to **On**.

   > [!NOTE]
   > The default value may vary by environment. Setting it to **On** enables Copilot features across all apps in the environment.

1. Select **Save**.

1. Select the **Leads** tab.

1. Review the default fields included in the lead summary. You should see fields like **Topic** and **Lead Source**.

1. Select **+ Add fields** and add the following fields to the summary:
   - **Company Name**
   - **Annual Revenue**
   - **No. of Employees**
   - **Rating**

    These fields help a rep quickly assess the size and potential of a lead without opening every tab.

1. Select **Save**.

1. Select the **Opportunities** tab.

1. Review the default opportunity summary fields. You should see fields like **Customer Need**, **Proposed Solution**, **Customer Pain Points**, **Current Situation**, **Originating Lead**, and **Description**.

1. Select **+ Add fields** and add **Budget Amount**.

1. Select the **Show opportunity summary as a widget in the form** checkbox to enable the summary as an inline widget on the opportunity form.

1. Select **Save**.

  > [!NOTE]
  > Changes to Copilot summarization take effect immediately for new sessions. Sellers who are already signed in may need to refresh their browser.

## Task 7: Verify your configuration

Before moving on, confirm that Copilot summarization is working as expected. You'll create a test lead to check the Copilot summary.

1. At the bottom of the left navigation, select **App Settings**, then select **Sales** to return to the main Sales Hub area.

1. In the left navigation, select **Leads**.

1. Select **+ New** on the command bar.

1. Fill in the following details for the first test lead:
   - **Topic**: Test Lead - Verify Config
   - **First Name**: Alex
   - **Last Name**: Rivera
   - **Company**: Northwind Trading

1. Select the **Details** tab on the lead record.

1. Enter the following values:
   - **Annual Revenue**: 500000
   - **No. of Employees**: 50

1. Select **Save** on the command bar.

1. On the saved lead record, select the record summary above Alex's name.

1. Confirm that the record summary includes **Company Name**, **Annual Revenue**, and **Number of Employees** (the fields you added in Task 6).

## Summary

You've created five user accounts, four territories, auto-numbering prefixes, and Copilot summarization configured for leads and opportunities. To review what you created, go to the **Microsoft 365 admin center** > **Active users** to see the Contoso Coffee team, and go to **App Settings** > **Sales territories** to see the four regions.

You're now done with Lab 01. Contoso Coffee's environment has a team of named users with appropriate security roles, a regional structure, consistent record numbering, and Copilot configured to help sellers work faster.
