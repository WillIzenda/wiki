#Caching in Izenda

[[_TOC_]]

##Question

What kinds of caching does Izenda use? Can I update the cache?

##Answer

Izenda caches all your reports and schema information automatically per browser session. By default, caching is stored in memory and in the temp folder of the server that Izenda is hosted on. Here is a list of the caching methods that are available in case you wish to manually update the cache, although generally the cache will self-update as needed.

###FilteredListReports

The [[AdHocConfig.FilteredListReports|http://wiki.izenda.us/FAQ/FilteredListReports]] method will return a list of reports that are guaranteed to be available to the current user. This means that the reports were found in storage, identified as available to the current user, successfully loaded from storage into cache, and ready for use.

###InvalidateFilteredCaches

The AdHocConfig.InvalidateFilteredCaches() method will clean up the results cached in the FilteredListReports method and can be called manually if needed. Like, for instance, when the XML definitions of one or more reports change outside the environment.

###DataCache Interval

Sets the number of seconds between cache refreshes. Example: ``AdHocSettings.DataCacheInterval = 60 * 24 * 30;``

###InvalidateSchemaCache

The AdHocContext.Driver.InvalidateSchemaCache() method will update the schema for database changes on, all filtered report lists, queries to the database that were cached, cached HTML results of reports, and cached XML report definitions.

###InvalidateSchemaOnNew

The AdHocSettings.InvalidateSchemaOnNew is a Boolean which tells the system if it should should update the schema for database changes when a new report is being created. This is useful for environments where the database is constantly changing.

###CleanUpCache

The ``FusionCache.CleanUpCache`` method is part of the Izenda Fusion Driver suite and will clear all cached XML reports and dashboards.

###RefreshAllCachedReports

The ``FusionCache.RefreshAllCachedReports`` method can be called to update the cache of XML reports and dashboards based on whether the time period specified in the [[DataCacheInterval|/API/CodeSamples/DataCacheInterval]] setting has elapsed since the last time the report was cached. Unlike CleanUpCache above, this will NOT clear the cache. It will include changes made to all HTML reports for the current user. You can call this method yourself to update the cache based on your unique business logic (such as daily, during downtime hours).

###RefreshAllCachedDashboards

The ``FusionCache.RefreshAllCachedDashboards method will update the cache of XML dashboards, but not reports, based on whether the time period specified in the [[DataCacheInterval|/API/CodeSamples/DataCacheInterval]] setting has elapsed since the last time the dashboard was cached. This can be called based on your unique business logic.

###StaticSharedStorage

The StaticSharedStorage class is used to implement a completely static memory mode for the entire application. This must be set before any calls to the Izenda API if it is to be used. This means that it must come before even the license key declaration. Otherwise, Izenda will automatically store much of its configuration data in Session. Here is how to initialize the class:

```csharp
StaticSharedStorage.Activate(true);
```

###Limitations

Izenda Reports is a web application. Therefore, caching is susceptible to the client state. For example, do not have Izenda Reports running in separate windows or tabs of Internet Explorer. Otherwise, you could get the following behavior: by loading a report in one window and then loading a different report in another window, you may have unknowingly cached the second report, overriding the first. To properly enforce caching, only have a single instance of Izenda Reports running at a time per browser session. If you do open other browser windows and create/modify reports in that window, be sure you do not go back to the previous tab to continue modifying reports. Otherwise, you may see the newly cached report in your viewer instead of the one you were expecting to see.