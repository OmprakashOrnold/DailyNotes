# REST 
## What is REST ?

### The **REST** stands for 
**REpresentational**
**State** 
**Transfer**

- **State** means data
- **REpresentational** means formats (such as xml, json, yaml, html, etc)
- **Transfer** means carry data between consumer and provider using HTTP protocol

## REST – Architecture

![Screenshot 2024-04-30 091301](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/64ee65fe-4aef-4b27-aebc-d48cf2591450)

## REST Architectural Constraints

An API that has following constraints is known as RESTful API:
- **Client-server architecture**: The client is the front-end and the server is the backend of the service. It is important to note that both of these entities are 
independent of each other.
- **Stateless**: No data should be stored on the server during the processing of the 
request transfer. The state of the session should be saved at the client’s end.
- **Cacheable**: The client should have the ability to store responses in a cache. This 
greatly improves the performance of the API.
- **Uniform Interface**: This constraint indicates a generic interface to manage all the 
interactions between the client and server in a unified way, which simplifies and 
decouples the architecture. 
- **Layered System**: The server can have multiple layers for implementation. This 
layered architecture helps to improve scalability by enabling load balancing.
- **Code on Demand**: This constraint is optional. This constraint indicates that the 
functionality of the client applications can be extended at runtime by allowing a 
code download from the server and executing the code.

## REST Key Concepts
- Resource
- Sub-resource
- URI
- HTTP Methods
- HTTP Status Codes

## REST - Resource
• The fundamental concept of a REST-based system is the resource. A resource is anything you want 
to expose to the outside world, through your application

![Screenshot 2024-04-30 093404](https://github.com/OmprakashOrnold/DailyNotes/assets/36263846/bef25fd0-f0c2-40c9-925c-a1b106d6e0eb)


## URI - Uniform Resource Identifier
- The resource an be identified by  a **Uniform Resource Identifier (URI)**. For webbased systems,
HTTP is the most commonly used protocol for communicating 
with external systems. You can identify a unique resource using a URI.
- Consider, we are developing a simple blog application and you can define URIs for  a blog Post resource

- **GET**  http://localhost:8080/api/posts/ Returns a list of all posts
- **GET**  http://localhost:8080/api/posts/2  Returns a post whose ID is 2
- **POST**  http://localhost:8080/api/posts/  Creates a new Post resource
- **PUT**  http://localhost:8080/api/posts/2  Updates a POST resource whose ID is 2
- **DELETE**  http://localhost:8080/api/posts/2 Deletes a POST resource whose ID is 2****

## REST - Sub-resource
- In REST, the relationships are often modeled by a sub-resource. Use 
the following pattern for sub-resources.

      GET /{resource}/{resource-id}/{sub-resource}
      GET /{resource}/{resource-id}/{sub-resource}/{sub-resource-id}
      POST /{resource}/{resource-id}/{sub-resource}
      
      GET /{post}/{post-id}/{comments}
      GET /{post}/{post-id}/{comments}/{comment-id}
      POST /{post}/{post-id}/{comments

## HTTP Methods
| HTTP Method | Description                                | Example                                |
|-------------|--------------------------------------------|----------------------------------------|
| GET         | To get a all resource  | `http://localhost:8080/api/users`     |
| GET         |  To get a  single resource  | `http://localhost:8080/api/users/1`   |
| POST        | To create a new resource                  | `http://localhost:8080/api/users`     |
| PUT         | To update an existing resource            | `http://localhost:8080/api/users/1`   |
| DELETE      | To delete a collection or a single resource | `http://localhost:8080/api/users/`  |


## HTTP Status Code
### Informational responses (100–199):
| Status Code | Explanation                                              |
|-------------|----------------------------------------------------------|
| 100         | Continue - The server has received the request headers and the client should proceed to send the request body. |
| 101         | Switching Protocols - The requester has asked the server to switch protocols. |

### Successful responses (200–299):
| Status Code | Explanation                                              |
|-------------|----------------------------------------------------------|
| 200         | OK - The request has succeeded.                          |
| 201         | Created - The request has been fulfilled and a new resource has been created. |
| 204         | No Content - The server successfully processed the request but there is no content to return. |

### Redirection messages (300–399):
| Status Code | Explanation                                              |
|-------------|----------------------------------------------------------|
| 300         | Multiple Choices - The request has more than one possible response. |
| 301         | Moved Permanently - The requested resource has been permanently moved to a new URL. |
| 302         | Found - The requested resource resides temporarily under a different URI. |
| 304         | Not Modified - Indicates that the resource has not been modified since the version specified by the request headers If-Modified-Since or If-None-Match. |

### Client error responses (400–499):
| Status Code | Explanation                                              |
|-------------|----------------------------------------------------------|
| 400         | Bad Request - The server cannot process the request due to client error. |
| 401         | Unauthorized - The client must authenticate itself to get the requested response. |
| 403         | Forbidden - The server understood the request but refuses to authorize it. |
| 404         | Not Found - The requested resource could not be found on the server. |
| 405         | Method Not Allowed - The method received in the request-line is known by the origin server but not supported by the target resource. |

### Server error responses (500–599):
| Status Code | Explanation                                              |
|-------------|----------------------------------------------------------|
| 500         | Internal Server Error - The server encountered an unexpected condition that prevented it from fulfilling the request. |
| 501         | Not Implemented - The server does not support the functionality required to fulfill the request. |
| 502         | Bad Gateway - The server, while acting as a gateway or proxy, received an invalid response from the upstream server it accessed in attempting to fulfill the request. |
| 503         | Service Unavailable - The server is currently unable to handle the request due to temporary overloading or maintenance of the server. |
| 504         | Gateway Timeout - The server, while acting as a gateway or proxy, did not receive a timely response from the upstream server specified by the URI or some other auxiliary server it needed to access in order to complete the request. |


