#ODBC Connection String

[[_TOC_]]

##Question

Will My ODBC Connection String Work With Izenda Reports?

##Answer

Izenda Reports requires that a .NET provider and associated connection string be used.  This means that a .NET provider of some kind must be installed to access your database (e.g. Oracle.Net, MySQL.net provider, etc).  The provider will usually be installed on the web server (Microsoft IIS 5 or higher) that hosts the Izenda Reports application.  This will allow Izenda Reports to access the ADO.NET provider for the database that formerly used an ODBC connection.  Please note that installing a provider should not change any existing ODBC functionality, but it is always best to check with the provider vendor for full details.

Izenda Reports must use this provider since ODBC is a generic provider, and Izenda Reports requires that a special built-in account, "NETWORK SERVICE", has access to the database meta-data through IIS. This can not occur when using a generic ODBC provider. Once the provider is installed, you will need to use a connection string that is compatible with it.  Please see your provider documentation for details.