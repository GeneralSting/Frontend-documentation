# Microservices

## Monolith arhitecture

- all components are part of a single unit, single applicaiton

## What are microservices

- arthitecture and an approach for writing software
- applications are broken down into their smallest components, independent from each other
  - lightweight
  - ability to share similar process across multiple apps
  - highly scalable
  - resilient, one parts of app do not impacts one another
  - easy to deploy, `service mesh layer`
  - accessible
  - more open
- tools and technologies that enable microservices
  - Containers, unit of software in which application code is packaged alongside all of the files necessary to make ir run, retaining full functionality
  - Kubernetes, container orhecstration platform that allows for single components within an application to be updated without affecting the rest of the technology stack
  - APIs, responsible for communicating with other applications
  - event streaming, even can be defined as any thing that happens within a microservice service - events form into event streams. Event stream processing allows immediate action to be taken
  - serverless computing, cloud-native development model that allows developers to build and run applications while a cloud provider is responsible for provisioning, maintaining and scaling the server infrastructure

## SOA vs microservices arhitecture

- microservice arhitecture is an evolution of `service-oriented arhitecture` (SOA)
- approach is similar in that they break large, complex applications into smaller components that are easier to work with
- SOA is an enterprise-wide approach to arhitecture, microservices are an implementation strategy within application development teams
