---
title: Environment Metrics
---

Environment Metrics
===================

## Metrics Overview
Looking through metrics data at a high level can give you a pretty good indication of how well your application is performing. The Catalyze Platform provides you with several metrics to get you started analyzing the performance of your application. Each metric reported represents the state captured during a collection window spanning one minute. 

### Can I get metrics outside of the last 24 hours?
The platform stores a maximum of 24 hours worth of metrics data for your environment, in 1-minute intervals (1440 data points). Additional data can be captured and stored off-site by using the Catalyze CLI (refer to the CLI's [metrics command](https://github.com/catalyzeio/cli/blob/master/Docs.md#-metrics) for more information). There’s no PHI in metrics so you can store that data anywhere you like. 

## CPU Metrics
### Usage
The usage value is the delta of cumulative CPU usage from the beginning to the end of the (one minute) collection window. While this definition is a bit vague, charting this value over time will show you trends and periods when the CPU is busier. If your application is consistently subjected to high usage and load your web application's performance may be impacting user experiences. 

One way to reduce perceived performance problems is to increase the scale of application instances. Sharing the load across two or more load balanced application instances is a good way to deliver high availability and great experiences. Contact us at [sales@catalyze.io](mailto:sales@catalyze.io) or [support@catalyze.io](mailto:support@catalyze.io) to inquire about scaling your application and highly-available environment configurations. 

## Memory Metrics
### Usage
Memory usage is reported in kilobytes. Three values are reported: the memory usage minimum, maximum, and average from the beginning to the end of the capture window. 

Memory can be critical to your application performing at its best. If your application's memory is approaching the limits of what's available you might consider upgrading to a larger size with more available memory. Reach out to us at [sales@catalyze.io](mailto:sales@catalyze.io) or [support@catalyze.io](mailto:support@catalyze.io) to get more information about resizing your services. 

## Disk I/O Metrics
### Read
The value reported in this field is the number of kilobytes read during the collection window. These values can be correlated with the retrieve operations of your web application. High values for bytes read can get costly for your application affecting the responsiveness your users will experiences. 

A couple ways to alleviate high reads is to store frequently used data in memory or add a memory based cache service, like Redis, to your environment. Contact us at [sales@catalyze.io](mailto:sales@catalyze.io) or [support@catalyze.io](mailto:support@catalyze.io) to inquire more about adding a cache service to your environment. 

### Write
The value reported in this field is the number of kilobytes written during the collection window. If you are observing high values, this can be correlated with create, update, and delete operations of your web application. 

High values can affect the performance of your web application. Background processing can be added to your application to alleviate request processing time and increase the responsiveness of your application. Background processing is easy to incorporate check out our [documentation resources](https://resources.catalyze.io/paas/paas-faq/background-processing/) or contact us at [sales@catalyze.io](mailto:sales@catalyze.io) or [support@catalyze.io](mailto:support@catalyze.io) to inquire more about background processing in your environment. 

### Synchronous and Asynchronous Operations 
The value reported in these fields are the number of operations completed during the collection window. These disk I/O operations will correspond with the read and write values as previously described. Like with read and write metrics, high values can indicate opportunities for performance optimizations. Reducing the number of operations is generally a difficult target to attain but the value of this metric is in recognizing and identifying times when your application's responsiveness is affected. Optimizing those operations within your application will result in better user experiences. 
