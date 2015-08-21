#Controllers in Umbraco

_There are are few types of controllers in Umbraco that perform different tasks_

##Render MVC Controllers

These are the controllers that get executed when rendering content during an Umbraco route. 

These controllers are of type `Umbraco.Web.MVC.RenderMvcController`.

See [Controller & Action Selection for details on using these controllers](../Default-Routing/Controller-Selection/)

##Surface Controllers

A SurfaceController is an MVC controller that interacts with the front-end rendering of an UmbracoPage. 
They can be used for rendering MVC Child Actions and for handling form data submissions. 
SurfaceControllers are auto-routed meaning that you don't have to add/create your own routes for these controllers to work. 

All implementations of SurfaceControllers inherit from the base class `Umbraco.Web.Mvc.SurfaceController`.

See [Reference documentation on SurfaceControllers for full details](../../../Reference/Routing/surface-controllers.md)

##Umbraco Api Controllers   

An Umbraco API Controller is an ASP.Net WebApi controller that is used for creating REST services. 
These controllers are auto-routed meaning that you don't have to add/create your own routes for these controllers to work.

All implementations of SurfaceControllers inherit from the base class `Umbraco.Web.WebApi.UmbracoApiController`.

See [Reference documentation on Umbraco Api Controllers for full details](../../../Reference/Routing/WebApi/index.md)

##Umbraco Authorized Controllers

An Umbraco Authorized controller is used when the controller requires member or user authentication (authN) and/or authorization (authZ).  
If either the authN or authZ fail the controller will return a "401 - unathorized response."  

The Umbraco Authorized controllers for back office users are:

#### MVC

Any MVC Controller or Action that is attributed with `Umbraco.Web.Mvc.UmbracoAuthorizeAttribute` will authenticate the request for a back office user.
A base class implementation that already exists with this attribute is: `Umbraco.Web.Mvc.UmbracoAuthorizedController`. These MVC controllers are not auto-routed.

#### WebApi

Any WebApi Controller or Action that is attributed with `Umbraco.Web.WebApi.UmbracoAuthorizeAttribute` will authenticate the request for a back office user.

A base class implementation that already exists with this attribute is: `Umbraco.Web.WebApi.UmbracoAuthorizedApiController`. Since this controller inherits from
`Umbraco.Web.WebApi.UmbracoApiController` it is auto-routed. This controller is also attributed with `Umbraco.Web.WebApi.IsBackOfficeAttribute` to ensure that it
is routed correctly to be authenticated for the back office.   

Another common base class implementation for the back office is `Umbraco.Web.Editors.UmbracoAuthorizedJsonController` which inherits from `Umbraco.Web.WebApi.UmbracoAuthorizedApiController`
but has some special filters applied to it to automatically handle anti-forgery tokens for use with AngularJS in the back office.

####Members and Users - Routing
There are specific rules used to determine if the request should used front end authN (members) or backoffice authN (users).  For details on the routes and route requirements see [Routing for authentication](../../../Reference/Routing/Authorized/index.md)  Umbraco Authorized controllers are not auto-routed so it is required to create routes specifically for your custom controllers.