# CloudFront #

## Introduction ##

It's a **Content Distribution Network** (CDN), it creates copies of your website at various Edge Locations around the world. Requests are served from the nearest Edge Location.

A **CDN** it's a distributed network of servers which delivers web pages and content to users, based on their geographical location, the origin of the webpage and a content delivery server.

## Core Components ##

* **Origin**, the location where all original files are located (S3, EC2, ELB, Route53)
* **Edge Location**, location where the web content will be cached
* **Distribution**, a collection of Edge Locations which defines how cached content should behave
  * you need to specify the origin
  * it replicates based on the Price Class
  * two types:
    * **Web**, for websites
    * **RTMP**, for streaming media
  * you can set:
    * **Behaviours**, redirect to HTTPS, restrict HTTP methods, restrict viewer access
    * **Invalidations**, manually invalidate cache on specific files
    * **Error Pages**, serve custom 404 pages
    * **Restrictions**, blacklist or whitelist specific country with Geo Restrictions

* **Lambda@Edge**, it's a feature to override the behaviour of request and responses. Are lambda functions. Use case is when you have protected content, only for authorized users. 4 types:
  * **Viewer request**, when CloudFront receives a request from a viewer
  * **Origin request**, before CloudFront forwards a request to the origin
  * **Origin response**, when CloudFront receives a response from the origin
  * **Viewer response**, before CloudFront, return the response to the viewer

* **Protection**, by default a Distribution allows everyone to have access. You can enable Restrict Viewer Access, that will use Signed Urls and Signed Cookies, that need an Original Access Identity.
  * **Original Access Identity** (OAI), a virtual user identity that will be used to give to CloudFront permissions to fetch a private object
  * **Signed URL**, url with temporary access to cached objects
  * **Signed Cookie**, cookie that is passed along with the request to CloudFront. Useful to provide access to multiple restricted files
