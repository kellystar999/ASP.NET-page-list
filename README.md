# What is MvcPagedList.Core ?

Easily paging in ASP.NET Core that get data as chunks from database

# Install via NuGet

To install MvcPagedList.Core, run the following command in the Package Manager Console
```code
pm> Install-Package MvcPagedList.Core
```
You can also view the [package page](https://www.nuget.org/packages/MvcPagedList.Core/) on NuGet.

# How to use ?
It is very simple to use. You just need to provide PageCount, currentPage and TotalItemCount in your controller and send them by [ViewBags](https://github.com/hamed-shirbandi/MvcPagedList.Core/blob/e868ad365424c474a8a7324cf4987c425bc912f6/MvcPagedList.Core.Example/Controllers/HomeController.cs#L44) to the view. Then in the view you just need to call [PagedList.Pager()](https://github.com/hamed-shirbandi/MvcPagedList.Core/blob/e868ad365424c474a8a7324cf4987c425bc912f6/MvcPagedList.Core.Example/Views/Home/_UsersPagedList.cshtml#L3) to show the pagination.


```code

@PagedList.Pager(actionName: "search", controllerName: "home",
    pagerOptions: new PagerOptions
    {
        currentPage = (int)ViewBag.CurrentPage,
        PageCount = (int)ViewBag.PageSize,
        TotalItemCount = (int)ViewBag.TotalItemCount,
    } )
    
```

# How to pass route values to the controller?
PagedList.Pager has a routeValues parameter. You can use it like bellow to pass your data to the controller:
```code

@PagedList.Pager(actionName: "search", controllerName: "home",
    routeValues: new
    {
        //Here we set term as a value and send it to the controller
        term = Context.Request.Query["term"],
    },
    pagerOptions: 
    {
      ...
    } )
    
```

# How to enable ajax pagination?
PagedList.Pager has an ajaxAttributes parameter. You can use it like bellow to enable ajax:
> Here you can use all [data-ajax attributes](https://github.com/hamed-shirbandi/MvcPagedList.Core/issues/11#issuecomment-984938612). Just replace "-" with "_"
```code

@PagedList.Pager(actionName: "search", controllerName: "home",
    ajaxAttributes: new
    {
        data_ajax = "true",
        data_ajax_loading = "#global-ajax-loading",
        data_ajax_update = "#ajax-show-list",
        data_ajax_method = "GET",
        data_ajax_mode = "replace"
    },
    pagerOptions: 
    {
      ...
    } )
    
```
 
# How to customize the pagination?
PagedList.Pager has a pagerOptions parameter. It has many properties that you can use to customize the pagination. Here is a table to describe the properties:
| Prop Name     | Description  
| ------------- | ------------- 
| TotalItemCount        | It is used to show total items count and should be provided by Controller
| PageCount        | It is used to show total pages count and should be provided by Controller
| CurrentPage        | It is used to show current page and should be provided by Controller    
| DisplayMode        | It used to controll display mode for the pagiation and has 3 options: • use 'DisplayMode.Never' when you want to hide the pagination in UI • use 'DisplayMode.IfNeeded' when you want to show the pagination if there is atleast 2 page to show • use 'DisplayMode.Always' when you want to show the pagination even there is 0 or 1 page 
| DisplayLinkToPreviousPage         |   Set it to ` false ` if you dont want to show the previous btn
| DisplayLinkToNextPage         | Set it to ` false ` if you dont want to show the next btn         
| DisplayInfoArea         | Set it to ` false ` if you dont want to show the information area and just need to show the pages. information area is a section bellow the pages to show TotalItemCount and PageCount and CurrentPage    
| DisplayPageCountAndCurrentLocation         | Set it to ` false ` if you dont want to show PageCount and CurrentPage in info area    
| CurrentLocationFormat         | It is a lable for currentPage. for example 'page' in 'page 1 of 12'   
| PageCountFormat         | It is a lable for PageCount. for example 'of' in 'page 1 of 12'    
| DisplayTotalItemCount         |  Set it to ` false ` if you dont want to show TotalItemCount in info area      
| TotalItemCountFormat         |  It is a lable for TotalItemCount. for example 'total items count' in 'total items count 400'     
| LinkToNextPageFormat         | It is a lable for next btn. for example 'next' or '>>'   
| LinkToPreviousPageFormat         | It is a lable for prev btn. for example 'prev' or '<<'       
| WrapperClasses         |  It is used to add a class from your custom css for main wrapper of the pagination    
| UlElementClasses         | It is used to add a class from your custom css for ul tage that wrapps all page numbers    
| LiElementClasses         | It is used to add a class from your custom css for li tags that wrapps each page number  
| GetStyleSheetFileFromCdn         | Set it to ` false ` if you dont want to load css file from CDN. Then you have to add it to your pages    
| DisplayPageNumbers         | Set it to ` false ` if you dont want to show the pages and just need to show info area    
| DisplayAjaxLoading         | Set it to ` false ` if you dont want to show ajax loading element    
| AjaxLoadingFormat         | Let it empty if you want to show default ajax loading or write a text to show when ajax request is sending by the pagination. for example you can write 'Please wait ... ' and it will be shown during an ajax request     


# Screenshots

![alt text](https://github.com/hamed-shirbandi/MvcPagedList.Core/blob/master/MvcPagedList.Core.Example/wwwroot/images/Screenshot-1.png)
