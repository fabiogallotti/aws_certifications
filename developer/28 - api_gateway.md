# API Gateway #

## Introduction ##

It's a service to create, publish, maintain, monitor and secure APIs at any scale. It creates APIs that act as a front door for applications to access data, business logic, or backend functionalities.

API Gateway:

* Handles all the tasks involved in processing up to **10.000/second** concurrent API calls, including traffic management, authorization, monitoring.
* Allows to track and control any usage of the APIs
* Expose HTTPS endpoints to define a RESTful API
* Highly scalable automatically
* Maintains many version of the same API

## Main Concepts ##

* **Resources**, are the urls you define to access the API. Can have children resources
* **Methods**, defined on a Resource (can be multiple), allow you to make API calls with a specific protocol (GET, POST, DELETE)
* **Stages**, are versions of the API. In order to use the API you need to Deploy it to Stages
* **Invoke URL**, the URL where you can make API calls, for each stage. It's possible to use a custom domain
* **Deploy API**, everytime you make a change to the API you need to deploy it, choosing the stage
* **Integration type**, when you create a Method you need to choose the integration type, the most common is Lambda. You can tune Request and Response.
* **Caching**, can be enabled to cache the endpoints response to API calls
  * caches responses for a specified Time To Live (TTL) period
  * reduces number of calls to the endpoint
  * improves latency
* **Same-Origin Policy**, is a concept in the application security model, where a browser permits to some scripts contained in a first webpage, to access data in a second webpage
  * helps to prevent Cross-site scripting (XSS) attacks
* **Cross-Origin Resource Sharing (CORS)**, is a way for the server to relax a same-origin policy
  * allows restricted resources to be requested from a different domain than the one of the initial resource
  * always enforced by the client
