# Logging: Best Practices

Log formatting is crucial to achieving readable log files. But why would you need readable (i.e., human-readable) log files in the first place?

You might argue that a log file should be machine-readable. I whole-heartedly agree with that. Having machine-readable logs enables you to use tools that can automatically parse, process, and analyze them. As a result, you can gain valuable insights that would otherwise be lost to you.

But your log files need to be easily readable to people, too. One of the primary purposes of logging is to enable post-mortem debugging. People will look at the log entries. They’ll use the information they see there to try and reconstruct what happened with the application. That job is already hard—there’s no need to make it harder by having unreadable log files.

Hopefully, you now agree that readable log files are a must. Now you need to know how to achieve readable log files, and that’s what the following tips will help you to do. Let’s get started.

## 1. Always use the library from OpenServiceFramework (OSF)

## 2. Make Your Log Entries Meaningful With Context

Consider the following log entry:

> 2017-05-23T15:02:27Z | WARN | Record not found

Consider now this one:

> 2017-05-23T15:02:27Z | WARN | Project with the id ’53’ was not found

Which one would you rather have? The second one, right? That’s what I thought. Add as much context as possible to your log messages with respect to their level and expected granularity. That will not only help its readers to get a headstart on fixing the problem. But it will also make each message more unique and easily distinguishable.

## 3. Employ Logging Levels Correctly

Properly employing [logging levels](logging-levels.md) is one of the most important things you can do for your log files. That’ll make it easier for automatic parsers to understand them. But it also helps human readers, which is our main focus today. The correct use of levels will make your log files more easily searchable and, yes, readable. But what are logging levels?

Briefly, logging levels are labels. You use them to categorize your log entries by urgency, or severity. By applying logging levels, you gain the ability to easily search and filter your log entries by their levels. Levels also help you control the granularity of your log entries—more on that later.

So, how do you set logging levels?

Simply by using correct method. The logging library in OSF has dedicated methods for each logging level. For DEBUG level it has logDebug, for INFO level it has logInfo, and so on.

We have provisioned for the following logging levels in the OSF logging library

- FATAL
- ERROR
- WARN
- INFO
- DEBUG
- TRACE


## 4. Include the Stack Trace When Logging an Exception

This section should be short since its title pretty much says everything there is to it. When logging an exception, you should always include its stack trace. For the developer performing a post-mortem debug, the stack trace is essential information that will help them connect the dots.

## 5. Include the Name of the Thread When Logging From a Multi-Threaded Application

Like the previous section, this one also has its contents spoiled by its title. When logging from an application with multiple threads, always include the name of the thread where the event happened. That will enable searching/filtering, making the entries not only easily parseable but also more readable for humans.

## Log Formatting Is Good for Machines and Great for Humans

Logging is vital for any non-trivial applications. Without logging, it’d be extremely hard to understand how the code we write behaves “in the wild.” We’d have a hard time trying to fix bugs. We’d have no idea about how our users actually use the software we write. In short—we’d be clueless to the extreme.

However, it’s not enough just to have logging in place. Getting started with logging is the first step. After that, you need to evolve your approach. You must ensure that your logs are readable, both by machines and humans. You should have logs that are well-formatted and easily parseable. That way, you can learn from your logs, gaining insights about your application and your users that would otherwise be lost.

By having logs that are easy for humans to read, you make post-mortem debug less of a burden for you and your fellow developers. Log formatting represents a win for everyone, so start employing it ASAP.

***
#### Reference:
- <https://www.sentinelone.com/blog/log-formatting-best-practices-readable/>
