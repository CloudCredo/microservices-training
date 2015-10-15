## App Version 3
### Microservices

We're going to push a new version of our feedback application to Cloud Foundry

This version of the app has a new feature - you can now ask us questions in real time!

We've added this new feature as a new microservice, which sits alongside the old monolith

To keep things simple we *haven't* added a separate API gateway service - the monolithic
app is doing that job for us. If we were doing this for a production system then we'd definitely look at breaking that feature out into its own service.

----

## Push to Cloud Foundry
    cf unbind-service feedback feedback-redis

    cf delete-service feedback-redis

    cf create-user-provided-service feedback-redis -p '{"url": "<redis url>"}'

    cf create-user-provided-service questions-redis -p '{"url": "<redis url>"}'

    cf push questions -f app/manifest.yml

    cf apps

    cf create-user-provided-service questions -p '{"url": "<questions app url>"}'

    cf push feedback -f app/manifest.yml

    cf apps

Tip:

`create-user-provided-service` can be abbreviated to `cups`

----

## Did it work?

    name       requested state   instances   memory   disk   urls
    feedback   started           1/1         356M     1G     feedback-[unique-name].cfapps.io
    questions  started           1/1         356M     1G     questions-[unique-name].cfapps.io

Browse to http://feedback-[unique-name].cfapps.io

----

## Microservice bonus task!

Write and push a new microservice using a supported buildpack

1. Make it listen on the port number injected by Cloud Foundry via the PORT environment variable
2. Make it respond to HTTP GET requests on `/my-microservice`
3. Use `cf push -m 128M --random-route` when you push your microservice to make sure it doesn't
use too much memory and doesn't collide with any other app routes
4. Set the `MY_MICROSERVICE_URL` env var of the feedback app

    `cf set-env feedback MY_MICROSERVICE_URL http://<your app url>`

    `cf restage feedback`

    This is an alternative approach to using user-provided services to provide microservices
    with the connection URLs they need

5. Watch the output in the `My Microservice` tab of the feedback application


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
