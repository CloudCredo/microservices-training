## 6. Blue Green Deployment

In this tutorial we will be working on the questions application only.

1. Open `./app/questions/manifest.yml` and add a route for your application. This
route needs to be a unique string. If you push an application with the same
route as an existing Cloud Foundry application then `cf push` will fail.
2. Push the questions application only.
2. Install the Autopilot cli plug-in. The command to install a
plugin is `cf install-plugin 'plugin-name' -r 'CF-Community'`
3. Re-push questions and see your application experience zero downtime. `cf
zero-downtime-deploy questions -f ./app/questions/manifest.yml`

##### Tip
Try running [siege](https://www.joedog.org/articles-tuning/) or
[JMeter](http://jmeter.apache.org/) against one of the of application endpoints
as you attempt a blue green deployment to discover the actual dropped requests

## Bonus step:

Grab the [concourse.ci](https://github.com/concourse/concourse) vagrant image
and setup a build pipeline to deploy the test application in to your
CloudFoundry account.


This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
