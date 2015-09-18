---
title: Manage Users - PaaS FAQ
---
#Manage Users

### How do I invite users to my environment via the Catalyze dashboard?

To invite a users to your environment via the dashboard, log in and view the environment you would like to add users to and click the manage users button.

Enter the email address of the user you would like to invite and click invite user.
![Invite User Email Input Screenshot](http://cdn2.dropmark.com/85294/09312c4db6ca933f8100d16022ac56bba6650a0f/Screen%20Shot%202015-09-18%20at%2012.23.55%20PM.png)

An email will be sent to that user with a link that will allow that user to accept the environment invitation.  

* Note: If the person you would like to invite does not have an account with Catalyze they will be asked to create one.

Once that user signs into their new account they can accept the invitation via the dashboard by pasting the invite code they recieved in the invite email into the text box that says enter invite code and clicking accept invitation.
![Enter Invite Code Screenshot](http://cdn2.dropmark.com/85294/2443d282addc717d3ced6d45f4913e86ef3404e9/Screen%20Shot%202015-09-18%20at%2012.23.43%20PM.png)

### How do I invite users to my environment via the Catalyze CLI?

To add a user via the Catalyze CLI, use the command `catalyze invites send {email}`. An email with directions on how to accept the invitation will then be sent to the email address specified.  More documentation on the catalyze CLI can be found [here](https://resources.catalyze.io/paas/cli/).

* Note: if you need to add users to multiple environments you must follow these steps for each environment.
