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

It contains four lines and all  of them represents **four** independent Events. 

### Filtering

In some cases is required to perform modifications on the Events content.  This process to alter, enrich or drop Events is called Filtering. 

