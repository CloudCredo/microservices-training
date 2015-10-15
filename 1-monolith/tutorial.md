## App Version 1
### The Monolith

We're going to have a go at pushing an application to Cloud Foundry

The application is a monolith - it *doesn't* adhere to the 12 Factor principles!

Its state is stored completely in memory

Over the course of the day we're going to fix this :)

----

## Create a Cloud Foundry account

Create a free Cloud Foundry account at [http://run.pivotal.io/]

We've provided the CF CLI for you on the USB stick, so you won't need to download it
again here

Follow the steps to log in to your Cloud Foundry account using the CLI

----

## Orgs and Spaces

Once you're logged in, you'll find you already have an org and a space (called `development`)
set up for you

Running `cf target` will show you that your CLI is targeting your org and space already.

----

## Push to Cloud Foundry

Let's push our monolithic app to Cloud Foundry to prove that it works

    cd app

    cf push -f manifest.yml

    cf apps

----

## Did it work?

    name       requested state   instances   memory   disk   urls
    feedback   started           1/1         356M     1G     feedback-[unique-name].cfapps.io

Browse to http://feedback-[unique-name].cfapps.io

Tell us how you feel!

----

## Application manifests

We said `cf push -f manifest.yml` - so what's this manifest thing?

There are three ways to tell Cloud Foundry about your app when you push it:

1. Do nothing. Run `cf push <app name>` with no arguments and let the platform figure out
some sensible defaults
2. Use `cf push <app name> <args>` to specify some more information. Try running
`cf help push` to see what kind of properties you can set
3. Use an application manifest

We're taking the manifest approach today. As we go through the later tutorials, keep taking
a look back at `manifest.yml` and see how it changes.

Tip: Running `cf push -f manifest.yml` pushes *all* the apps defined in the manifest, one
after another. To push just one app from the manifest, run `cf push <app name> -f manifest.yml`.

----

## Check out the available buildpacks

Check out all the available buildpacks:

    cf buildpacks
    
Lots of supported languages to play with!    
    
----    

## Cloud Foundry Introduction bonus task!

Write and push an application using a supported buildpack that prints its environment variables to stdout.
See what Cloud Foundry gives you by default.

    cf push [your app name] -i 128M
    cf logs --recent [your app name]

or for JVM languages

    cf push [your app name] -p [path/to/your-executable-jar.jar] -i 128M

Tip: We're using `-i 128M` to tell Cloud Foundry to allocate 128Mb of RAM to your app. Maybe
you'll need more or less, so feel free to choose a more suitable value.

----


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
