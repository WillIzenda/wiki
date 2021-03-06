#PrintMode

[[_TOC_]]

##About

Gets or sets the value indicating what print mode will be used for printing reports on the ReportDesigner. There are a number of different settings for this property consisting of different combinations of HTML and PDF formats. This setting also controls the legacy ReportViewer toolbar. It currently has no effect on the modern ReportViewer.

**Default Value:** PrintMode.PdfAndHtml (PrintMode.Html2PdfAndHtml for version 6.6 and higher)

Possible values:
* PdfAndHtml
* Html2PdfAndHtml
* Html
* Pdf
* Html2Pdf

##Global.asax (C♯)

``` csharp
//main class: inherits DatabaseAdHocConfig or FileSystemAdHocConfig
public class CustomAdHocConfig : Izenda.AdHoc.DatabaseAdHocConfig
{
  // Configure settings
  // Add custom settings after setting the license key and connection string by overriding the ConfigureSettings() method
  public static void InitializeReporting() {
    //Check to see if we've already initialized.
    if (HttpContext.Current.Session == null || HttpContext.Current.Session["ReportingInitialized"] != null)
      return;
    AdHocSettings.LicenseKey = "INSERT_LICENSE_KEY_HERE";
    AdHocSettings.SqlServerConnectionString = "INSERT_CONNECTION_STRING_HERE";
    Izenda.AdHoc.AdHocSettings.AdHocConfig = new CustomAdHocConfig();
    AdHocSettings.PrintMode = PrintMode.Html2PdfAndHtml; //The relevant setting
    HttpContext.Current.Session["ReportingInitialized"] = true;
  }
}
```

##Global.asax (VB.NET)

```visualbasic
'main class: inherits DatabaseAdHocConfig or FileSystemAdHocConfig
Public Class CustomAdHocConfig
    Inherits Izenda.AdHoc.DatabaseAdHocConfig

    Shared Sub InitializeReporting()
        'Check to see if we've already initialized
        If HttpContext.Current.Session Is Nothing OrElse HttpContext.Current.Session("ReportingInitialized") IsNot Nothing Then
            Return
        'Initialize System
        AdHocSettings.LicenseKey = "INSERT_LICENSE_KEY_HERE"
        AdHocSettings.SqlServerConnectionString = "INSERT_CONNECTION_STRING_HERE"
        Izenda.AdHoc.AdHocSettings.AdHocConfig = New CustomAdHocConfig()
        AdHocSettings.PrintMode = PrintMode.Html2PdfAndHtml 'The relevant setting
        HttpContext.Current.Session("ReportingInitialized") = True
    End Sub
End Class
```

##Screenshots

PrintMode.Html2PdfAndHtml

![](/API/CodeSamples/PrintMode/PrintMode_Html2PdfAndHtml.png)

PrintMode.Html2Pdf

![](/API/CodeSamples/PrintMode/PrintMode_Html2Pdf.png)

PrintMode.Html

![](/API/CodeSamples/PrintMode/PrintMode_Html.png)