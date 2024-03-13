---
layout: post
title: What is Backstage? 
tags: SoftwareEngineering
image: https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage.jpg
lang: en
---

As the software we are developing grows larger, more microservices are created, more individuals work simultaneously on the software, and transferring knowledge between teams becomes harder and more complex.

Let me give you a real-world example; in the company I work for, each service publishes its APIs in a tool called Swagger. Swagger is a web-based tool that displays the schemas of APIs and allows you to call them right from there. Over time, the number of microservices in our organization increased, leading to a higher number of Swagger panels for each of these applications. You had to keep track of the Swagger addresses for all these services or ask their developers. The main problem arose when you didn't even know who the developer of the service you were interested in was or which team they belonged to.

As seen in this example, the missing link in this story is the lack of a suitable platform for knowledge transfer between teams.

So what happened? One of the creative programmers in the organization took the initiative to create a simple HTML panel where all the Swagger addresses of the services were listed.

Let me raise another requirement; suppose one of your services encounters an issue. You know that this service interacts with several other services and you need to see if these services developed by other teams have recently undergone any changes or not. Or imagine you want to view the documentation related to your service or other services in one centralized location.

All of these make you have to log in to thousands of panels throughout the day and gather various pieces of information from different tools to advance an issue, provided that you have the necessary access for this matter.

Imagine if there was a panel that provided all this information. How much simpler life would be? Backstage is precisely developed for this purpose.

## What is Backstage?
So what is Backstage? Exactly, Backstage is a solution to the aforementioned problem. Developers at Spotify, just like us, faced the above-mentioned challenges and, therefore, needed what they termed as a developer portal to facilitate and expedite knowledge transfer. For this reason, they developed Backstage and when they saw that it's not such a strange thing technologically but rather a very effective solution, they decided to open-source it and let developers from other companies also benefit from it.

So, Backstage is a self-declared tool (meaning developers help enrich it with information) with a bit of automation thrown in.

To put it more precisely, in Backstage, you specify your service in a way (which I will mention later), define its APIs, share relevant links to your service, specify its dependencies (and thousands of other tasks like these), and Backstage takes responsibility for displaying, categorizing, updating changed data, and so on.

In the image below, you can see an example of the service list in Backstage:
 
![Link to Image](https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/components.png)

For each of the services, we can display information such as dependencies on other services, a list of important document links and merge requests, programming language, and whatever else we want.

In the image below, you can see the minimal representation of service information in Backstage:

![Link to Image](https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/component.webp)

One of the main features of Backstage is that you can install various plugins on it and enrich the information related to each of the services in Backstage.

For example, the image below shows an example of the GitLab plugin displaying information related to one of the services: 


![Link to Image](https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/gitlab.webp)

And finally, if I want to connect the end of my discussions to the beginning, if you remember I talked about sharing APIs in the form of Swagger, in Backstage, you can define APIs for each service. The image below shows an example of the API defined in one of the services: 

![Link to Image](https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage/api.webp)

## Conclusion
In general, if everything is organized in your organization and you are living happily but having multiple tabs in your browser, numerous authentications every day, and such annoyances bother your developers, or if knowledge transfer between developers has become difficult and you are looking for a tool to document everything in one shared panel, Backstage can help you.
