#ConfigureSettings()

This method controls global settings. These settings will remain set for all users and reports. Any settings placed inside will override the settings.aspx page settings. This method should be overridden in your global.asax file provided the global.asax main class also inherits the DatabaseAdHocConfig or FileSystemAdHocConfig interfaces.

##C♯

```csharp
public override void ConfigureSettings()
{
    Izenda.AdHoc.AdHocSettings.ShowInvisible = true; 
    Izenda.AdHoc.AdHocSettings.ShowClientEmailButton = false;
}
```

##VB.NET

```visualbasic
Public Overrides Sub ConfigureSettings()
    Izenda.AdHoc.AdHocSettings.ShowInvisible = True
    Izenda.AdHoc.AdHocSettings.ShowClientEmailButton = False
End Sub