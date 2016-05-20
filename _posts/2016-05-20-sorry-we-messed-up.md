---
layout: post
author: shamiksharma
title: Sorry, we messed up
description: Yesterday we unintentionally inundated many of your phones with notifications.  We messed up and owe you an explanation of what happened and what we are doing to ensure it doesn’t happen again.
---

Yesterday we unintentionally inundated many of your phones with notifications.  We messed up and owe you an explanation of what happened and what we are doing to ensure it doesn’t happen again.

#####What happened

On Thursday, May 19, at around 2:00 pm, the notifications team updated our fleet of notification servers with a code change. It took about 3 minutes for the deployment systems to update all our notification servers with the change.

Within minutes of the code-push, our users, including several employees started reporting that they were getting bombarded with notifications, unrelated to their interactions with Myntra.  The team immediately stopped our notification systems and started to troubleshoot. However, within that short period, a lot of notifications had already been sent.  We did cancel a lot of the notifications that were en-route, but unfortunately by then a lot of our customers had already received them.

#####Why it happened

After shutting down the notification sending systems, the team worked on reviewing why the error had occurred. We realized that the problem was not with the new code base - which had been tested independently -  but with how it was deployed. 

Notification systems require a set of  “transformations” to a message before it is sent - for example, adding the recipient’s name inside the message, adding the list of users to whom the message should be sent etc. Each of these transformations is done by a set of processes which do their part and then put the message back in a queue for the next set of processes to take up.  The new code had a “schema change” - the list of recipients was now expected to be in a new field called “userId” rather than “recipient”.  

When we deployed our new code, there was a short  period (2 min 37 sec) when the new code was active while notifications created by the older code were still being processed. This led to a “race condition” - the old code had already added the recipient in the old field (“recipients”)  while the new code was expecting it in the new field (“userId”) and upon not finding a userId, left it blank.  Defensive code should have been written for this case, but was missed.  

Notification messages that went through the system during this intermediate state, became untargeted notifications (ie. did not have any userids). This resulted in them being broadcast to a very large set of users. 

#####What we have learnt

There were several causes of the problem - a shortcoming in the deployment model of our notification systems - all incoming notifications should be stopped and older notifications should be flushed out before a new codebase is deployed.   We should also have had more stringent checks in the code -  notifications missing a recipient list should be held back and subject to more checks and the number of notifications that any user can get in a short time-period should be more stringently capped.  Over the last 24 hours, we have already added some of these checks and will be adding more.

The last several hours have been a humbling period for us and we deeply regret the terrible customer experience this incident has caused. I am reaching out to the affected customers and apologizing for this error.  We will strive to make it up to you by committing ourselves towards building a Myntra shopping experience that is truly wonderful. 

Also, immediately, we will be reviewing all our systems and processes  - and looking at our architecture as well as our deployment systems in great depth to check for any other such shortcomings. 

_Shamik Sharma_ <br/>
_CTO, Myntra_