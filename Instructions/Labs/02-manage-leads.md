---
lab:
    title: 'Lab 2 - Manage leads in Dynamics 365 Sales'
    description: "Create and import leads, review them with Copilot, and qualify a lead to create an opportunity — using data from Contoso Coffee's most recent trade show."
    duration: '35 minutes'
    level: 200
    islab: true
---

# Lab 2 - Manage leads in Dynamics 365 Sales

Contoso Coffee just returned from **FoodService Summit Denver**, a three-day food service and hospitality industry trade show. Their booth team collected 47 business cards and badge scans from prospects interested in upgrading their commercial coffee and espresso equipment. Those contacts are currently sitting in a spreadsheet on the event manager's laptop — not in Dynamics 365, not assigned to any rep, and not being followed up on.

This is exactly the scenario Priya described when she said "leads fall through the cracks." In this lab, you'll fix that. You'll create leads manually, import a batch of leads from a CSV file, review them with Copilot, and qualify the most promising one to create an opportunity.

This lab should take approximately **35** minutes to complete.

## Before you start

You need to be signed in to Sales Hub. If you haven't completed Lab 01, make sure you have at least signed in to your environment (Lab 00).

## Task 1: Create a lead manually

After a rep named **Jordan Park** left the conference floor, they typed a quick note about a conversation they had with a prospect named Maya Torres from Northwind Traders. You'll capture that as a lead.

1. In **Sales Hub**, select **Leads** in the left navigation.

1. Select **+ New** on the command bar.

1. Fill in the following fields on the main form:
   - **Topic**: Commercial espresso machine lease - 12 locations
   - **First Name**: Maya
   - **Last Name**: Torres
   - **Job Title**: Director of Operations
   - **Business Phone**: +1 (972) 555-0143
   - **Company**: Northwind Traders
   - **Email**: maya@northwindtraders.com

1. In the record header above the Business process flow bar, select the **chevron (˅)** next to the **Owner** field to expand the header details. Then set:
   - **Lead Source**: Trade Show
   - **Rating**: Hot

1. Select the **Details** tab and fill in:
   - **Description**: Met at FoodService Summit Denver. Northwind Traders is upgrading their coffee program across all 12 restaurant locations. Decision expected within 60 days. Budget is approved. Wants a site visit next week.
   - **Industry**: Eating and Drinking Places
   - **Annual Revenue**: 85000000
   - **No. of Employees**: 450

1. Select **Save** on the command bar. If you receive the duplicate record warning, select **Ignore and save**.

    Dynamics 365 creates the lead record. Notice the **Business process flow** bar at the top showing the lead in the **Qualify** stage.

1. Select **Qualify** to immediately open the lead qualification dialog, but don't complete it yet. You'll qualify this lead in Task 4 after working with the import.

## Task 2: Import leads from a CSV file

Jordan collected 47 cards at the conference, but you'll work with a small representative sample. You'll import five leads at once using Dynamics 365's CSV import feature.

### Prepare the import file

1. Open a plain text editor (such as Notepad) on your computer.

1. Copy and paste the following content exactly as shown:

    ```
    First Name,Last Name,Job Title,Company Name,Email,Business Phone,Lead Source,Rating,Industry,Number of Employees,Topic
    Daniel,Nguyen,VP of Operations,Litware Inc.,daniel@litwareinc.com,+1 (216) 555-0198,Trade Show,Hot,Hotels and Motels,1200,Commercial espresso machine lease - 18 hotel properties
    Aisha,Patel,Facilities Manager,Coho Winery,aisha@cohowinery.com,+1 (206) 555-0112,Trade Show,Warm,Eating and Drinking Places,85,Commercial coffee maker - tasting room and restaurant
    Marcus,Webb,General Manager,Relecloud,marcus@relecloud.com,+1 (512) 555-0177,Trade Show,Warm,Hotels and Motels,320,Espresso machine upgrade - lobby café and restaurant
    Sofia,Mendez,Director of Operations,VanArsdel Ltd.,sofia@vanarsdelltd.com,+1 (617) 555-0165,Trade Show,Cold,Eating and Drinking Places,2400,Service and maintenance contract renewal - 8 locations
    Ben,Andrews,Facilities Director,Tailspin Toys,ben@tailspintoys.com,+1 (303) 555-0133,Trade Show,Hot,Durable Manufacturing,680,Corporate campus espresso machine lease - 3 locations
    ```

1. Save the file as `foodservice-summit-leads.csv` in a location you can easily find (such as your Desktop). In the **Save As** dialog, set **Save as type** to **All Files** — otherwise Notepad adds a `.txt` extension and the import will fail.

### Import the file

1. Select the **Settings** gear icon in the top navigation bar, then select **Advanced settings**.

1. In the **System** section, select **Data Management**, then select **Imports**.

1. Select **+ Import data** on the command bar.

1. In the import wizard, select **Choose file** and browse to the `foodservice-summit-leads.csv` file you saved. Select **Next**.

1. On the **Review file upload summary** page, confirm the defaults are set as follows, then select **Next**:
   - **Data delimiter**: Quotation mark (")
   - **Field delimiter**: Comma (,)
   - **First row contains column headings**: checked
   - **Allow duplicates**: off

1. On the **Map record types** page, leave **Data map templates** set to **Default (Automatic mapping)**. In the **Entity mapping** dropdown, select **Lead**, then select **Next**.

1. On the **Map fields** page, confirm the following mappings, then select **Next**:
   - **Last Name**: Last Name
   - **Topic**: Topic
   - **Business Phone**: Business Phone
   - **Company Name**: Company Name
   - **Email**: Email
   - **First Name**: First Name
   - **Industry**: Industry (Option set — leave all option mappings as default)
   - **Lead Source**: Lead Source (Option set — leave all option mappings as default)
   - **Number of Employees**: No. of Employees
   - **Rating**: Rating (Option set — leave all option mappings as default)

1. Select **Next**.

1. Select **Finish**.

1. You're still in Advanced Settings. Wait on the Imports page and select the **Refresh** button on the command bar after about 30 seconds. When the import finishes, check the **Successes** and **Errors** columns.

  > [!NOTE]
  > If you see any errors, check the **Errors** column for details. The duplicate detection rule you configured in Lab 01 will block any leads whose company name matches an existing record in your environment.

1. Return to Sales Hub by selecting the app switcher or navigating back to your Sales Hub URL.

1. In Sales Hub, select **Leads** in the left navigation.

1. On the command bar, select **Read-only grid** to switch to the grid view.

1. Search for one of the names from your CSV file (such as `Ben Andrews`) to confirm the imported leads appear in the list.

  > [!NOTE]
  > If the leads don't appear immediately, wait another 30 seconds and refresh again.

## Task 3: Review leads and use Copilot insights

Now that the leads are in the system, you'll use Copilot to review one of the hot leads before deciding whether to qualify it.

1. Select **Ben Andrews** from the leads list to open his record.

1. At the top of the lead form, locate the Copilot **Summary** section. Read the summary generated for Ben's lead — it should highlight key details such as his role, company size, topic, and lead source.

1. On Ben's lead record, scroll to the **Timeline** section. Select **+** and choose **Phone Call** to log a planned call.

1. In the Quick Create form:
   - **Subject**: Discovery call - equipment consultation
   - **Direction**: Outgoing
   - **Description**: Follow up from FoodService Summit Denver. Confirm equipment needs and site count.
   - **Duration**: 30 minutes

1. Select **Save and close**.

   The call activity now appears in Ben's timeline, making it visible to anyone on Jordan's team who might cover for them.

## Task 4: Qualify a lead

Maya Torres is a hot lead with a confirmed budget and an accelerated timeline. It's time to qualify her and create an opportunity.

1. Select the **back** button to return to the Leads view. Remove any filters.

1. Select **Maya Torres** from the leads list to open her record.

1. Review the lead details to make sure they're complete. Then select **Qualify** on the business process flow.

1. In the **Qualify Lead** dialog, fill in the following fields:
   - **Existing Account?**: Select **Northwind Traders** — they should already be an account in the system, so you can look up the record.
   - **Existing Contact?**: Select **+ New**. In the Quick Create form, Maya's information populates. Select **Save and Close**.
   - **Purchase timeframe**: This quarter
   - **Estimated budget**: 150000

1. Select **Qualify** from the command bar.

    Dynamics 365 links three records automatically: the Account for Northwind Traders, a Contact for Maya Torres, and an Opportunity pre-populated with the lead's details. The lead itself is marked as **Qualified** and closed.

1. You'll be redirected to the new **Opportunity** record. Confirm that the opportunity information shows:
   - **Topic**: Commercial espresso machine lease - 12 locations
   - **Account**: Northwind Traders (this is in the header, next to the **Owner** field)

    You'll work with this opportunity more in Lab 05.

You've successfully created a lead manually, imported a batch of leads from a trade show, used Copilot to review a lead, and qualified the hottest lead into an opportunity. Priya's second requirement — a standardized lead lifecycle — is in place.
