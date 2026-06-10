# OptimizelyCms13Lab

Solution to show problem with Razor Pages in EPiServer CMS 13.

## Prerequisites

- EPiServer.Templates 2.0.1

## Steps to reproduce

- dotnet new epi-cms-empty
- Add endpoints.MapRazorPages() in Startup.cs

		app.UseEndpoints(endpoints =>
		{
			endpoints.MapContent();
			endpoints.MapRazorPages();
		});

- Create a simple start-page (/Models/Pages/StartPage.cs)
- Create a Razor Page as start page (/Pages/Index.cshtml)
- Run the application
- Create an In-Process application in settings and create a new StartPage

## Problems

- CurrentContent is null when browsing to the start-page
- In edit-mode in the preview area you get an exception:

	System.InvalidOperationException: Failed to compare two elements in the array.
		---> System.NullReferenceException: Object reference not set to an instance of an object.
		at EPiServer.Web.Routing.Matching.Internal.DefaultActionComparer.CompareMetadata(ControllerActionDescriptor x, ControllerActionDescriptor y) in /_/src/content-platform/src/EPiServer.Cms.AspNetCore.Routing/Web/Routing/Matching/Internal/DefaultActionComparer.cs:line 20
		at EPiServer.Web.Routing.Matching.Internal.EndpointComparer.Compare(Endpoint x, Endpoint y) in /_/src/content-platform/src/EPiServer.Cms.AspNetCore.Routing/Web/Routing/Matching/Internal/EndpointComparer.cs:line 24
		at System.Linq.Enumerable.EnumerableSorter`2.CompareAnyKeys(Int32 index1, Int32 index2)
		at System.Collections.Generic.ArraySortHelper`1.SwapIfGreater(Span`1 keys, Comparison`1 comparer, Int32 i, Int32 j)
		at System.Collections.Generic.ArraySortHelper`1.IntroSort(Span`1 keys, Int32 depthLimit, Comparison`1 comparer)
		at System.Collections.Generic.ArraySortHelper`1.Sort(Span`1 keys, Comparison`1 comparer)
		--- End of inner exception stack trace ---
		at System.Collections.Generic.ArraySortHelper`1.Sort(Span`1 keys, Comparison`1 comparer)
		at System.Linq.Enumerable.EnumerableSorter`2.QuickSort(Int32[] keys, Int32 lo, Int32 hi)
		at System.Linq.Enumerable.EnumerableSorter`1.Sort(TElement[] elements, Int32 count)
		at System.Linq.Enumerable.OrderedIterator`1.Fill(TElement[] buffer, Span`1 destination)
		at System.Linq.Enumerable.OrderedIterator`1.ToArray()
		at EPiServer.Web.Routing.Matching.Internal.DefaultContentEndpointSelector.SelectAsync(ContentRouteData contentRouteData, HttpContext context) in /_/src/content-platform/src/EPiServer.Cms.AspNetCore.Routing/Web/Routing/Matching/Internal/DefaultContentEndpointSelector.cs:line 48
		at EPiServer.Web.Routing.Matching.Internal.ContentMatcherPolicy.MapEndpointAsync(Endpoint originalEndpoint, HttpContext httpContext) in /_/src/content-platform/src/EPiServer.Cms.AspNetCore.Routing/Web/Routing/Matching/Internal/ContentMatcherPolicy.cs:line 202
		at EPiServer.Web.Routing.Matching.Internal.ContentMatcherPolicy.ApplyAsync(HttpContext httpContext, CandidateSet candidates) in /_/src/content-platform/src/EPiServer.Cms.AspNetCore.Routing/Web/Routing/Matching/Internal/ContentMatcherPolicy.cs:line 75
		at Microsoft.AspNetCore.Routing.Matching.DfaMatcher.SelectEndpointWithPoliciesAsync(HttpContext httpContext, IEndpointSelectorPolicy[] policies, CandidateSet candidateSet)
		at Microsoft.AspNetCore.Routing.EndpointRoutingMiddleware.<Invoke>g__AwaitMatch|10_1(EndpointRoutingMiddleware middleware, HttpContext httpContext, Task matchTask)
		at Microsoft.AspNetCore.Diagnostics.DeveloperExceptionPageMiddlewareImpl.Invoke(HttpContext context)