---
title: Manage Users - PaaS FAQ
---

#Manage Users

##Add Users

### How do I add users to my environment via the Catalyze dashboard?

To add a user via the Catalyze dashboard, click on your environment and go to manage users. 

Enter the id of the user you would like to add and click add user. 

* Note: you can find your user ID by going to the accounts page in the Catalyze dashboard [here](https://dashboard.catalyze.io/account)

### How do I add users to my environment via the Catalyze CLI?

To add a user via the catalyze CLI use the command `catalyze adduser {userid}` this will add a user to the environment associated with the local directory you are in. (hint: you can get a user’s ID by using `catalyze whoami` from the Catalyze CLI)

* Note: if you need to add users to multiple environments you must follow these steps for each environment.

