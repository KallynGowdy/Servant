# Routing

Routing in Servant is built to be quick, easy, and configurable. There are a couple core features that need to be described though:

1. Servant implements routing using a layered architecture.
  - This allows Servant to provide two types of routing tools, convention based and configuration based.
  - The convention based routing gives you simple MVC style routing capabilities, whereas the configuration based routing allows you to do whatever you want.
2. Routes in Servant do not handle authentication or authorization.
  - This allows the router to do what it does best, trigger the right code when a request comes in.
  - For reference, authentication and authorization are handled by separate components that can be called by content endpoints.
3. Routes do not automatically redirect.
  - If you return a response to the client, routes will not get in the way of that and change it up.
  - Unless you specify, routes will not automatically rewrite the URL to point to the canonical endpoint.
4. Routes in Servant follow a path through content endpoints.
  - Content endpoints are what they say they are. Places where data is exposed to the services.
  - Content endpoints are where you talk to your data access layer.

So, with those "out of the way", we can talk about the two routing APIs that Servant provides.

The first API is the core routing library. This library is what all other routing in Servant is built on. The goals of this library are to provide a simple, declarative configuration API for setting up routes to different parts of the application and to make automation of route configuration easy for convention based setups.

The second API is the convention routing library. This library seeks to provide a super high-level convention based API for rigging routes to your code while still giving you hooks into the core routing library.


## Core

The core routing library allows you to define routes just like you would in most any other library, but it also gives you much more control and configuration than you would normally get.

Let's start with the basics:

What is a route?

A route is an object that defines a _path_ and it's corresponding _target_. Often, routes are used to trigger specific code to run when a certain URL is requested.

How do you define a route with Servant?

Routes in Servant are defined using implementations of the `IServantRouteBuilder` interface. Often, you will create a route using a static URL and bind it to a specific service.
