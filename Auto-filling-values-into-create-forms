# Auto-filling-values-into-create-forms

<p class="p1"><span class="s1">Create forms can be auto-filled with certain values by constructing an Auto-fill URL. You can then add this in to your app as a button to allow your users to create new records with some fields already filled in for them.</span></p>
<p class="p1"><strong>Note: Auto-fill only works on create forms. </strong></p>
<h2 class="p1" id="h_01H9RECBW93FXDXPQQ3189VQME"><span class="s1">How to construct your autofill URL</span></h2>
<p class="p1"><span class="s1">Where and how you do this is dependent on what the intended function of the URL will be...</span></p>
<p class="p1"><span class="s1">If you want to autofill your create form with a static field e.g. a fixed Type or Status and you want the button for this to be within each detail record view, you can add in a button by dragging a new 'Banner' container in and then adding in your Auto-fill URL directly into the box.</span></p>
<p class="p1"><span class="s1">However if you want to autofill your create form with a variable field i.e. something dependent on the current record you are in, using linked records etc, or you want to display your button on a list view -you need to add in your autofill URL as a new field in Airtable.</span></p>
<h2 class="p3" id="h_01H9RECBW9G53W4EP7X079B8GE"><span class="s1">Basic Link Structure</span></h2>
<p class="p1"><span class="s1">Auto-fill link</span><span style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;">s must be in the following format:</span></p>
<p class="p1"><span class="s1"><img style="font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Helvetica, Arial, sans-serif;" src="https://support.stackerhq.com/hc/article_attachments/11330614149267" alt="Autofill.png" width="607" height="78"></span></p>
<blockquote>We recommend using a relative link format i.e. not containing the start of your app URL (e.g. testapp-1.my.stacker.app) just in case you decide to change it or use a custom domain, then you won't need to update this URL too. </blockquote>
<ul class="ul1">
<li class="li5">
<span class="s3">where <em><strong>workspacename</strong></em></span><em><strong><span class="s4">/page/new</span></strong></em><span class="s3"><em><strong> </strong></em>- is the extension of the URL for the create form of the page you want to add a new record to. For example in one app where we would like to autofill values in the create form for the 'Members' page, the URL extension can be seen as /members/new</span>
</li>
<li class="li5">
<em><strong><span class="s4">field</span></strong></em><span class="s3"> is the developer name of the field to be filled</span>
</li>
</ul>
<p> </p>
<p>Auto-fill multiple fields by adding the <strong>&amp;</strong> separator in the url that you create. </p>
<p>For example:</p>
<p><img src="https://support.stackerhq.com/hc/article_attachments/11330753933331" alt="autofillplus.png"></p>
<p class="p1"><span class="s1">To find the developer names, go to <em class="far fa-table scolor"> </em><strong>Manage fields and data</strong> &gt; <strong>[Table name]</strong> &gt; <strong>Fields</strong> and toggle on <strong>Show developer name</strong>. </span><span class="s1">The developer name appears underneath the user-facing name for each field. Developer names are all lower-case and are case-sensitive.</span></p>
<p class="p1"><span class="s1"><img src="https://support.stackerhq.com/hc/article_attachments/6121393787795" alt="Screenshot_2022-05-10_at_12.22.02.png"></span></p>
<h3 class="p1" id="h_01H9RECBW9W0RE94G5TW2GW05H">Field Types</h3>
<ul class="ul1">
<li class="li1"><span class="s2">Text-type fields, such as Text and Long Text.</span></li>
<li class="li1"><span class="s2">Dropdowns. For multi-select dropdowns, only a single value can be auto-filled.</span></li>
<li class="li1"><span class="s2">Link to another record. These can be filled using the Stacker ID for the record (see below). For link fields which can take multiple values, only a single value can be auto-filled.</span></li>
<li class="li1">
<span class="s2">Checkboxes can be filled by supplying the value </span><span class="s3">true</span><span class="s2"> or </span><span class="s3">false</span><span class="s2">.</span>
</li>
<li class="li1">
<span class="s2">Numbers, Percentages and Currencies. Percentages should be supplied as a fraction, so 40% is given as </span><span class="s3">0.4</span><span class="s2"> in the URL.</span>
</li>
</ul>
<h3 class="p1" id="h_01H9RECBW9QYDANF1Z18QE7FBW"><span class="s1">Finding record IDs for pre-filling links to other records</span></h3>
<p class="p1"><span class="s1">To fill a link to another record, you will need the Stacker ID for the linked record.</span></p>
<p class="p1"><span class="s1">This can be found at the end of the URL of the record detail page on the table that the record is linked to, not the table you want to autofill.</span></p>
<p class="p1"><span class="s1">For example:</span></p>
<p class="p1"><span class="s1">Autofilling field "link to users" in the Form table. You need to click on the link to find the correct record ID and not the one shown on the detail page of the Form table.</span></p>
<p class="p1"><img src="https://support.stackerhq.com/hc/article_attachments/4409807548691" alt="Screen_Shot_2021-04-06_at_5.22.57_pm.png"></p>
<p class="p1"><img src="https://support.stackerhq.com/hc/article_attachments/4409799426707" alt="Screen_Shot_2021-04-06_at_5.23.06_pm.png"></p>
<p class="p1"><span class="s1">My autofill url will look something like this:</span></p>
<p class="p1"><img src="https://support.stackerhq.com/hc/article_attachments/4409792179987" alt="Screen_Shot_2021-04-06_at_5.30.31_pm.png"></p>
<p class="p1"> </p>
<p class="p1"><span class="s1">If you need to auto-generate the auto-fill URL, the Stacker ID consists of a static Stacker table prefix, an underscore The Stacker ID consists of a static Stacker table prefix, an underscore and the Airtable Record ID if your data comes from Airtable.</span></p>
<p class="p1"><span class="s1">If you use Google Sheets, the ID will either be the record's row number in the sheet, or the Stacker ID listed in the Stacker ID column in your sheet.</span></p>
<h3 class="p1" id="h_01H9RECBW9DCCTEHAS8HKAEECV"><span class="s1">How to use your auto-fill url</span></h3>
<p class="p1"><span class="s1">Once you have constructed your url you can use this in your app in a couple of ways:</span></p>
<ul class="ul1">
<li class="li2"><span class="s3">You can add it directly by including a banner widget in a detail view and pasting your URL into the 'Button URL' box and adding a label. This method can only be used if you want to autofill your create form with a static field i.e. you wanted a fixed value inputted</span></li>
</ul>
<ul class="ul1">
<li class="li1"><span class="s2">You can alternatively add your URL into your Airtable base in a URL field and display it as a button. You can add this button in the list view or the detail view.</span></li>
</ul>
<p><span class="s2"><img src="https://support.stackerhq.com/hc/article_attachments/4409792190995" alt="Screenshot_2020-11-24_at_11.04.13.png"></span></p>
<p><img src="https://support.stackerhq.com/hc/article_attachments/6122491935507" alt="Screenshot_2022-05-10_at_14.05.44.png"></p>
<p> </p>
<blockquote>This method requires you to enter the URL for each record individually!</blockquote>
<p class="p1"><span class="s1"><strong>Auto-generation of autofill URL links in Airtable</strong></span></p>
<p class="p2"><span class="s1">You may wish to have a button that autofills a create form based upon the specific record the button is pressed in - for example, you could create a new order for a particular item in an inventory table. Rather than having to manually formulate the URL for each individual record, we can use a formula in Airtable to do it automatically.</span></p>
<p class="p2"><span class="s1">Our formula will take the following format:</span></p>
<pre class="p2"><span class="s1"><code>/orders/new?autofill__inventory=inv_'&amp;{Record ID}&amp;'&amp;autofill__type=Installation</code></span></pre>
<ul class="ul1">
<li class="li4">
<span class="s3">Where we use parenthesis</span><span class="s3"> to ask Airtable to 'print' this text, so anything between these will be static. Then we use the </span><span class="s4">&amp;</span><span class="s3"> to tie the two aspects together (it is not used here in the same way as in the actual URL) and then </span><span class="s4">{Record ID}</span><span class="s3"> is asking Airtable to fill in information for each specific record (in this example the record ID which you will need to generate by adding in an additional formula field with the formula </span><span class="s4">RECORD ID())</span>
</li>
</ul>
<p><span class="s4"><img src="https://support.stackerhq.com/hc/article_attachments/4409807568659" alt="Screenshot_2020-11-27_at_17.02.36.png"></span></p>
<p><img src="https://support.stackerhq.com/hc/article_attachments/4409799447571" alt="Screenshot_2020-11-27_at_17.02.53.png"></p>
<blockquote>Using this method, we only need to input the formula for the URL once and then Airtable will generate the link for every record added!</blockquote>
<p class="p1"><span class="s1">You can then add in your formula field to either the detail or list view and treat as a URL, switching it to a button as in the example previously.</span></p>
<p class="p2"><span class="s1"><em>In the above example, we are generating a URL to be displayed as a button in the </em><strong><em>Inventory</em></strong><em> page, which autofills a new </em><strong><em>Order</em></strong><em> record with the linked record field as the specific<span class="Apple-converted-space"> </span></em></span></p>
<p class="p2"> </p>
<h2 id="h_01H9RECBWA210FPWA1TDSDV6WH">Creating a new landing page on an Autofill link:</h2>
<p>Adding this at the end of the URL would redirect to a specific detail record:</p>
<pre>&amp;previous=%2Fmeerkat%2Fcontacts%2Fview%2Fcon_recrlRnO0V8yzSTlM</pre>
<p>It essentially means “Previous page we were on was /meerkat/contacts/view/con_recrlRnO0V8yzSTlM”</p>
<ul>
<li>meerkat is the app name</li>
<li>contacts is the table name</li>
<li>view is just short for the detail view</li>
<li>con_recrlRnO0V8yzSTlM is the unique identifier for the record.</li>
</ul>
<p> </p>
