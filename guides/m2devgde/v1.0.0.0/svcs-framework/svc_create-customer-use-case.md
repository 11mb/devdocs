---
layout: howtom2devgde_chapters
title: Services Use Case&mdash;Creating a Customer from an External Source 
---
 
# Services Use Case&mdash;Creating a Customer from an External Source

<p><a href="{{ site.githuburl }}guides/m2devgde/v1.0.0.0/svcs-framework/svc_create-customer-use-case.md" target="_blank"><em>Help us improve this page</em></a>&nbsp;<img src="{{ site.baseurl }}common/images/newWindow.gif"/></p>

Say you want to create customer records in Magento from an external source like Salesforce, Facebook, PayPal, or Google. How does the Magento service framework help you do that?

This topic discusses a simplified way to create customer records using a conceptualized service. We discuss how to get started by helping you examine service layer models and interfaces to get the mechanism you need; and how to use the data object builder and service data objects to send the data. After you read this topic, you should have a general idea of how to work with services.

## Getting Started

Before you think about writing your own service, you should look at an existing Magento service to see what it offers you. For example, the Customer service provides the following resources:

*	Models

	Models interact with resources to do things like get objects, set passwords, and perform authentication. Customer service models have more than 70 public methods, including `public function loadByEmail($customerEmail)` in <a href="https://github.com/magento/magento2/tree/master/app/code/Magento/Customer/Model/Customer.php" target="_blank">Customer</a>, which gets a customer record using their e-mail address.
	
	One advantage of using a service is your client code doesn't interact directly with the model at all; the service does that for you.

*	Interfaces

	Clients interact with services using methods on their interfaces, as discussed in [What is the Magento 2 Service Framework?](what-is-svc.html). Customer service interfaces have more than 20 public methods, including public function `createCustomer()` in <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/CustomerAccountServiceInterface.php" target="_blank">CustomerAccountServiceInterface</a>, which creates a customer record.

*	Service data objects

	Service data objects send data to and from interfaces. Service data objects are "read-only", meaning they have getters but not setters. The Customer service has several service data objects, including <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/Data/Customer.php" target="_blank">Customer</a>, which returns customer data.
	
*	Service data object builders

	Builders have the setters you can use to set data values in the service data object before sending them to the service to be consumed. For example, <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/Data/CustomerBuilder.php" target="_blank">CustomerBuilder</a> has a `setFirstname` method you can use to set a customer's first name. You can get the first name using the `getFirstname` method in <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/Data/Customer.php" target="_blank">Customer data object</a>.

## Creating the Customer Record 

Create a customer record as follows:

1.	Locate the `createCustomer` method on the <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/CustomerAccountServiceInterface.php" target="_blank">CustomerAccountServiceInterface</a>. 

	Notice the code comments also:

	<script src="https://gist.github.com/xcomSteveJohnson/398aa808d3986351b972.js"></script>
	
	This is the interface your client code interacts with. 

2.	In your client code, declare a constructor dependency:

	<script src="https://gist.github.com/xcomSteveJohnson/4b9a08174a6aaa83a4e8.js"></script>
	
	Dependency injection passes (injects) dependencies to an object instead of the object pulling the dependencies from the environment. In other words, instead of objects configuring themselves, the objects are configured by an external entity. For more information, see <a href="https://wiki.magento.com/display/MAGE2DOC/Using+Dependency+Injection" target="_blank">Using Dependency Injection</a>.
	
	Constructor dependency injection uses a constructor to declare the dependencies. In dependencies in the preceding example are named:
	
	*	`$customerAccountService`, a dependency on <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/CustomerAccountServiceInterface.php" target="_blank">CustomerAccountServiceInterface</a>.
	*	`$customerDetailsBuilder`, a dependency on <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/Data/CustomerDetailsBuilder.php" target="_blank">CustomerDetailsBuilder</a> data object builder.
	*	`$customerBuilder`, a dependency on <a href="https://github.com/magento/magento2/blob/master/app/code/Magento/Customer/Service/V1/Data/CustomerBuilder.php" target="_blank">CustomerBuilder</a> CustomerBuilder data object builder.
	
3.	In your client code, create the customer record.

	<script src="https://gist.github.com/xcomSteveJohnson/d9c51387caa8f7f8d15f.js"></script>
	
	This code uses the dependencies declared in step 2 to create a customer record.
	
## Summary

The preceding section showed how to:

*	Create a customer record.
*	Create addresses for the customer.
*	Set up a password reset token.
*	Send the customer a welcome e-mail with a link to reset their password.

#### Related Topics

*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/svc-how-to-use.html">How a Client Uses a Service</a>
*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/svcs-framework/build-svc.html">Basics of Building a Service</a>
*	<a href="{{ site.baseurl }}guides/m2devgde/v1.0.0.0/rest/rest-overview.html">Accessing Magento Objects Using REST</a>
