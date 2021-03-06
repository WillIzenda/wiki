#Divide by Zero

[[_TOC_]]

##Question

I'm Getting #DIV/0 In My Report preview. What is this? Can I change it?

##Answer

If you accidentally divide by zero, Izenda would handle it by outputting the string "#DIV/0". However, you can change the output text with a custom format option. This functionality was implemented in release 6.7.0.258.

Usage; code for your Izenda ``global.asax``:

```csharp
// By default the display still shows "#DIV/0" when a divide by zero action occurs.


//To Display "Division by Zero Text"
(AdHocSettings.Formats.Get("DivisionByZero") as AdHoc.Formats.Formats.DivisionByZeroFormat).ReplaceText = "Division by Zero Text";


//To Display "0"
(AdHocSettings.Formats.Get("DivisionByZero") as AdHoc.Formats.Formats.DivisionByZeroFormat).ReplaceText = "0";


//To Display NULL (nothing)
(AdHocSettings.Formats.Get("DivisionByZero") as AdHoc.Formats.Formats.DivisionByZeroFormat).ReplaceText = "";
```

###Expressions

The use of expressions in a calculated field will cause the SQL server itself to throw a DIV/0 error. This is opposed to arithmetic operators, which will not cause SQL to throw exceptions. In the case of using expressions, you will have to catch possible divide by zero errors in a case statement. One example is detailed below.

```sql
CASE WHEN [OrderID]=0 THEN CAST(2147483647 AS float) ELSE [Freight]/[OrderID]
```

Using the number seen in the cast will indicate to Izenda that it should use the DIV/0 format option for that value.