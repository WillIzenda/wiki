#ReportViewerConfig

[[_TOC_]]

##About

The ``reportviewerconfig`` command is passed through rs.aspx via an [[AjaxRequest|/API/CodeSamples/Javascript/AjaxRequest]]. This returns JSON formatted data related to the Report Viewer page's configuration. It can be used to control whether the current report that is loading is read-only, view-only, or locked. It also returns several settings that are found in [[AdHocSettings|/API/AdHocSettings]] related to the report viewer.

Here is the Ajax call to use:

```javascript
AjaxRequest('./rs.aspx', 'wscmd=reportviewerconfig&wsarg0=' + jq$(window).width() + '&wsarg1=' + jq$(window).height(), GotReportViewerConfig, null, 'reportviewerconfig');
```

Here is a list of the object keys sent back and their default values

|Key|Value|
|:-:|:---:|
|ReportListUrl|ReportList.aspx|
|ReportDesignerUrl|ReportDesigner.aspx|		
|ResponseServerUrl|rs.aspx|
|ReportViewerUrl|ReportViewer.aspx|
|DashboardsUrl|Dashboards.aspx|		
|InitialResults|100|
|ReportIsReadOnly|false|
|ReportIsViewOnly|false|
|ReportIsLocked|false|
|AllowNewFiltersInReportViewer|true|
|AllowRTFExportFormat|false|
|DateFormat|m/d/yy|
|CategoryCharacter|\\|
|UseBulkCsv|false|

GotReportViewerConfig is a callback method that takes two arguments. The first is the data above. The second is the id of the config object.