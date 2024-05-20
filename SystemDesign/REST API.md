# REST API (RESTful API)

- REST - representational state transfer
- API - application programming interface
- it is an application programming interface (API or web API) that conforms to the constraints of REST arhitectural style and allows for interaction with RESTful web services

## API

- set of definitions and protocols for building and intergrating application software
- referred as a contract between an information provider and an information user - establishing the content required from the consumer (the call) and the content required by the producer (the response)
- API is a mediator between the users or clients and the resources or web services they want to get. It's also a way for an organization to share resources and information while maintaining security, control and authentication

### How do APIs work

- allows to product or service to communicate with other products and services without having to know how they are implemented
- APIs are a simplified way to connect your own infrastructure
  - connects `microservices` application arhitecture through APIs
  - share data with public, public APIs
- APIs let you open up access to your resources while maintaining security and control
  - `API management`
  - `API gateway`

![How API works](https://www.redhat.com/rhdc/managed-files/styles/wysiwyg_full_width/private/API-page-graphic.png?itok=RRsvST-_)

### API gateway

- handles common tasks that are used across a system of API services, such as user authnetication, rate limiting
- API management role
- most basic example: API service accepts a remote request and returns a response
- real life cases:
  - protect APIs from overuse and abuse - rate limiting
  - understand how peaople uses APIs - analytics and monitoring tools
  - in `microservice` arhitecture single request can require dozens of different application parts
  - adding new API service and retiring others requires need for clients to still find services in the same place, location
- offers client a simple and dependable experience in the face of all complexity - API gateway decouples client interface from backend implementation
  - when client makes request, API gateway breaks it into multiple requests, routes them to the right places, produces response, and keeps track of everything

### API release policies

- private
  - API us only for use internally
  - most control over API
- partner
  - shared with specific business partners
- public
  - available to everyone
  - allows third parties to develop apps that interact with your API

### Remote APIs

- interact through a communications network, resource being manipulated by the API are somewhere outside the computer making the request
- most APIs are designed based on web standards
- typically use HTTP for request messages and provide a definition of the structure of response messages
  - response messages takes the form of an XML or JSON file

### Webhooks

- webhook is an HTTP-based callback funciton that allows lightweight, event-driven communcation betweeon 2 APIs
  - often referred to as everse APIs or push APIs because they put the responsibility of communcation on the server, rather than the client
  - webhooks are not APIs, they work together - application must have an API to use a webhook

## REST

- REST - Representational State Transfer
  - it's not protocol, it is arhitectural style
  - viewed as faster alternative in web-based scenarios
  - lightweight
  - set of guidelines that offers fexible implementation
  - web APIs that adhere to the REST arhitectural constraints are caled RESTful APIs
  - APIs are RESTful as long as they comply with the 6 guiding constrains of a RESTful system:
    1. client-server arhitecture, handles request through HTTP
    2. statelessness, no client content is stored on the server between requests, session state is helded on client
    3. cacheability
    4. layered-system, client-server interactions can be mediated by additional layers, load balacing, shared caches or security
    5. code on demand (optional), servers can extend the functionality of client by transferring executable code
    6. uniform interface, 4 facets
    - resource idenitfication in requests, resources are identified in requests and are separate from the representations returned to the client
    - resource manipulation through representations, clients receive files that represent resources, these representations must have enought information to allow modification or deletion
    - self-descriptive messages, each message returned to a client contains enough information to describe how the client should process the information
    - hypermedia as the endgine of application state, after accessing a resource, REST client should be able to discover through hyperlinks all other actions that are currently available

### SOAP vs REST

- REST and SOAP are 2 different approaches to online data transmission
- both define how to build APIs

#### SOAP

- SOAP - Simple Object Access Protocol

  - standard protocol designed so that applications built with different languages and on different platforms could communicate
  - it is protocol so it means that imposes built-in rules that increase its complexity and overhead, which can lead to longer page times
  - use XML for message format
  - requests received through HTTP, SMTP, TCP...
  - makes it easier for apps running in different environments or written in different langauges to share information
  - not cachable by a browser
