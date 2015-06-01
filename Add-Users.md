#Manage Users

###Add Users

Q: How do I add users to my environment via the Catalyze dashboard?

A: To add a user via the Catalyze dashboard, click on your environment and go to manage users. 

![Manage Users Button](Manage Users Screenshot.png)
Enter the id of the user you would like to add and click add user. 

![Add User Button](Add User Screenshot.png)
hint: you can find your user ID by going to the accounts page in the Catalyze dashboard [here](https://dashboard.catalyze.io/account))

![Dashboard User ID](User ID Screenshot.png)


Q: How do I add users to my environment via the Catalyze CLI?

A: To add a user via the catalyze CLI use the command `catalyze adduser {userid}` this will add a user to the environment associated with the local directory you are in. 
hint: you can get a user’s ID by using `catalyze whoami` from the Catalyze CLI

*Note: if you need to add users to multiple environments you must follow these steps for each environment.

