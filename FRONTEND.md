# Frontend

## 1. Final Check os
os for *Open Source*

This is a **Final Check** implementation using `Angular 2` frontend framework and `AWS Cognito` authentication system.

It has a simple Application data model
* Application
```javascript
// application: represent the monitored system
{
  id: string,
  name: string,
  description: string,
  appcode: string // used by the logging systems when sending logs to Final Check backend
}
```

* Applicaton Summary
```javascript
// summary
{
  appId: string,
  appName: string,
  OK: number, // number of logs with status code of 200
  ERROR: number, // number of logs with status code of 500
  OTHER: number // number of logs with status code other than 200 or 500
}
```

* ApiRequest
```javascript
// api-request: represent the http request log (Final Check log)
{
  id: string,
  url: string,
  request: json,
  response: json,
  latency: number
}
```

* ApiRequest Origin
```javascript
// request-origin: used to display all call origins on a world map
{
  ip: string,
  ipOwner: string,
  long: string,
  lat: string,
  requestCount: number
}
```

More Information can be found at the [Github repo](https://github.com/clearonline-org/final-check-os)
