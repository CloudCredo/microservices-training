## 4 Distributed Tracing

1. Push the demo applications using `cf push -f app/manifest.yml`.
2. Send some requests into the application.
3. Check the logs for the system applications.
4. Ensure that the span and trace ids for the request flow through all logs for
all requests.

##### Tip:
1. Use `cf logs` to grab the logs from Cloud Foundry.

#### Bonus step:

Reconfigure your application to use a Papertrail account to aggregate your
Microservices application logs.


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
