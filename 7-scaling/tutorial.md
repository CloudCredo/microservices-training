## App Version 7
### Scaling

We're going to push a new version of our feedback application to Cloud Foundry.

This version has a new feature - it displays the amount of traffic being received by each of our
asynchronous workers.

Then we can scale our workers and handle more load!

## Push to Cloud Foundry

Let's push our apps to Cloud Foundry to prove that it works:

    cf push -f app/manifest.yml

    cf apps

----

## Did it work?

    name                requested state   instances   memory   disk   urls
    feedback            started           1/1         356M     1G     feedback-[unique-name].cfapps.io
    questions           started           1/1         356M     1G     questions-[unique-name].cfapps.io
    request-data-api    started           1/1         128M     1G     request-data-api-[unique-name].cfapps.io
    request-data-worker started           2/2         128M     1G

Browse to http://feedback-[unique-name].cfapps.io

----

## Scaling horizontally

1. We now have two instances of our `request-data-worker` app. Note the setting in
`app/manifest.yml` that controls this
2. Note the number of requests per second each worker is handling on the chart in the UI
3. Horizontally scale the worker app to 4 instances: `cf scale request-data-worker -i 4`
4. What happens to the number of requests each worker is receiving?
5. Now we can handle more load!

----

## Scaling vertically

We can also scale our apps vertically by allocating them more memory and/or disk.
Essentially giving them a bigger slice of Cloud Foundry to run on.

1. Note the settings that control the default memory and disk settings for each app
in `app/manifest.yml`
2. Give the `request-data-api` application a bit more memory to play with:
 `cf scale request-data-api -m 256M`

----

## Scaling bonus task!

Back in session 3 you wrote your own microservice. What happens if you scale it?
It might be hard to tell if it always responds with the same output. Try returning
the unique instance number from your microservice's `CF_INSTANCE_INDEX`
environment variable.


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
