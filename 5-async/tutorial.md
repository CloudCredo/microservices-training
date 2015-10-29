## App Version 5
### Asynchronous Communication

We're going to push a new version of our feedback application to Cloud Foundry

This version of the app has a new feature - you can now see stats of the underlying
requests that are flowing through our API

We've added this new feature as a new microservice

The `feedback` app publishes API call metadata to a queue in Redis. The `request-data-worker` app consumes from the queue,
processes the messages, then stores the results back in Redis. The `request-data-api` app serves those results up so we
can see them in the web app.

Although this is a very simple example, it's a good use of a queue. We wouldn't want our
API to be slowed down by having to wait for the metadata collector to process the data
and return a response

Instead we've decoupled the two concerns using Redis as a very quick message broker

----

## Push to Cloud Foundry

Let's push our apps to Cloud Foundry to prove that it works

    cf cups async-redis -p '{"url": "<redis url>"}'

    cf push request-data-api -f app/manifest.yml

    cf cups request-data -p '{"url": "<request-data-api app url>"}'

    cf push -f app/manifest.yml

    cf apps

----

## Did it work?

    name                requested state   instances   memory   disk   urls
    feedback            started           1/1         356M     1G     feedback-[unique-name].cfapps.io
    questions           started           1/1         356M     1G     questions-[unique-name].cfapps.io
    request-data-api    started           1/1         128M     1G     request-data-api-[unique-name].cfapps.io
    request-data-worker started           1/1         128M     1G

Browse to http://feedback-[unique-name].cfapps.io

----

## Things to note

1. `request-data-worker` in the `cf apps` list has no URL. It's a worker - it doesn't need one!
Check out the setting for this in `app/manifest.yml`
2. We've written our `request-data` apps in Ruby - did you notice the different buildpack output from your `cf push`?
We now have Java apps talking to Ruby apps. Cloud Foundry buildpacks let you pick the right
language for the job.

----

## Asynchronous bonus task!

You've seen an example of asynchronous services which communicate via
a Redis queue.

Write and push two new new microservices using a supported buildpack.

The first app should publish messages to both a Redis queue and a Redis topic.
Make sure you can tell the messages apart from each other. You could publish
the value of an incrementing counter, for example.

The second app should consume the messages from both the queue and the topic
and log them out. Make sure you can tell from the logs which are coming from
the queue and which are coming from the topic.

Once you've got this working, try scaling the number of instances of your
consumer app to 2 or more:

    cf scale <consumer app> -i 2

What happens to the messages you receive? Check in the logs to see which
instances are consuming which messages.


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
