# Welcome 2

Create forms can be auto-filled with certain values by constructing an Auto-fill URL. You can then add this in to your app as a button to allow your users to create new records with some fields already filled in for them.&#x20;

new para

**Note: Auto-fill only works on create forms.**&#x20;

## How to construct your autofill URL <a href="#h_01h9recbw93fxdxpqq3189vqme" id="h_01h9recbw93fxdxpqq3189vqme"></a>

Where and how you do this is dependent on what the intended function of the URL will be...

If you want to autofill your create form with a static field e.g. a fixed Type or Status and you want the button for this to be within each detail record view, you can add in a button by dragging a new 'Banner' container in and then adding in your Auto-fill URL directly into the box.

However if you want to autofill your create form with a variable field i.e. something dependent on the current record you are in, using linked records etc, or you want to display your button on a list view -you need to add in your autofill URL as a new field in Airtable.

## Basic Link Structure <a href="#h_01h9recbw9g53w4ep7x079b8ge" id="h_01h9recbw9g53w4ep7x079b8ge"></a>

Auto-fill links must be in the following format:

![Autofill.png](https://support.stackerhq.com/hc/article_attachments/11330614149267)

> We recommend using a relative link format i.e. not containing the start of your app URL (e.g. testapp-1.my.stacker.app) just in case you decide to change it or use a custom domain, then you won't need to update this URL too.&#x20;

* where _**workspacename/page/new**_ - is the extension of the URL for the create form of the page you want to add a new record to. For example in one app where we would like to autofill values in the create form for the 'Members' page, the URL extension can be seen as /members/new
* _**field**_ is the developer name of the field to be filled

&#x20;

Auto-fill multiple fields by adding the **&** separator in the url that you create.&#x20;

For example:

![autofillplus.png](https://support.stackerhq.com/hc/article_attachments/11330753933331)

To find the developer names, go to  **Manage fields and data** > **\[Table name]** > **Fields** and toggle on **Show developer name**. The developer name appears underneath the user-facing name for each field. Developer names are all lower-case and are case-sensitive.

![Screenshot\_2022-05-10\_at\_12.22.02.png](https://support.stackerhq.com/hc/article_attachments/6121393787795)

### Field Types <a href="#h_01h9recbw9w0re94g5tw2gw05h" id="h_01h9recbw9w0re94g5tw2gw05h"></a>

* Text-type fields, such as Text and Long Text.
* Dropdowns. For multi-select dropdowns, only a single value can be auto-filled.
* Link to another record. These can be filled using the Stacker ID for the record (see below). For link fields which can take multiple values, only a single value can be auto-filled.
* Checkboxes can be filled by supplying the value true or false.
* Numbers, Percentages and Currencies. Percentages should be supplied as a fraction, so 40% is given as 0.4 in the URL.

### Finding record IDs for pre-filling links to other records <a href="#h_01h9recbw9qydanf1z18qe7fbw" id="h_01h9recbw9qydanf1z18qe7fbw"></a>

To fill a link to another record, you will need the Stacker ID for the linked record.

This can be found at the end of the URL of the record detail page on the table that the record is linked to, not the table you want to autofill.

For example:

Autofilling field "link to users" in the Form table. You need to click on the link to find the correct record ID and not the one shown on the detail page of the Form table.

![Screen\_Shot\_2021-04-06\_at\_5.22.57\_pm.png](https://support.stackerhq.com/hc/article_attachments/4409807548691)

![Screen\_Shot\_2021-04-06\_at\_5.23.06\_pm.png](https://support.stackerhq.com/hc/article_attachments/4409799426707)

My autofill url will look something like this:

![Screen\_Shot\_2021-04-06\_at\_5.30.31\_pm.png](https://support.stackerhq.com/hc/article_attachments/4409792179987)

&#x20;

If you need to auto-generate the auto-fill URL, the Stacker ID consists of a static Stacker table prefix, an underscore The Stacker ID consists of a static Stacker table prefix, an underscore and the Airtable Record ID if your data comes from Airtable.

If you use Google Sheets, the ID will either be the record's row number in the sheet, or the Stacker ID listed in the Stacker ID column in your sheet.

### How to use your auto-fill url <a href="#h_01h9recbw9dcctehas8hkaeecv" id="h_01h9recbw9dcctehas8hkaeecv"></a>

Once you have constructed your url you can use this in your app in a couple of ways:

* You can add it directly by including a banner widget in a detail view and pasting your URL into the 'Button URL' box and adding a label. This method can only be used if you want to autofill your create form with a static field i.e. you wanted a fixed value inputted
* You can alternatively add your URL into your Airtable base in a URL field and display it as a button. You can add this button in the list view or the detail view.

![Screenshot\_2020-11-24\_at\_11.04.13.png](https://support.stackerhq.com/hc/article_attachments/4409792190995)

![Screenshot\_2022-05-10\_at\_14.05.44.png](https://support.stackerhq.com/hc/article_attachments/6122491935507)

&#x20;

> This method requires you to enter the URL for each record individually!

**Auto-generation of autofill URL links in Airtable**

You may wish to have a button that autofills a create form based upon the specific record the button is pressed in - for example, you could create a new order for a particular item in an inventory table. Rather than having to manually formulate the URL for each individual record, we can use a formula in Airtable to do it automatically.

Our formula will take the following format:

```
/orders/new?autofill__inventory=inv_'&{Record ID}&'&autofill__type=Installation
```

* Where we use parenthesis to ask Airtable to 'print' this text, so anything between these will be static. Then we use the & to tie the two aspects together (it is not used here in the same way as in the actual URL) and then {Record ID} is asking Airtable to fill in information for each specific record (in this example the record ID which you will need to generate by adding in an additional formula field with the formula RECORD ID())

![Screenshot\_2020-11-27\_at\_17.02.36.png](https://support.stackerhq.com/hc/article_attachments/4409807568659)

![Screenshot\_2020-11-27\_at\_17.02.53.png](https://support.stackerhq.com/hc/article_attachments/4409799447571)

> Using this method, we only need to input the formula for the URL once and then Airtable will generate the link for every record added!

You can then add in your formula field to either the detail or list view and treat as a URL, switching it to a button as in the example previously.

_In the above example, we are generating a URL to be displayed as a button in the **Inventory** page, which autofills a new **Order** record with the linked record field as the specific_&#x20;

&#x20;

## Creating a new landing page on an Autofill link: <a href="#h_01h9recbwa210fpwa1tdsdv6wh" id="h_01h9recbwa210fpwa1tdsdv6wh"></a>

Adding this at the end of the URL would redirect to a specific detail record:

```
&previous=%2Fmeerkat%2Fcontacts%2Fview%2Fcon_recrlRnO0V8yzSTlM
```

It essentially means “Previous page we were on was /meerkat/contacts/view/con\_recrlRnO0V8yzSTlM”

* meerkat is the app name
* contacts is the table name
* view is just short for the detail view
* con\_recrlRnO0V8yzSTlM is the unique identifier for the record.

&#x20;
