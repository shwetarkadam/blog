---
title:  "Integrating Swagger OpenAPI for easy API documentation in spring boot"
date: 2022-01-16T15:34:30-04:00
categories:
  - API specification
  - REST API
tags:
  - Swagger OPENAPI
  - API documentation
  - spring boot
  - REST API
published: true
comments: true
author_profile: true
header:
  teaser: "/assets/images/swaggerui.PNG"
toc: true
toc_label: "Table of Contents"
toc_icon: "cog"  
---

These days I am more into creating backend projects which include microservices.But if anyone wants to test these services one needs postman or do the old classic way of curl command. 

Both do the job brilliantly but what if I wanted some user who doesn't want to install postman or use curl and still wants to test my live APIs thru the browser? I came across this ***swagger open API specification*** and this is a really handy tool!


In layman's terms, Swagger OpenAPI specification provides ***API documentation*** for REST APIs. An OpenAPI file allows you to describe all the APIs within the project and even lets you ***try out the APIs!***

Available endpoints can be /projectApi and all operations on each endpoint which can GET /getProjectApi , POST /insertProjectApi , DELETE /deleteProjectApi .

![swaggerui](/assets/images/swaggerui.PNG)

Also, integration of swagger open API is pretty painless in spring boot and it lets users try out the APIs within the browser without any installation of any software from the user (sounds pretty convenient and sweet to me)

In this post, I will describe how I integrated swagger open API in Spring boot project.First you need a spring boot project having basic dependcies using Spring Initializr https://start.spring.io/ or you could use this project used in the example [here][Here]


First add the springdoc-openapi-ui dependency to ***pom.xml***:

{% gist 0f069ca7e1350a57600a963d2afae23f %}


Then run the application and check the below url to check open api specification
```
http://localhost:8080/v3/api-docs/
```

You should be able to see something like this

![open-apidocs](/assets/images/open-apidocs.PNG)

You can also add a custom path by adding entry in ***application.properties*** file
```
springdoc.api-docs.path=/api
and now check the url http://localhost:8080/api
```
![custom-open-apidocs](/assets/images/custom-open-apidocs.PNG)


For the web ui,have the same maven dependency in pom.xml and lets customize the ui path by adding the following entries in ***application.properties*** file.

```
springdoc.api-docs.path=/api
springdoc.swagger-ui.path=/swagger
springdoc.swagger-ui.operationsSorter=method
```
Check http://localhost:8080/swagger for web UI.To show you in this example we have a following apis in the controller.

{% gist 181eb58a229e86455f1124d1ab99fa63 %}


So the swagger ui look something like this

![swaggerui](/assets/images/swaggerui.PNG)


Also json docs will be available at http://localhost:8080/api
``` springdoc.swagger-ui.operationsSorter=method ``` sorts the API paths in order of their HTTP methods.

You can try and test the apis from web ui too.
![post-eg-swagger](/assets/images/post-eg-swagger.PNG)
![get-eg-swagger](/assets/images/get-eg-swagger.PNG)

It also shows schema information!

![schema-swagger](/assets/images/schema-swagger.PNG)


Overall this is a much convenient way of setting up documentation for your apis which can be handy in some situations.

That's all folks!

[Here]: https://github.com/shwetarkadam/BooksDocker
