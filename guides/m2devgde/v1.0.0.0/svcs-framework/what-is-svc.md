---
layout: howtom2devgde
title: What is the Magento 2 Service Framework?
---
 
# What is the Magento 2 Service Framework?

<p><a href="{{ site.githuburl }}guides/m2devgde/v1.0.0.0/svcs-framework/what-is-svc.md" target="_blank"><em>Help us improve this page</em></a>&nbsp;<img src="{{ site.baseurl }}common/images/newWindow.gif"/></p>

The Magento 2 service framework defines and exposes extensible features. The service framework (also referred to as the *service layer*) is between the presentation layer and business logic as the following figure shows:

![The service interface accepts requests from web pages and web services, meaning they do not need to know the details of business logic]({{ site.baseurl }}common/images/service-layer_block-diagram.png "The service interface accepts requests from web pages and web services, meaning they do not need to know the details of business logic")

The service layer:

 * Is a functional abstraction that represents the business features available to other parts of an application or Magento. 
 * Represents a boundary that encapsulates the business logic a module exposes without revealing any of the details about how that functionality is implemented. 
 
A service is:

*  	An interface definition

	<a href="https://github.com/magento/magento2/tree/master/app/code/Magento/Customer/Service/V1" target="_blank">All Customer services interfaces</a>. 
	
*  	A class that implements the interface 

	The service class typically delegates some business logic to other components like models and helpers, making the service class relatively "thin".

	<a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/CustomerAccountService.php" target="_blank">Here</a> is a class that implements the <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/CustomerAccountServiceInterface.php" target="_blank">CusomterAccountServiceInterface</a>.

*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/build-svc.html#about-service-data-objects">Service data objects</a> that serialize, deserialize, and format data.	
	
## Benefits of the Service Layer

Benefits include:

<ul><li>Enables you to move business logic out of templates, which reduces the size of templates and makes customization easier.</li>
<li>Enables all business logic to be easily made available to external applications as web services by creating <tt>webapi.xml</tt> (<a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/etc/webapi.xml" target="_blank">sample</a>).</li>
<li>Services are versioned, which provides a way for them to be backward-compatible. We recommend, for example, that when you provide V2 of a service you enable V1 of the service to function after upgrading Magento software.</li></ul>
 
## Related Topics

*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/svcs-props.html">Interacting With Services</a>
*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/build-svc.html">Basics of Building a Service</a>
*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/svc-how-to-use.html">How a Client Uses a Service</a>
*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/compare_mage1_mage2.html">Services Use Case&mdash;Magento 1 and Magento 2 Side-By-Side</a>
*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/svc_create-customer-use-case.html">Services Use Case&mdash;Creating a Customer from an External Source</a>