+++
type = "post"
categories = ["OpenShift"]
tags = ["openshift"]
author = "Andy Downs"
date = "2017-05-09T07:36:12+01:00"
title = "Openshift Project Granularity"
draft = true

+++

I have been lucky to spend some time in the new [Red Hat Innovation Lab](https://www.redhat.com/en/open-innovation-labs) in London this week, helping out where I can. One of the things I was asked to do was to talk about the options of project granularity within OpenShift. Basically to list the pros and cons of the main ways I've seen customers doing this.

A quick word of warning, I am writing this based on OpenShift Container Platform 3.5 (Origin 1.5), there is a new feature in tech preview called [NetworkPolicy](https://blog.openshift.com/whats-new-in-openshift-3-5-network-policy-tech-preview/). This will affect the decisions below and I will try to point out which ones.

## What is a Project?  

First off it is worth defining what a project is. The [official docs state](https://docs.openshift.com/container-platform/3.5/architecture/core_concepts/projects_and_users.html#projects) :

>A project is a Kubernetes namespace with additional annotations, and is the central vehicle by which access to resources for regular users is managed. A project allows a community of users to organize and manage their content in isolation from other communities. Users must be given access to projects by administrators, or if allowed to create projects, automatically have access to their own projects.

In a nutshell this means that we can RBAC a project and use the multi-tenant network plugin to isolate traffic within the bounds of a project. NetworkPolicy gives more fine grained isolation.

## Your "Application"

For the purpose of talking about granularity the scope is one application, so would be replicated for each application you are builing. The example I am going to use is an application made up of a number of distinct services, or micro-services if you will. Each service has an API, some are restful, some are event driven. This is mainly to show the things to consider with different protocols. At the moment these services are only used by one application but in the future it is probable that some services will be used by other applications.

### One project per Service

This is pretty self explanatory, each service that makes up the application is deployed into it's own project.

**Pros** :

* A service is owned by a team and we can limit access to the project to that team.
* Resouce limits and quotas are set for how this service runs.
* Network Isolation of all the parts that make up the service.
* Clearer seperation of concerns


**Cons** :

* Project sprawl - Lots of projects for each service (May have a Test, UAT, Prod etc projects for each service)
* Network protocols - Into a project it is HTTP(S) or SNI based protocols.
* Creating a route to a application to allow services in other projects to communicate exposes the service "outside" of OpenShift. This may be a service that is only ever going to be used by internal services.

**Mitigations**

* With the multi-tenant network plugin we can join projects together to get round protocols. NetworkPolicy will allow more fine grained control as well.
* [Router Sharding](https://docs.openshift.com/container-platform/3.3/architecture/core_concepts/routes.html#router-sharding) allows control of ingress traffic to specific routers, so we could have an "internal" router that doesn't expose internal services to the outside world.

### One project per "Environment"

This is following a more traditional approach in that you create a project that represents a dev, test, UAT, production etc for each application.

**Pros** :

* Network is "flat" in a project so each service can talk to each other, no worry about protocols passing the routing boundary.
* Simplicity of projects: Obvious what the project is for and helps simplify pipelines/access control.
* Lack of complications, the learning curve for some of the mitigations can be high along with everything else. This method has less "moving" parts and could argueably be more familiar.


**Cons** :

* If a service is owned by a team the RBAC is for the project, therefore a team could touch a service that doesn't belong to them.
* If a service is used by another application then which project does it belong in?
* Resource limits and quotas are for the whole application and each service may scale differently.
* If a service has it's own datasource deployed in the project, with the right information another service could talk direct to it.


**Mitigations**

* When a service is reused outside one application it could be moved to it's own project. Effectivaly becoming it's own application.
* Again [NetworkPolicy](https://kubernetes.io/docs/concepts/services-networking/networkpolicies/ ) can help with separation of services.

## Conclusion

There isn't a right or wrong way to do this, it really is what fits your team and application. Personally I think starting out, the one project per "environment" (per application) is probably the best way to start. This is really down to your definition of an application and when a service becomes an application in it's own right. The service/application definition is a little bit of semantics, but
