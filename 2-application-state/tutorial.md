## 2 Application State

1. Create a new Redis service.
2. `cf push` the test application and get it working with your new service.
3. Store some data in the application, restart the app to see the data is still present.

##### Tips: 

1. The name of the service you create must match the service name the application
expects! See the application manifest for more context.
2. Take a look at the `cf env` command. Run this against your test application
and see what credentials Cloud Foundry has injected into your application for
services.

#### Bonus step:

Create and register a user defined services and customise the application to
use it. Your service could be something as simple as a basic Spring Boot or
Sinatra application.


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
