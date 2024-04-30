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
