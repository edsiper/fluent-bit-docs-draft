# Key Concepts

Before diving into [Fluent Bit](https://fluentbit.io) it’s good to get acquainted with some of the key concepts of the service. This document provides a gentle introduction to those concepts and common [Fluent Bit](https://fluentbit.io) terminology. We’ve provided a list below of all the terms we’ll cover, but we recommend reading this document from start to finish to gain a more general understanding of our log and stream processor.

* Event or Record
* Filtering
* Tag
* Timestamp
* Match
* Source
* Structured Message

### Event or Record

Every incoming piece of data that belongs to a log or a metric that is retrieved by Fluent Bit is considered an Event or a Record. 

As an example consider the following content of a Syslog file:

```text
Jan 18 12:52:16 flb systemd[2222]: Starting GNOME Terminal Server
Jan 18 12:52:16 flb dbus-daemon[2243]: [session uid=1000 pid=2243] Successfully activated service 'org.gnome.Terminal'
Jan 18 12:52:16 flb systemd[2222]: Started GNOME Terminal Server.
Jan 18 12:52:16 flb gsd-media-keys[2640]: # watch_fast: "/org/gnome/terminal/legacy/" (establishing: 0, active: 0)
```

It contains four lines and all of them represents **four** independent Events. 

Internally, an Event always has two minimum components in an array form:

```javascript
[TIMESTAMP, MESSAGE]
```

### Filtering

In some cases is required to perform modifications on the Events content,  the process to alter, enrich or drop Events is called Filtering. 

There are many use cases when Filtering is required like:

* Append specific information to the Event like an IP address or metadata.
* Select a specific piece of the Event content.
* Drop Events that matches certain pattern.

### Tag

Every Event that gets into Fluent Bit gets assigned a Tag. This tag is an internal string that is used in a later stage by the Router to decide which Filter or Output phase it must go through.

Most of the tags are assigned manually in the configuration. If a tag is not specified, Fluent Bit will assign the name of the Input plugin instance from where that Event was generated from.

{% hint style="info" %}
The only input plugin that **don't** assign Tags is Forward input. This plugin speaks the Fluentd wire protocol called Forward where every Event already comes with a Tag associated. Fluent Bit will always use the incoming Tag set by the client.
{% endhint %}

### Timestamp

The Timestamp represents the _time_ when an Event was generated. Every Event contains a Timestamp associated. The Timestamp is a numeric fractional integer in the format:

```javascript
SECONDS.NANOSECONDS
```

#### Seconds

It is the number of seconds that have elapsed since the _Unix epoch_

#### Nanoseconds

