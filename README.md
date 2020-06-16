# shopify-orders
Deluge script for configuring a Shopify Orders integration with Zoho CRM.

# Configuration

##  Zoho CRM Modules
You will need two custom modules for this integration: Shopify Orders and Shopify Order Line Items
### Shopify Orders
| Field                | Type                 |
|----------------------|----------------------|
| Shopify Order Name*  | Single Line          |
| Shopify Order Owner* | Single Line          |
| Order Date           | Date                 |
| Status URL           | URL                  |
| Order Number         | Single Line (Unique) |
| Line Items           | Multi-Line           |
| Contact              | Lookup               |
| First Name           | Single Line          |
| Last Name            | Single Line          |
| Email*               | Email                |
| Phone                | Phone                |
| Discount             | Currency             |
| Subtotal             | Currency             |
| Tax                  | Currency             |
| Total                | Currency             |
| Currency*            | Picklist             |
| Address Line 1       | Single Line          |
| Address Line 2       | Single Line          |
| City                 | Single Line          |
| State                | Single Line          |
| Country              | Single Line          |
| Postal Code          | Single Line          |

### Shopify Line Items
| Field                | Type                 |
|----------------------|----------------------|
| Shopify Order Name*  | Single Line          |
| Shopify Order Owner* | Single Line          |
| Order Date           | Date                 |
| Status URL           | URL                  |
| Order Number         | Single Line (Unique) |
| Line Items           | Multi-Line           |
| Contact              | Lookup               |
| First Name           | Single Line          |
| Last Name            | Single Line          |
| Email*               | Email                |
| Phone                | Phone                |
| Discount             | Currency             |
| Subtotal             | Currency             |
| Tax                  | Currency             |
| Total                | Currency             |
| Currency*            | Picklist             |
| Address Line 1       | Single Line          |
| Address Line 2       | Single Line          |
| City                 | Single Line          |
| State                | Single Line          |
| Country              | Single Line          |
| Postal Code          | Single Line          |

## Zapier Setup
To configure Zapier, you must have an account with access to the Shopify and Zoho CRM apps. 

Create a new Zap and perform the following setup:

### Shopify

#### Choose App & Event
* Search and find **Shopify** and select it.
* Select the **New Order** event.
    * Click *Continue*

#### Choose Account
* Pick the correct account, or create a new one.
    * Click *Continue*

#### Find Data
* Click **Test Trigger** to get test results.
    * Click *Continue*


### Formatter
#### Choose App & Event
* Search and find **Formatter by Zapier** and select it.
* Select the **Utilities** event.
    * Click *Continue*

#### Customize Utilities
* Under *Transform* select **Line-item to Text**.
* In the *Input*, type and insert the following **exactly** how it is shown below (items in square brackets are Zapier fields):
    * `Item:[1. Line Items Name]??Quantity:[1. Line Items Quantity]??SKU:[1. Line Items Sku]??Price:[1. Line Items Price]`
* In the *Separator* field insert: `&&`
* Click *Continue*
* Click *Test & Continue*

### Zoho CRM
#### Choose App & Event
* Search and find **Zoho CRM** and select it.
* Select the **Create/Update Module Entry** event.
    * Click *Continue*

#### Choose Account
* Pick the correct account, or create a new one.
    * Click *Continue*

#### Customize Module Entry
* Map the corresponding fields in Zapier to Zoho CRM fields:
    * Module → Shopify Orders
    * Layout → Standard
    * Trigger → Workflow
    * Duplicate Check Fields → Order Number
    * CustomModule Name → [1. Name] for [1. Billing Address First Name] [1. Billing Address Last Name]
    * Order Date → {{zap_meta_human_now}}
    * Status URL → [1. Order Status URL]
    * Order Number → [1. Order Number]
    * Line Items → [2. Output Text]
    * First Name → [1. Billing Address First Name]
    * Last Name → [1. Billing Address Last Name]
    * Email → [1. Email]
    * Phone → [1. Billing Address Phone]
    * Discount → [1. Total Discounts]
    * Subtotal → [1. Subtotal Price]
    * Tax → [1. Total Tax]
    * Total → [1. Total Price]
    * Currency → [1. Presentment Currency]
    * Address Line 1 → [1. Billing Address Address1]
    * Adress Line 2 → [1. Billing Address Address2]
    * City → [1. Billing Address City]
    * State → [1. Billing Address Province]
    * Country → [1. Billing Address Country]
    * Postal Code → [1. Billing Address Zip]

* Click *Continue*
* Click *Test & Continue*. This will create a new module entry.

* When satisfied with the results, turn on your Zap.

## CRM Workflow
Triggers on new or updated Shopify Order.

# Tutorial
This function parses the Line Item string text sent from Shopify to create new Shopify Line Item records.
