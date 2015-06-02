
---
title: Manage Users - PaaS FAQ
---

#Manage Users

##Add Users

### How do I add users to my environment via the Catalyze dashboard?

To add a user via the Catalyze dashboard, click on your environment and go to manage users. 

![Manage Users](http://cdn2.dropmark.com/85294/5e84c62bd76d286b7bbe47a2adb52bacba87b84c/Manage%20Users%20Screen%20Shot%20.png)

Enter the id of the user you would like to add and click add user. 

![Add User](http://cdn2.dropmark.com/85294/e9fde899c38cff85ef3977f0bd107a0ba34742e1/Add%20User%20Screen%20Shot.png)

* Note: you can find your user ID by going to the accounts page in the Catalyze dashboard [here](https://dashboard.catalyze.io/account)

![Dashboard User ID](http://cdn2.dropmark.com/85294/95c2e1447b13b02d66e575c58138ba95a4732209/User%20ID%20Screen%20Shot%20.png)


### How do I add users to my environment via the Catalyze CLI?

To add a user via the catalyze CLI use the command `catalyze adduser {userid}` this will add a user to the environment associated with the local directory you are in. (hint: you can get a user’s ID by using `catalyze whoami` from the Catalyze CLI)

* Note: if you need to add users to multiple environments you must follow these steps for each environment.

