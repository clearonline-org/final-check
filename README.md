# Final check
Easy way to monitor your network API calls

# End Goal
* Three parties **System**(HTTP Accessible), **Good User**, and **Bad User**
* We want to find out whether the **System** is providing *correct information* to the **Good User**
* We want to find out whether the **System** is providing *right error messages* to the **Bad User**

# Philosophy
Most of software developers strive to write code that provide value to their *intended* end users. In most cases, this works well for *offline applications* because the developer don't have to worry about these *unintended* users corrupting their apps. And this "corruption" is very frequent for network application.

In a typical network application, the user sends some information `in a form of commands` to the application hosting computer, then the hosting computer sends back some other information. During this interaction, the hope is that this user is a good user and will send information that conforms to what the hosted application expects, and that the hosted application will sastify the user's expectations. However, in reality things always do get out of hand and that is why Monitoring systems exist.

# Experience
I created a messenger robot using the serverless technology `AWS lambda`, then at some point after deployment, it started sending multiple responses everytime a user would send one message. I tried to look into cloudwatch, but their logs didn't reveal anything abnormal, so i shut down the robot and create an http logger whose sole purpose was to show me each request that `AWS lambda` receives and the response it returns.

After finishing the *http logger service*, i turned the robot on and when user started using it again, it worked fine! Unfortunately, till now, the robot has not made that same mistake again, so i haven't really used the looger to catch anything suspicious. But having this logger gave me the confidence that the robot will not do any unwanted action without my knowledge!

NOTE:
* corrupting = sending fake data to the real user on behalf of the app.
* corrupting = trying to request data from the app, that do not belong to them

# Design
The name **Final check** was chosen because the *project's intended purpose* is, to provide clarity on how the developer's final product is performing. I.e. monitor what the app does after all development work is complete.

This project is about monitoring **http requests** because of past expiriences (through work and personal projects). I.e. this is the place where most of developers have trouble knowing what is going on (and it always feels good if *You know why a software is malfunctioning* just in case the boss asks why).

This project uses the *microservice* architecture because of it has been proven to be scalable and cost effective.

This project has three parts:
* [The Log collecting plugins](https://github.com/clearonline-org/final-check/blob/master/LOGGER_PLUGINS.md): middleware/addons that a developer integrate into their app.
* [The frontend dashboard](https://github.com/clearonline-org/final-check/blob/master/FRONTEND.md): where developers view the logs and configure notifications.
* [The backend](https://github.com/clearonline-org/final-check/blob/master/BACKEND.md): a list of serverless functions that *store* and *analyse* the logs

# Protocol
### content of the http log
When making an http request, user sends input information `method, headers, ...` then they expect to receive output information `requested payload, status, ...`, So Final check requires all logs to have these key pieces of information. 

Below is an interface with all required attributes in order for a log to be considered valid.
```typescript
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
     statusCode: number,
     status: string // the status message ex: OK, 200 OK, ...
  }
  latency: number 
}
```
