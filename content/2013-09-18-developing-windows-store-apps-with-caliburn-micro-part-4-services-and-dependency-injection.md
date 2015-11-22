---
title: 'Developing Windows Store apps with Caliburn Micro Part 4: services and dependency injection'
author: Igor Kulman
layout: post
date: 2013-09-18
url: /developing-windows-store-apps-with-caliburn-micro-part-4-services-and-dependency-injection/
dsq_thread_id:
  - 1774910578
categories:
  - WinRT
tags:
  - 'c#'
  - Caliburn.Micro
  - fody
  - metro
  - winrt
  - xaml
---
In this installment of the series I will show you how user data services. We will finally use the Unity DI container that is part of the project setup.

**Data and Services**

In next installment we will be showing a list of products, so let&#8217;s create a simple Product class first in the Data directory:

PropertyChangedBase is a base class implementing the INotifyPropertyChanged interface and the ImplementPropertyChanged attribute makes sure it&#8217;s method is called for all the property changes. (More about Fody [here][1])

All the operations will be handled by a service implementing the IProductService interface:

You can implement this interface any way you want. To keep things simple I chose an implementation with two hardcoded products:

**Registering services**

All our services need to be registered with the Unity DI container before being used. The place to do it is the App class (App.xaml.cs file). You can override the Configure method to do it:

This registers the ProductService class to the IProductService interface. The new ContainerControlledLifetimeManager() parameter is Unity&#8217;s way of setting the registration to be a singleton.

**Injecting services into ViewModel**

Injecting the ProductService into our MainViewModel is very simple. Just declare a IProductService variable and initialize it from constructor. Unity will take care of the rest:

Next time we will implement a typical master-detail scenario showing products usign the ProductService whe have created. All the code is again [available at GitHub][2].

 [1]: http://blog.kulman.sk/inotifypropertychanged-the-easy-way-in-windows-phone-and-windows-8/ "INotifyPropertyChanged the easy way in Windows Phone and Windows 8"
 [2]: https://github.com/igorkulman/CaliburnDemoWinRT