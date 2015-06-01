#Adding users to an environment

Q: How do I add users to my environment via the Catalyze dashboard?

A: To add a user via the Catalyze dashboard, click on your environment and go to manage users. 
![Manage Users Button](/Add Users Screenshots/Manage Users Screenshot.png)
Enter in the id of the user you would like to add and click add user. (hint: you can get a user’s ID by using `catalyze whoami` from the Catalyze CLI)
![Add User Button](/Add Users Screenshots/Add User Screenshot.png)

Q: How do I add users to my environment via the Catalyze CLI?

A: To add a user via the catalyze CLI use the command `catalyze adduser {userid}` this will add a user to the environment associated with the local directory you are in. (hint: you can get a user’s ID by using `catalyze whoami` from the Catalyze CLI)

*Note: if you need to add users to multiple environments you must follow these steps for each environment you want to add users to.
