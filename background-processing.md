# Background Processing and Workers
Background processing includes any operations performed outside of the main application. These operations are typically long running tasks that can be more resource intensive. You don't want these operations to detract from the performance of your application, and have your customers' experience damaged, so the logical choice is to separate them.

Catalyze has designed a feature to help you easily deploy background "worker" processes that exist within your application's code base. Workers are long running processes that will run along side of your application. Workers are not tasks designed to be run once (rake tasks, database migrations, etc). A couple common frameworks for background processing include [Sidekiq (Ruby)](http://sidekiq.org/) and [Celery (Python)](http://www.celeryproject.org/). These frameworks are convenient because they allow you to develop and maintain your background processing along with your application code in one repository. These frameworks typically operate asynchronously by passing messages via a broker or queue (RabbitMQ and Redis are popular options).

## OK, i'm ready to deploy a worker, what do I do?

There are just two simple things you need to do in order to launch a worker process.

1. Add a target to your Procfile
2. Deploy the worker with the Catalyze CLI

In your Procfile you can have multiple targets defined. If you look at the contents of your Procfile you will see a line like `web: ...` with the command to start up your web application. After adding a worker target your Procfile might look like this:

```
web: bundle exec unicorn -p $PORT -c ./config/unicorn.rb
worker: bundle exec sidekiq
```

After modifying the Procfile, commit and push the new changes Catalyze. Now that the Procfile changes are deployed we are ready to launch the worker process. Using the Catalyze CLI this is easy. Running `catalyze worker --help` will show you the details of the command. The command takes one argument, the name of the Procfile start you want to run as a worker process. Using the Procfile declared above the command would be `catalyze worker worker`. If you had named the worker target more descriptively, say "notification-sender" the CLI command would be `catalyze worker notification-sender`.

## How does my worker process access the "X" service?
Each worker process is started from your application service and therefore inherits all of the same attributes (network interfaces, environment variables, etc). Connecting to your database/cache/message broker service is done by consuming the same environment variables as your application.

## How is my worker process updated?
On each build/redeploy of your application service your worker processes will also be redeployed so that they are running on the same code base as your web application.

## Error launching workers
Worker process logs are sent to your environment's central logging service, you can search for them in the logging interface.  All worker process logs that are logged to syslog will be forwarded to the logging service.  If you receive an error regarding your contracted limits please contact your account manager.
