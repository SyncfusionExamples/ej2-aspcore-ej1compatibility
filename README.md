# Compatibility with Syncfusion ASP.NET Core (Essential JS 1)

This demo purpose to avoid EJ1 & EJ2 compatibility issues.

# Solution

The below setps help you to render EJ1 and EJ2 Syncfusion components in a single page ASP.NET Core Application.

## Adding application

You can create Essential JS 1 and Essential JS 2 controls using the following links:

Getting started for [EJ2 ASPNET Core control](https://ej2.syncfusion.com/aspnetcore/documentation/grid/getting-started-core)

Getting started for [EJ1 ASPNET Core control](https://help.syncfusion.com/aspnet-core/grid/getting-started)

## Style compatibility

Add compatibility styles. Essential JS 1 and Essential JS 2 controls have compatibility styles that do not affect each other.

```html
<head>
    @* Syncfusion Essential JS 1 Styles *@
    <link href="https://cdn.syncfusion.com/19.4.0.55/js/web/material/ej.web.all.compatibility.min.css"  rel="stylesheet"/>
    @* Syncfusion Essential JS 2 Styles *@
    <link href="https://cdn.syncfusion.com/ej2/19.4.55/styles/compatibility/material.css" rel="stylesheet" />
</head>
```

## Script compatibility

Add scripts for Essential JS 1 and Essential JS 2 as shown in the following codes

```html
    @* Syncfusion Essential JS 1 Scripts *@
    <script src="~/lib/jquery/dist/jquery.min.js"></script>
    <script src="https://cdn.syncfusion.com/js/assets/external/jsrender.min.js"></script>
    <script src="https://cdn.syncfusion.com/19.4.0.55/js/web/ej.web.all.min.js"></script>

    @* Syncfusion Essential JS 2 Scripts *@
    <script src="https://cdn.syncfusion.com/ej2/19.4.55/dist/ej2.min.js"></script>
```

Note: If you do not add ej1 script before ej2 script, it will throw script error.

## Adding compatibility

To add compatibility, use the following code in the _Layout.cshtml page. Since EJ1 and EJ2 controls have same library names to perform different actions, conflicts may occur when you refer these both controls in same application. To overcome this, extend these libraries in ej namespace.

```html
<script>
    var dataCopy = Object.assign({}, ej.data);
    $.extend(ej, Syncfusion);
    $.extend(ej.data, dataCopy);
</script>
```

## Adding script manager

Define script manager for both Essential JS 1 and Essential JS 2:

```html
    <ej-script-manager></ej-script-manager>
    <ejs-scripts></ejs-scripts>
```

The following code illustrates the final view of layout page.

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>@ViewData["Title"] - SyncfusionEJ1andEJ2</title>
    <link rel="stylesheet" href="~/lib/bootstrap/dist/css/bootstrap.min.css" />
    <link rel="stylesheet" href="~/css/site.css" asp-append-version="true" />
    <link rel="stylesheet" href="~/SyncfusionEJ1andEJ2.styles.css" asp-append-version="true" />
    @* Syncfusion Essential JS 1 Styles *@
    <link href="https://cdn.syncfusion.com/19.4.0.55/js/web/material/ej.web.all.compatibility.min.css"  rel="stylesheet"/>
    @* Syncfusion Essential JS 2 Styles *@
    <link href="https://cdn.syncfusion.com/ej2/19.4.55/styles/compatibility/material.css" rel="stylesheet" />

    @* Syncfusion Essential JS 1 Scripts *@
    <script src="~/lib/jquery/dist/jquery.min.js"></script>
    <script src="https://cdn.syncfusion.com/js/assets/external/jsrender.min.js"></script>
    <script src="https://cdn.syncfusion.com/19.4.0.55/js/web/ej.web.all.min.js"></script>

    @* Syncfusion Essential JS 2 Scripts *@
    <script src="https://cdn.syncfusion.com/ej2/19.4.55/dist/ej2.min.js"></script>
</head>
<body>
    <header>
        <nav class="navbar navbar-expand-sm navbar-toggleable-sm navbar-light bg-white border-bottom box-shadow mb-3">
            <div class="container">
                <a class="navbar-brand" asp-area="" asp-page="/Index">SyncfusionEJ1andEJ2</a>
                <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target=".navbar-collapse" aria-controls="navbarSupportedContent"
                        aria-expanded="false" aria-label="Toggle navigation">
                    <span class="navbar-toggler-icon"></span>
                </button>
                <div class="navbar-collapse collapse d-sm-inline-flex justify-content-between">
                    <ul class="navbar-nav flex-grow-1">
                        <li class="nav-item">
                            <a class="nav-link text-dark" asp-area="" asp-page="/Index">Home</a>
                        </li>
                        <li class="nav-item">
                            <a class="nav-link text-dark" asp-area="" asp-page="/Privacy">Privacy</a>
                        </li>
                    </ul>
                </div>
            </div>
        </nav>
    </header>
    <div class="container">
        <main role="main" class="pb-3">
            @RenderBody()
        </main>
    </div>

    <footer class="border-top footer text-muted">
        <div class="container">
            &copy; 2022 - SyncfusionEJ1andEJ2 - <a asp-area="" asp-page="/Privacy">Privacy</a>
        </div>
    </footer>

    <script src="~/lib/bootstrap/dist/js/bootstrap.bundle.min.js"></script>
    <script src="~/js/site.js" asp-append-version="true"></script>

    @await RenderSectionAsync("Scripts", required: false)
    <script>
        var dataCopy = Object.assign({}, ej.data);
        $.extend(ej, Syncfusion);
        $.extend(ej.data, dataCopy);
    </script>
    <ej-script-manager></ej-script-manager>
    <ejs-scripts></ejs-scripts>
</body>
</html>
```

## Declare Essential JS 1 and Essential JS 2 controls

Essential JS 1 and Essential JS 2 controls have already been initialized via getting started. If you want change control, you can initialize using the following code.

```html

<h2> Essential JS 1 - Grid Control</h2>

<ej-grid id="FlatGrid" allow-paging="true">
    <e-datamanager url="https://services.odata.org/v4/northwind/northwind.svc/Orders" adaptor="ODataV4Adaptor"></e-datamanager>
    <e-columns>
        <e-column field="OrderID" header-text="Order ID" text-align="Right" width="70"></e-column>
        <e-column field="CustomerID" header-text="Customer ID" width="80"></e-column>
        <e-column field="EmployeeID" header-text="Employee ID" text-align="Left" width="75"></e-column>
        <e-column field="Freight" header-text="Freight" text-align="Right" format="{0:C2}" width="75"></e-column>
        <e-column field="ShipCity" header-text="Ship City" width="110"></e-column>
    </e-columns>
</ej-grid>

<h2> Essential JS 2 - Grid Control</h2>

<ejs-grid id="Grid" allowPaging="true">
    <e-data-manager url="https://services.odata.org/V4/Northwind/Northwind.svc/Orders" adaptor="ODataV4Adaptor" crossdomain="true"></e-data-manager>
    <e-grid-columns>
        <e-grid-column field="OrderID" headerText="Order ID" type="number" textAlign="Right" width="120"></e-grid-column>
        <e-grid-column field="CustomerID" headerText="Customer ID" type="string" width="140"></e-grid-column>
        <e-grid-column field="Freight" headerText="Freight" textAlign="Right" format="C2" width="120"></e-grid-column>
        <e-grid-column field="OrderDate" headerText="Order Date" format='yMd' textAlign="Right" width="140"></e-grid-column>
    </e-grid-columns>
</ejs-grid>

```