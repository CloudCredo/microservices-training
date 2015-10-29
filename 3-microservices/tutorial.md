## App Version 3
### Microservices

We're going to push a new version of our feedback application to Cloud Foundry

This version of the app has a new feature - you can now ask us questions in real time!

We've added this new feature as a new microservice, which sits alongside the old monolith

To keep things simple we *haven't* added a separate API gateway service - the monolithic
app is doing that job for us. If we were doing this for a production system then we'd
definitely look at breaking that feature out into its own service.

----

## Reconfigure Redis

In the last tutorial you created your own personal Redis instance. But if we
stick with that, you'll only ever see your own feedback and questions in the
app, which isn't very useful!

So we're going to show you an alternative way to connect your Cloud Foundry
apps to a service - by creating a 'user provided' service to inject the
Redis connection details into the apps.

    cf unbind-service feedback feedback-redis

    cf delete-service feedback-redis

    cf create-user-provided-service feedback-redis -p '{"url": "<redis url>"}'

    cf create-user-provided-service questions-redis -p '{"url": "<redis url>"}'

You'll notice that we create both a `feedback-redis` and `questions-redis` service,
but provide the same URL for each. This is because in a true microservices architecture,
we would want to bind our microservices to their own, dedicated, completely separate
database instances. Microservices should be free to communicate with each other, but
that should be done through controlled APIs, not through shared databases.

Just for the purposes of this workshop though, it'd be tricky to set up enough
Redis instances for everyone, so we've bent the rules and stuck to a single instance.

Tip:
`create-user-provided-service` can be abbreviated to `cups`

----

## Push to Cloud Foundry

Next we'll push our microservices. Once the questions app is up, you'll
create a user-provided service which holds its URL. You'll notice in the
application manifest that the feedback app is bound to this service. This
is a simple way to tell the feedback app where to find the questions service.

    cf push questions -f app/manifest.yml

    cf apps

    cf create-user-provided-service questions -p '{"url": "<questions app url>"}'

    cf push feedback -f app/manifest.yml

    cf apps

In a large scale production deployment with many microservice apps, creating
these user-provided services becomes unwieldy. This is where patterns like *service discovery*
come into their own. We're not going to go into that in this workshop, but it's good to know
about if you're thinking about large deployments.

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
3. Use `cf push <your app name> -m 128M --random-route` when you push your microservice to make sure
   it doesn't use too much memory and doesn't collide with any other app routes
4. Set the `MY_MICROSERVICE_URL` env var of the feedback app

    `cf set-env feedback MY_MICROSERVICE_URL http://<your app url>`

    `cf restage feedback`

    This is an alternative approach to using user-provided services to provide microservices
    with the connection URLs they need

5. Watch the output in the `My Microservice` tab of the feedback application


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
