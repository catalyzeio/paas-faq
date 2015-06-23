---
title: High Availability (HA) - PaaS FAQ
---

# Highly Available (HA) Services
## What is HA?
An HA service means a service is Highly Available. A service is highly available when there is a mechanism in place to detect when a service component is unavailable and restore the service. Catalyze provides HA services by providing redundant components and the ability to quickly restore a service component.

Catalyze provides HA data source and application services for a Platform Environment by adding additional nodes for applications and data sources (servers such as databases and caching servers) when a HA configuration is requested by a customer.

## Can my web application be scaled to handle greater loads?
Yes! Code scaling is increasing a system's ability to handle a growing work load. As the work of a system increases a system with a scaling method should be able to grow to handle the load. Code scaling often means adding additional application servers to a service to handle increased demand. This feature is built right into the Catalyze Platform feature set, contact your account manager or support@catalyze.io to have your Service's limits adjusted.

## Are HA services required by HIPAA?
Highly Available services are not a requirement to be HIPAA Compliant.

## Can I add an HA service to my environment later?
HA components can be added after an environment is deployed. Your application code may need to be changed to handle HA services. The type of code change of course will depend on the type of service and the code platform. Please contact Catalyze Support for assistance with adding HA services to your environment.

## HA Service Examples:
### How do I connect to my Redis HA Service?

The Catalyze Redis HA solution leverages Redis Sentinel to check the health of master and slave nodes. Sentinel provides automatic failover functionality in the event one of the nodes goes down. You can read more about Redis Sentinel here: [Sentinel docs](http://redis.io/topics/sentinel). To leverage this HA solution your client application code will have to connect and talk to the Sentinels to determine which node is the master node. The following will outline to do so.

**Applicable Environment Variables**
The following environment variables will be available to your application:

```
REDIS_SENTINEL_URL="redis-sentinel://127.0.0.14:26379"
REDIS_SENTINEL_LIST="127.0.0.14:26379,127.0.0.15:26379,127.0.0.16:26379"
REDIS_SENTINEL_MASTER="redis01"
```

The `REDIS_SENTINEL_LIST` variable is really the key variable. Depending on the redis client, you can pass the list of sentinels to the client and then it automatically determines which instance is the master and that commands get sent to.

For the connection, if needed/accepted by the client, the name of the master is the name, or label,
of the first redis service ("redis_01", for example) also specified in the `REDIS_SENTINEL_MASTER`
environment variable.

**Connection Examples**
Redis clients have made integrating Redis Sentinel very easy. In most cases, all you need to do is provide the connection with a list of the Sentinel addresses. The client then takes care of the negotiations to determine the node to send the Redis commands to.

#### Redis-Client Connection Examples

**Node.js**
Node packages avaiable to connect to redis sentinels:

* [ioredis](https://www.npmjs.com/package/ioredis#sentinel)

    ```
    var Redis = require('ioredis');

    var addresses = process.env.REDIS_SENTINEL_LIST.split(',');
    var endpoints = new Array(addresses.length)
    addresses.forEach(function(element, index, array) {
        addr = element.split(':');
        endpoints[index] = {host: addr[0], port: addr[1]};
    });

    var redisClient = new Redis({
        sentinels: endpoints,
        name: process.env.REDIS_SENTINEL_MASTER
    });
    ```

* [redis-sentinel](https://www.npmjs.com/package/redis-sentinel) (wrapper around node_redis)

    ```
    var sentinel = require('redis-sentinel');

    var addresses = process.env.REDIS_SENTINEL_LIST.split(',');
    var endpoints = new Array(addresses.length)
    addresses.forEach(function(element, index, array) {
        addr = element.split(':');
        endpoints[index] = {host: addr[0], port: addr[1]};
    });

    var redisClient = sentinel.createClient(endpoints, process.env.REDIS_SENTINEL_MASTER);
    ```

**Ruby**
Ruby packages avaiable to connect to redis sentinels:

* [redis-rb](https://github.com/redis/redis-rb#sentinel-support)

    ```
    require "redis"

    sentinel_master = ENV['REDIS_SENTINEL_MASTER']
    addresses = ENV['REDIS_SENTINEL_LIST'].split(',')
    endpoints = Array.new(addresses.length)
    addresses.each_with_index { |addr, index| a = addr.split(':'); endpoints[index] = {:host => a[0], :port => a[1]} }

    redis = Redis.new(:url => "redis://#{sentinel_master}", :sentinels => endpoints, :role => :master)
    ```

**Python**
Python packages avaiable to connect to redis sentinels:

* [redis-py](https://github.com/andymccurdy/redis-py#sentinel-support)

    ```
    import os
    from redis.sentinel import Sentinel

    sentinel_master = os.environ['REDIS_SENTINEL_MASTER']
    sentinel_address_list = os.environ['REDIS_SENTINEL_LIST']
    sentinel = Sentinel([tuple(address.split(':')) for address in sentinel_address_list.split(',')])
    master = sentinel.master_for(sentinel_master)
    ```
