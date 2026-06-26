---
lab:
    title: 'Set up the product catalog'
    description: "Build Contoso Coffee's product catalog in Dynamics 365 Sales, including unit groups, products, price lists, and volume discount tiers."
    duration: '40 minutes'
    level: 200
    islab: true
---

# Set up the product catalog

Last month, a rep in the West region quoted a hotel chain $350 per month to lease a commercial espresso machine. Two weeks later, a rep in the Northeast quoted a different hotel chain $290 per month for the same model. When the first client found out, they were furious — and the West region rep had to go back and renegotiate.

Priya's response: "No more quoting from memory." Contoso Coffee needs a centralized product catalog where every product has a defined price and every rep quotes from the same source of truth.

In this lab, you'll build that catalog. You'll create unit groups, define Contoso Coffee's core products, build a standard price list, and set up a volume discount tier so that larger deals get the right pricing automatically.

This lab should take approximately **40** minutes to complete.

## Before you start

You need to be signed in to Sales Hub with the **App Settings** area accessible. You should also have admin or system customizer permissions in your environment.

## Task 1: Create a unit group

Dynamics 365 Sales uses unit groups to define how products are measured and sold. Contoso Coffee sells equipment as outright purchases and as monthly leases, and service contracts as flat-rate annual agreements. You'll create a unit group for equipment first.

1. In Sales Hub, select **App Settings** from the bottom of the left navigation.

1. Under the **Product catalog** section, select **Unit groups**.

1. Select **New** on the command bar.

1. Fill in the unit group details:
   - **Name**: `Equipment Units`
   - **Primary unit**: `Unit`

1. Select **OK** or **Save**.

1. On the **Equipment Units** record, select **Related** and then select **Units.**

1. Select **New Unit.**

1. Add the following unit:
   - **Name**: `Month (lease)`
   - **Quantity**: `1`
   - **Base unit**: Unit

1. Select **Save and close.**

1. Add another unit:
   - **Name**: `Year (lease)`
   - **Quantity**: `12`
   - **Base unit**: Month (Lease)

1. Select **Save and close**.

1. Return to the **Unit groups** list and select **New** again to create a second unit group for service contracts.

1. Fill in:
    - **Name**: `Service Units`
    - **Primary unit**: `Visit`

1. Select **OK** or **Save**.

1. On the **Service Units** record, select **Related** and **Units.** Add the following units:
    - **Name**: `Month (flat rate)` — Quantity: `1`, Base Unit: Visit
    - **Name**: `Year (flat rate)` — Quantity: `12`, Base Unit: Month (flat rate)

1. Select **Save and close**.

## Task 2: Create products

Now you'll add Contoso Coffee's four core offerings to the product catalog.

1. In **App Settings** > **Product catalog**, select **Families and products**.

1. Select **Add Product** on the command bar.

1. Fill in the first product:
   - **Name**: `Espresso Machine - Standard`
   - **Product ID**: `ESP-STD`
   - **Valid from**: Today's date
   - **Description**: `Commercial single-group espresso machine suitable for cafés, small restaurants, and hotel lobby bars serving up to 80 drinks per day.`
   - **Unit group**: `Equipment Units`
   - **Default unit**: `Unit`
   - **Decimals supported**: `0`

1. Select **Save**.

1. Confirm the **Status** shows **Active**. Products are saved as active immediately in this environment.

1. Select the back button to return to the Products, Families, and Bundles view. Repeat steps 2–5 to create three more products:

    **Product 2:**
    - **Name**: `Espresso Machine - Pro`
    - **Product ID**: `ESP-PRO`
    - **Valid from**: Today's date
    - **Description**: `Commercial dual-group espresso machine for high-volume environments such as hotel restaurants, corporate cafeterias, and conference centers serving up to 300 drinks per day.`
    - **Unit group**: `Equipment Units`
    - **Default unit**: `Unit`
    - **Decimals supported**: `0`

    **Product 3:**
    - **Name**: `Batch Brew Coffee Maker`
    - **Product ID**: `BREW-STD`
    - **Valid from**: Today's date
    - **Description**: `High-capacity batch brew coffee maker for offices, conference rooms, and break rooms. Brews up to 3 gallons per hour.`
    - **Unit group**: `Equipment Units`
    - **Default unit**: `Unit`
    - **Decimals supported**: `0`

    **Product 4:**
    - **Name**: `Equipment Service Contract`
    - **Product ID**: `SVC-CONTRACT`
    - **Valid from**: Today's date
    - **Description**: `Monthly service and maintenance contract covering two scheduled preventive maintenance visits per year and unlimited on-call repair support during business hours.`
    - **Unit group**: `Service Units`
    - **Default unit**: `Month (flat rate)`
    - **Decimals supported**: `0`

1. Return to the **Products, Families, and Bundles** list and confirm all four products show an **Active** status.

## Task 3: Create a price list

A price list connects your products to specific prices. Contoso Coffee has one standard price list for North American clients billed in USD. You'll build it now.

1. In **App Settings** > **Product catalog**, select **Price lists**.

1. Select **New** on the command bar.

1. Fill in the price list details:
   - **Name**: `Contoso Coffee North America - USD`
   - **Start date**: Today's date
   - **End date**: Leave blank (this is Contoso Coffee's permanent standard list)
   - **Currency**: `US Dollar`

1. Select **Save**.

1. On the price list record, select the **Price List Items** tab, then select **New Price List Item** on the command bar.

1. On the **General** tab, fill in:
   - **Product**: `Espresso Machine - Standard`
   - **Unit**: `Unit`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `3200.00`

1. Select **Save and close**, then select **+ New Price List Item**. On the **General** tab, fill in:
   - **Product**: `Espresso Machine - Standard`
   - **Unit**: `Month (lease)`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `145.00`

1. Select **Save and close**, then select **+ New Price List Item**. On the **General** tab, fill in:
   - **Product**: `Espresso Machine - Pro`
   - **Unit**: `Unit`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `5800.00`

1. Select **Save and close**, then select **+ New Price List Item**. On the **General** tab, fill in:
   - **Product**: `Espresso Machine - Pro`
   - **Unit**: `Year (lease)`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `3180.00`

1. Select **Save and close**, then select **+ New Price List Item**. On the **General** tab, fill in:
   - **Product**: `Batch Brew Coffee Maker`
   - **Unit**: `Unit`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `1400.00`

1. Select **Save and close**, then select **+ New Price List Item**. On the **General** tab, fill in:
   - **Product**: `Batch Brew Coffee Maker`
   - **Unit**: `Month (lease)`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `65.00`

1. Select **Save and close**, then select **+ New Price List Item**. On the **General** tab, fill in:
   - **Product**: `Equipment Service Contract`
   - **Unit**: `Year (flat rate)`

1. Select the **Pricing Information** tab and enter:
   - **Amount**: `1068.00`

1. Select **Save and close**.

1. Confirm that all seven price list items appear on the **Price List Items** tab of the **Contoso Coffee North America - USD** record.

## Task 4: Create a volume discount list

Contoso Coffee offers volume discounts on equipment leases when a customer leases five or more units. Five to nine units gets a 5% discount; ten or more units gets 10%.

1. In **App Settings** > **Product catalog**, select **Discount lists**.

1. Select **New** on the command bar.

1. Fill in:
   - **Name**: `Equipment Lease Volume Discounts`
   - **Type**: **Percentage**

1. Select **Save**.

1. Select **Related** and **Discounts.**

1. In the **Discounts** section, select **+ New discount**.

1. Add the first discount tier:
   - **Begin quantity**: `1`
   - **End quantity**: `4`
   - **Percentage**: `0`

1. Select **Save and close**, then select **New Discount**. Add:
   - **Begin quantity**: `5`
   - **End quantity**: `9`
   - **Percentage**: `5`

1. Select **Save and close**, then select **New Discount**. Add:
   - **Begin quantity**: `10`
   - **End quantity**: `9999`
   - **Percentage**: `10`

1. Select **Save**.

1. Select **Price lists** from the left menu.

1. Return to the **Contoso Coffee North America - USD** price list and select **Price list items.**

1. Find the **Espresso Machine - Standard (Month (lease))** price list item and open it. (To open it, select the pop-out at the very end of the view row - selecting the name of the Product opens the Product record, but we want to be on the Price List Item record.)

1. In the **Discount list** field, select `Equipment Lease Volume Discounts`.

1. Select **Save**.

1. Repeat steps 13–15 for the **Espresso Machine - Pro (Year (lease))** and **Batch Brew Coffee Maker (Month (lease))** price list items.

    Now when a rep adds leased equipment to an opportunity and the quantity reaches five or more units, the discount applies automatically.

## Task 5: Configure product catalog settings

Before reps start using the catalog, you'll make a few global settings to streamline the experience.

1. In **App Settings** > **Product catalog**, select **Product catalog settings**.

1. Configure the following settings:
   - **Create products in active state**: Toggle **On** — new products will be immediately available without needing to be manually published each time.
   - **Allow selection of default pricelist**: Toggle **On** — Dynamics 365 will automatically suggest the right price list based on the territory.
   - **Enhanced experience for adding products**: Toggle **On** — reps will see a grid where they can select and quantity multiple products at once, rather than adding them one at a time.
   - **Discount calculation method**: Set to **Line item** — the discount is applied to the total line amount after multiplying unit price × quantity.

1. Select **Save**.

## Summary

The product catalog you've created will be used in Lab 05 when you add products to an opportunity. 

If you'd like to review your work, go to **App Settings** > **Families and products** to see your four published products, and **Price lists** to see the **Contoso Coffee North America - USD** list with its discount tiers applied.

Contoso Coffee now has a centralized, consistent product catalog. Every rep who opens an opportunity and selects a product will see the same prices — and the system will automatically apply volume discounts when the deal qualifies. Requirement five: complete.
