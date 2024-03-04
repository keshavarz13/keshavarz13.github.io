---
layout: post
title: What is Backstage and how to use it? 
tags: SoftwareEngineering
image: https://raw.githubusercontent.com/keshavarz13/keshavarz13.github.io/main/images/backstage.jpg
lang: en
---


As part of the software development process, where teams and individuals with various roles and multiple processes within an organization are involved, sharing information and knowledge increasingly becomes complex and even unmanageable. 

For example, it often happens that one of your services encounters an issue. You know that this service is connected to several other services, and you need to see whether other services developed by other teams have recently undergone any changes. Or, for another example, you may want to view documents related to your service or other services in one centralized location. Or imagine wanting to view, for instance, the Swagger documentation of a service, among thousands of similar tasks that arise during our day. To solve such issues, you often need access to multiple different panels. Moreover, if you have the necessary access to view this information (especially if your organization does not use a mono repository), you need a comprehensive panel that contains all this information. Since enterprise software has evolved into its present form, the idea of having such a comprehensive panel has always been a fantasy but an enticing one.

## What is Backstage?

Backstage is an open-source platform for building developer portals developed by Spotify developers as the magical panel mentioned above. Backstage integrates all your infrastructure tools, services, and documentation to create an end-to-end development environment seamlessly. How does this panel work? Backstage works by having all services in their repositories write their service specifications in a defined format (a YAML file). Once you register this file in Backstage, the magic begins. Dependencies, APIs, related links, pipelines, contributors, and more are all displayed in the Backstage panel. To update it, you just need to keep your YAML file up-to-date in your repository, and the Backstage panel periodically checks and keeps itself updated. In general, Backstage aims to improve onboarding processes, reduce the number of questions and distractions from other team members, and enhance other similar aspects. To see if Backstage has had a positive impact on your organization, you just need to see how much things have improved in these areas.


## How to Set Up Backstage?

To install Backstage, you need to have NodeJS, Yarn, Docker, and Git installed. Then run the following command:

```sh
npx @backstage/create-app@latest
```

Then run the following commands too:

```sh
cd your-backstage-directory
yarn dev
```

Congratulations, now you just need to open localhost:3000 in your browser to bring up Backstage for the first time on your system.

In general, I will list below the things you should do to configure your backstage in the best way:

<b>
1: Setting up the postgres database for your backstage
</b>

  This will cause your changes to be saved on the database, by default sqlite is used in the backstage, which we all know its problems :)

  To do this, you can use the [guide](https://backstage.io/docs/getting-started/configuration#install-and-configure-postgresql)


<b>
2: Integrating with your organization's gitlab (self hosted gitlab)
</b>

  doing this allows the backstage to read the definition of your services from your organization's git, can update it periodically, and information such as requests, contributors, issues, language Have programming and information like this from each of your repositories in the backstage.

  To do this, there is a proper plugin that you can easily use by using the [guide](https://github.com/immobiliare/backstage-plugin-gitlab).


<b>
3: Deploying and Docking the application
</b>

  There are several methods for this, such as separating slow and front-end, such as using a multi-stage docker file and other such methods, for this, there is no better place than [Backstage official document](https://backstage. io/docs/deployment/) cannot help you.


### Adding a service to Backstage:
To add a service behind the scenes, follow two steps.

#### Step 1: Adding the YAML file for the service in the Git repository:
To add a new service, create a YAML file in the service repository and fill in the service specifications.

```yaml
apiVersion: backstage.io/v1alpha1
kind: Component
metadata:
  name: your-service-name # In this section, write the name of your service, for example, report-center and...
  description: some shit about your service # In this section, you can explain a little about what this service is for.
  links: # In this section, you can add links related to your service, such as Grafana, Hangfire, Confluence, etc.
    - url: https://some.link/ 
      title: some-link 
      icon: some-material-icon # For this part, you can use material UI icons, for example, dashboard, etc. To be able to use the right icon, you can use this link: https://fonts.google.com/icons
    - url: https://another.link/
      title: backstage-official-website
      icon: some-material-icon
spec:
  type: service 
  lifecycle: Production # you can use Production/Development
  owner: platform # write your team name. (Choose you team from this file: )
  providesApis: # Names of API resources provided by your service and defined below (you can have any number of APIs)
    - openapi-example 
    - proto-example
  consumesApis: # Names of API resources provided by another service and defined in the entities.yaml of that service(you can have any number of APIs)
    - another-service-api-proto 

--- 
apiVersion: backstage.io/v1alpha1
kind: API
metadata:
  name: openapi-example 
  description: your openapi api information
spec:
  type: openapi
  lifecycle: production
  owner: platform
  dependsOn: # The names of the components you have dependencies on (if that component exists in the backstage, the name you enter must be the same as its name in the backstage)
    - sql-serevr
    - envoy
    - report-center
  definition:
    $text: https://address.swagger.json/ # Add address of your swagger json for example https://foo.bar/swagger/v1/swagger.json
--- 
apiVersion: backstage.io/v1alpha1
kind: API
metadata:
  name: grpc-example
  description: your proto api information
spec:
  type: grpc
  lifecycle: production
  owner: platform
  definition:
    $text: https://gitlab.your.company/rout/to/your/proto-file.proto
```

#### Step 2: Register your file in Backstage:
1. Go to Backstage and click "+ create".
2. Click on "Register Existing Component".
3. Enter the address of your YAML file and click "Analyze".
4. After reviewing, confirm the added components.
