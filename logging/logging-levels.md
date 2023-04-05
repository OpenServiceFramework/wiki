# Logging Levels

Logging levels probably aren’t the most exciting thing in this world.  But then again, neither is banking.  And yet both things are fundamental to the people who use them as a tool.

Application logging is one of the most important things you can do in your code when it comes to facilitating production support.  Your log files serve as a sort of archaeological record of what on earth your codebase did in production.  Each entry in a log file has important information, including a time stamp, contextual information, and a message.  Oh—and generally, something called a logging level.

So what are logging levels?

Well, put as simply as possible, they’re simply a means of categorizing the entries in your log file.  But they categorize in a very specific way—by urgency or severity.  At a glance, the logging level lets you separate the following kinds of information:

- Hey, someone might find this interesting: we just got our fourth user named Bill.
- OH NO SOMEONE GET A FIRE EXTINGUISHER SERIOUSLY RIGHT NOW.

For the most part, this distinction helps in two ways.  First, you can filter your log files this way during search.  And second, you can control the amount of information that you log.  But we’ll get to that in a bit.

## Logging Levels: Why Do We Do It?

When it comes to logging, you have two essential and opposing forces, if you will.  On the one hand, you want to capture every last detail you can because this might prove useful during troubleshooting or auditing your system.  But on the other hand, all of that logging consumes resources. You can eat up disk space, overload people reading the logs, and even start to slow down your production code if you go overboard.

So logging requires either a balance or a way to get both the proverbial signal and the noise.  And logging levels look to help with this by making your situation configurable on the fly.

Here’s a helpful metaphor, perhaps.  Imagine you have an android friend and you ask him about what he did today.

>“Well, I woke up, inhaled, moved my nose three inches to the right—”
>
>“No!  Too much information.  Go from granularity 10 down to 3.”
>
>“I woke up, had breakfast, caught a taxi…”
>
>“THAT’s better.”

Usually, you don’t need to know everything the android did.  But if he starts malfunctioning, you might want to go back to “granularity 10” to zoom in on the problem as narrowly as possible.

Logging levels work this way.  Often you’ll only want to know if there are problems or warning conditions.  But sometimes you’ll really want to dial up the information for troubleshooting purposes.

## Where Did Logging Levels Come From, Anyway?

Most people that have spent time in the software industry, especially supporting it in production, have seen this, at least in passing.  But this is not actually a new phenomenon.  It’s been around for quite a while.

Back in the 1980s, a project called Sendmail prompted the development of the syslog utility.  This became a de facto standard, and along with it came the concept of severity level.

In the years since then, programming languages have matured and evolved, developing ecosystems.  The standardization around logging has grown into application logging frameworks, including such popular ones as log4j and log4net.  And the concept of severity level came along for the ride at some point, emerging into today’s logging levels.

Of course, you don’t have completely uniform names for the levels across all languages, frameworks, and stacks.  But the concepts are by and large the same.

## Common Logging Levels

So what are these logging levels?  Here are some common ones that you’ll see, listed in order from most severe to least severe, and followed up by some that are meta-considerations.  When logging from your application, follow these guidelines:

## FATAL

Fatal represents truly catastrophic situations, as far as your application is concerned.  Your application is about to abort to prevent some kind of corruption or serious problem, if possible.  This entry in the log should probably result in someone getting a 3 AM phone call.

## ERROR

An error is a serious issue and represents the failure of something important going on in your application.  Unlike FATAL, the application itself isn’t going down the tubes.  Here you’ve got something like dropped database connections or the inability to access a file or service.  This will require someone’s attention probably sooner than later, but the application can limp along.

## WARN

Now we’re getting into the grayer area of hypotheticals.  You use the WARN log level to indicate that you might have a problem and that you’ve detected an unusual situation.  Maybe you were trying to invoke a service and it failed a couple of times before connecting on an automatic retry.  It’s unexpected and unusual, but no real harm done, and it’s not known whether the issue will persist or recur.  Someone should investigate warnings.

## INFO

Finally, we can dial down the stress level.  INFO messages correspond to normal application behavior and milestones.  You probably won’t care too much about these entries during normal operations, but they provide the skeleton of what happened.  A service started or stopped.  You added a new user to the database.  That sort of thing.

## DEBUG

With DEBUG, you start to include more granular, diagnostic information.  Here, you’re probably getting into “noisy” territory and furnishing more information than you’d want in normal production situations.  You’re providing detailed diagnostic information for fellow developers, sysadmins, etc.

## TRACE

This is really fine-grained information—finer even than DEBUG.  When you’re at this level, you’re basically looking to capture every detail you possibly can about the application’s behavior.  This is likely to swamp your resources in production and is seriously diagnostic.

## How This Works: the Dance of Log Requests

At this point, you might be wondering how all this happens between the log file and the application.  Well, simply put, there are two participating parties in logging:

- The logging framework, at runtime, has a configured log level.
- The application code makes logging requests.

If the framework has a given log level enabled, then all requests at that level or higher priority wind up in the log platform.  Everything else is denied.  So consider the following pseudo-code:

```javascript
void DoStuffWithInts(int x, int y) {
    log.trace(x);
    log.error(y);
}
```

If we had the log level set to ALL or TRACE, you would see both integers in the log file.  If we changed the log level to, say, WARN, then we would only see y.  And if we turned the log level all the way down to FATAL, we would see nothing.

## Use Logging Levels Liberally

When it comes to logging levels, though, I’ll close with one last bit of advice.  Use them liberally in your application, erring on the side of providing too much information (but in the lower levels, like DEBUG or TRACE).  This gives you the option of tuning the log level and making adjustments down the road.  If you err on the side of leaving them out, there’s no production setting that can magically include them.  And giving yourself options in production is the name of the game.

***

### References

- [Sentinelone: Logging Levels](https://www.sentinelone.com/blog/logging-levels)
