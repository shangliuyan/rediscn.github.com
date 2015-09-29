---
layout: commands
title: zcount 命令 -- Redis中文资料站
permalink: commands/zcount.html
disqusIdentifier: command_zcount
disqusUrl: http://redis.cn/commands/zcount.html
commandsType: keys
---

Returns the number of elements in the sorted set at `key` with a score between
`min` and `max`.

The `min` and `max` arguments have the same semantic as described for
`ZRANGEBYSCORE`.

Note: the command has a complexity of just O(log(N)) because it uses elements ranks (see `ZRANK`) to get an idea of the range. Because of this there is no need to do a work proportional to the size of the range.

@return

@integer-reply: the number of elements in the specified score range.

@examples

```cli
ZADD myzset 1 "one"
ZADD myzset 2 "two"
ZADD myzset 3 "three"
ZCOUNT myzset -inf +inf
ZCOUNT myzset (1 3
```