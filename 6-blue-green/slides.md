This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.

----

## As a Cloud Native I can deploy my application with zero downtime

----

Automate everything

Note:

1. Reduce friction
2. Reduce delay
3. Remove human element

----

Continuous Delivery

Note:

1. Reduce inventory of code
2. Release little and often 
3. Increase business agility
3. Reduce risk

----

Concourse.ci

----

Minimise downtime

----

Blue Green

Note:

0. A production application exists an environment. This is the blue environment.
1. Standup an application next to the running application. This is the green application. 
2. Once tests have passed against the new application the router can be switched from blue to green
3. The blue application is now idle

----

Rollback to blue

*Or roll forward*

----

Costs...

Note: 

The return of the paid lunch

----

Architect for costs

----

Missed transactions

Note: 

1. This must be architected for 
2. You may want to leave Blue app running until it has completed all of its work
3. Can use scaleover technique if BlueGreen is too harsh

----

Schema migrations

Note:

Backward and Forward compatible schemas

----

Cloud Foundry Solutions...

----

cf plugins

----

cf autopilot

----

cf scaleover

----

CI of your choice

----

Questions?

----

Over to you...

Note: 

1. Talk about the random routes

----

This content is copyright of CloudCredo. © CloudCredo 2015. All rights reserved.
