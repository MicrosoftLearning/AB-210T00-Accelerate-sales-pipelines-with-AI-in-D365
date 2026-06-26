---
lab:
    title: 'Set up your lab environment'
    description: "Sign in to your Dynamics 365 Sales environment and meet the fictional company you'll work with throughout this course."
    duration: '15 minutes'
    level: 100
    islab: true
---

# Set up your lab environment

In this lab, you'll sign in to your Dynamics 365 Sales environment using the credentials provided by your authorized lab host, and you'll open the Sales Hub app where all the hands-on work takes place.

This lab also introduces **Contoso Coffee**, the fictional company you'll be helping throughout this course. Every lab builds on the same company story, so it's worth reading the background carefully before you dive in.

This lab should take approximately **15** minutes to complete.

## Meet Contoso Coffee

Founded in 2009 and headquartered in Seattle, Contoso Coffee is a mid-size commercial coffee equipment company with 175 employees and a 25-person sales team. They sell premium equipment and service contracts to businesses across the food service and hospitality industries, primarily:

- **Commercial espresso machines:** countertop and built-in models for cafés, restaurants, and hotels
- **Commercial coffee makers:** batch brew systems for offices, corporate cafeterias, and convention centers
- **Equipment leases:** 12-, 24-, and 36-month lease agreements for all equipment lines
- **Service and maintenance contracts:** preventive maintenance visits and on-call repair coverage

Their sales team is divided into four regional teams: **Northeast**, **Southeast**, **Central**, and **West**. Each region has a sales manager and between four and seven account executives.

Despite strong demand, Contoso is tracking at $8.5 million against a $12 million revenue target. Their VP of Sales, **Priya**, has commissioned a Dynamics 365 Sales implementation to fix that.

### What's going wrong

Priya identified nine critical problems with Contoso's current sales process:

1. **No system of record:** Deals live in personal spreadsheets and email threads. No manager has visibility into the full pipeline.
2. **Leads fall through the cracks:** Contoso attends six food service and hospitality trade shows per year and runs quarterly email campaigns, generating 200–300 leads each time. Without a defined lead lifecycle, most go cold.
3. **Manual prospect research:** Before a first call, reps spend an average of three hours researching a prospect — looking up restaurant group locations, hotel brand footprints, and office campus sizes — time that could be automated.
4. **Slow follow-up:** Prospects wait 24–48 hours for a reply. Competitors with faster response times are winning deals.
5. **Inconsistent pricing:** Reps quote lease and purchase prices from memory. A hotel chain in the West region was recently quoted a different monthly lease rate than a hotel chain in the Northeast for the same espresso machine model.
6. **Lost deals, unknown reasons:** Deals involving multiple stakeholders — a facilities manager, a procurement lead, and a general manager — frequently go quiet with no record of why the deal was lost.
7. **No pipeline visibility:** Priya can't answer "How much will we close this quarter?" without asking every rep to update a spreadsheet manually.
8. **Missed renewals and upsells:** Customers on 36-month equipment leases aren't being contacted before their leases expire. Reps only find out a lease is ending when the customer calls to arrange equipment return.
9. **Disconnected tools:** Reps use separate email clients, file-sharing platforms, and manual tracking methods. Nothing is connected.

### The requirements

Priya gave you, the Dynamics 365 functional consultant, a list of eight things the new system must do:

| # | Requirement | Addressed in |
|---|-------------|-------------|
| 1 | Configure the system with Contoso's four sales regions and appropriate security roles | Lab 01 |
| 2 | Standardize the lead lifecycle — import, assign, qualify, and convert leads consistently | Lab 02 |
| 3 | Use AI to research and score leads so reps focus on the best opportunities first | Lab 03 |
| 4 | Build a product catalog with all offerings, unit pricing, and discount tiers | Lab 04 |
| 5 | Track opportunities end-to-end with stakeholder mapping and competitor tracking | Lab 05 |
| 6 | Deploy AI agents to monitor pipeline health and automate customer follow-up | Lab 06 |
| 7 | Integrate with productivity and collaboration tools for email, calendar, and document management | (covered in module content) |
| 8 | Extend with Power Automate workflows and Power BI dashboards | Lab 07 |

In these labs, you're playing the role of the Dynamics 365 functional consultant who was brought in to turn these requirements into solutions. Each lab solves one of Contoso Coffee's problems. By the time you finish Lab 07, Contoso will have a working system, and you'll have the hands-on skills to back it up.

## Task 1: Sign up for a Dynamics 365 Sales trial

Use the credentials provided by your authorized lab host to sign up for a Dynamics 365 Sales trial.

1. Open a browser and go to `https://www.microsoft.com/en-us/dynamics-365/free-trial`.

1. Find the **Sales** section, and select **Try for free**.

1. Enter the **Username** provided by your lab host, and then select **Next**.

1. Enter the **Password** provided by your lab host, and then select **Sign in**.

1. On the confirmation page, verify your country or region and phone number, and then select **Get started**.

1. If you're prompted to stay signed in, select **Yes**.

1. Wait for the trial environment to finish setting up. This may take a few minutes.

    When setup is complete, you're taken to your Sales trial environment. In the next task, you'll open the Sales Hub app.

## Task 2: Open the Dynamics 365 Sales Hub app

1. At the top of the screen, select **Sales trial** to open the app selector.

1. In the app selector, select **Sales Hub**.

1. Take a moment to explore the left navigation. You'll see sections for **Leads**, **Opportunities**, **Accounts**, **Contacts**, and more. The **App Settings** area (accessible from the bottom of the navigation or via the gear icon) is where you'll do most of the configuration work.

1. Confirm that you can see the **Sales Hub** title in the top-left corner of the screen. If you can, your environment is ready.

    > **Note**: Your environment may look slightly different depending on the Dynamics 365 Sales version and any settings already configured by your lab host. This is normal.

You've successfully signed in and opened your Dynamics 365 Sales environment. You're ready to start building Contoso Coffee's sales system, beginning with Lab 01.
