[[API]]
# Two Sides of API Management 

*Administrative* 
- Define or import APIs
- Define policies
- bundle APIs into products
- manage users and subscriptions
- Monitor API usage
	- Consumption level

*Consumer/Developer*
- Subscribe to products
	- The consumer can use these products
- Check API documentation
- Test APIs using interactive console
- Check their own analytics

> [!NOTE] Personal Experience 
> This reminds me of using the Strava API, in that case I was the consumer

## Components
### Administrative
APIs and Operations, API Gateway, Policies

### Consumer
Products, users, groups, subscriptions and developer portal

*users* -> by creating user groups you manage visibility of products. 
- Admins are built in and it contains the owner of the account 
- Developers can access the developer portal and subscribe to groups 
- Guests -> Anonymous users who can browse the portal but not call APIs unless authorized 
- You can also create custom groups and assign people to them by the Azure Active Directory 

*Product* -> Bundle of APIs that can be used. 
- Types: 
	- Open product -> anybody can use it through the developer portal. Without subscribing they can access the APIs inside. 
	- Protected product -> User needs to subscribe to the product, you could get access immediately or admins could provide access. Both can happen. 

### Subscription
Product + user = once a user subscribes to a product -> receives subscription key for a product to access it
- some subscriptions are protected, others are open. 

## Creating Products/Bundles
Inside the API portal, on the left hand side you can see the option for Products.

You have a starter pack and unlimited. 

On the top left you can click add and create a new product 

Here you decide if its an open product or if its a protected product
- Requires subscription -> if unchecked its an open product 
	- You also decide the count limit of subscriptions -> for example only a maximum of 10 people. 
- Requires approval -> if checked, it will require admin approval

There is also a section for legal terms 

At the bottom of this window, you select the APIs that will part of this product 

Inside the bundle, you have an option to open access control and decide who can use this bundle 

# Developer Portal Overview
Automatically generated fully customizable website with documentation for your API 

You just need to `publish` inside the Portal Overview 

You should enable the CORS -> cross origin resource sharing 

If you click on the portal from the Management Console, it will take you to *admin view* where you can modify the website. This website is easily modifiable with drag and drop features. 

*As a consumer* you can sign up right ahead after creation and you'll have access to the API. As an admin you don't need to create anything. 
- This is like any subscription to a package of APIs like Strava or google. 
- Inside the portal you can also test the APIs - you can only test after being authorized 

Inside the API Portal management console, there is a section called `subscriptions` here you approve the requests to use the API bundle

*As a consumer*, after you subscribe, you get your primary and secondary keys. The request for subscription will be in `submitted` state. After the admin approves it, it will become approved and you will be able to use the APIs. 






