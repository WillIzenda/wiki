#Adding Bulk CSV On the Report Viewer

[[_TOC_]]

##Question

How do I Add the Bulk CSV option to the Report Viewer and Report Designer?

##Answer

You can alter the CSV option to use the bulk CSV functionality on the report viewer and report designer by setting [[UseBulkCSV|/API/CodeSamples/UseBulkCSV]] = true in your global.asax. If you wish to use regular CSV exports and bulk CSV exports at the same time, there are a few different methods to accomplish this.

Newer versions of Izenda have diverged the Report Viewer from the Report Designer methodology of showing this button. One methodology for the Report Viewer is demonstrated below, but this is not an absolute edict.


###
###Report Viewer

The report viewer page is all contained in Resources/html/ReportViewer-Body.ascx and is completely editable within any standard text editor. Therefore, you can use any HTML you want as long as you call the following javascript function:

```javascript
responseServer.OpenUrlWithModalDialogNew, 'rs.aspx?output=BULKCSV', 'aspnetForm', 'reportFrame');
```

Here is an example HTML snippet to insert a new item into an unordered list (can be used on ReportViewer)

```html
<li><a href="javascript:void(0)" title=""
  onclick="responseServer.OpenUrlWithModalDialogNew, 'rs.aspx?output=BULKCSV', 'aspnetForm', 'reportFrame');">
  <img class="icon" src="rs.aspx?image=ModernImages.csv-32.png" alt="" />
  <b lang-text="js_CSV">Bulk CSV</b><br>
  <span lang-text="js_CSVMessage">Stores large batches of tabular data in a text file that is portable and easy to process</span>
</a></li>
```

###Report Designer

This code will show how to show the bulk csv option on the Report Designer.

```csharp
//show (unhide) the option for bulk csv
AdHocSettings.OutputTypes["BULKCSV"].Hidden = false;

//hide the option for csv
AdHocSettings.OutputTypes["CSV"].Hidden = true;

```

###String keys for other output types

The string keys which are available are listed [[in this article|/FAQ/Formatting/How-do-I-hide-Output-Types]]

##Troubleshooting the Bulk CSV Option

The Bulk CSV option is for exporting large amounts of data and is inherently dependent on your server's ability to process the data. If you are getting an **Out of memory exception**, the bulk CSV option may not be right for your application. 

If you are getting a **504 Gateway Time-out** error, you may need to set the [[SqlCommandTimeout]] setting to a higher value to allow for larger exports.

If you want to test the bulk CSV export option to see if it's correct for you, follow the steps below.

* Open a larger report in the Report Viewer
* Append the string "&output=bulkcsv" onto the URL (e.g. http://www.izenda.com/bi/ReportViewer.aspx?rn=Budget&output=bulkcsv)
* Press enter to export the report as a bulk csv file

_**Note:** The total amount of records that will be exported via the bulk CSV option will still be limited by the [[ExportLimit|/API/CodeSamples/ExportLimit]] setting._