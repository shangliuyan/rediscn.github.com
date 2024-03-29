---
layout: commands
title: client-pause 命令 -- Redis中文资料站
permalink: commands/client-pause.html
disqusIdentifier: command_client-pause
disqusUrl: http://redis.cn/commands/client-pause.html
commandsType: keys
---

`CLIENT PAUSE` is a connections control command able to suspend all the Redis clients for the specified amount of time (in milliseconds).

The command performs the following actions:

* It stops processing all the pending commands from normal and pub/sub clients. However interactions with slaves will continue normally.
* However it returns OK to the caller ASAP, so the `CLIENT PAUSE` command execution is not paused by itself.
* When the specified amount of time has elapsed, all the clients are unblocked: this will trigger the processing of all the commands accumulated in the query buffer of every client during the pause.

This command is useful as it makes able to switch clients from a Redis instance to another one in a controlled way. For example during an instance upgrade the system administrator could do the following:

* Pause the clients using `CLIENT PAUSE`
* Wait a few seconds to make sure the slaves processed the latest replication stream from the master.
* Turn one of the slaves into a master.
* Reconfigure clients to connect with the new master.

It is possible to send `CLIENT PAUSE` in a MULTI/EXEC block together with the `INFO replication` command in order to get the current master offset at the time the clients are blocked. This way it is possible to wait for a specific offset in the slave side in order to make sure all the replication stream was processed.

@return

@simple-string-reply: The command returns OK or an error if the timeout is invalid.
