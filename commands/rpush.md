---
layout: commands
title: rpush 命令 -- Redis中文资料站
permalink: commands/rpush.html
disqusIdentifier: command_rpush
disqusUrl: http://redis.cn/commands/rpush.html
commandsType: keys
---

Insert all the specified values at the tail of the list stored at `key`.
If `key` does not exist, it is created as empty list before performing the push
operation.
When `key` holds a value that is not a list, an error is returned.

It is possible to push multiple elements using a single command call just
specifying multiple arguments at the end of the command.
Elements are inserted one after the other to the tail of the list, from the
leftmost element to the rightmost element.
So for instance the command `RPUSH mylist a b c` will result into a list
containing `a` as first element, `b` as second element and `c` as third element.

@return

@integer-reply: the length of the list after the push operation.

@history

* `>= 2.4`: Accepts multiple `value` arguments.
  In Redis versions older than 2.4 it was possible to push a single value per
  command.

@examples

```cli
RPUSH mylist "hello"
RPUSH mylist "world"
LRANGE mylist 0 -1
```