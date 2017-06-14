# Final check
Easy way to monitor your network API calls

# Philosophy




# Protocol
### content of the http log
When making an http request, user sends input information `method, headers, ...` then they expect to receive output information `requested payload, status, ...`, So Final check requires all logs to have these key pieces of information. 

Below is an interface with all required attributes in order for a log to be considered valid.
```javascript
{ 
  url: string,
  request: { 
     payload: any, // governed by the request content-type header
     method: enum, // known http methods
     headers: { [key: string]: string | number },
     host: string, // url ip of the server that provides the response
     clientIp: string // ip of the client that initiate the http request
  }
  respone: { 
     payload: any, // governed by the response content-type header
     headers: { [key: string]: string | number },
     status: string
  }
  latency: number 
 }
```
