---
title: Manage Users - PaaS FAQ
---

#Manage Users

##Add Users

### How do I add users to my environment via the Catalyze dashboard?

To add a user via the Catalyze dashboard, view the environment you want to add a user to and click the "Manage Users" button.
Enter the User ID of the user you would like to add and click "Add User".
(hint: User IDs can be located by going to the [accounts page](https://dashboard.catalyze.io/account) in the Catalyze dashboard)

### How do I add users to my environment via the Catalyze CLI?

To add a user via the catalyze CLI use the command `catalyze adduser {userid}` this will add a user to the environment associated with the local directory you are in. 
(hint: you can get a user’s ID by using `catalyze whoami` from the Catalyze CLI)

* Note: if you need to add users to multiple environments you must follow these steps for each environment.

