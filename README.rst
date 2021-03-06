.. -*- rst auto-fill -*-

Redis-LevelDB
============================================================

A redis frontend to google's leveldb: Use leveldb as a Redis-Server.

Redis COMMAND Supported
------------------------------------------------------------

* incr/incrby
* get/set
* mget/mset
* multi/exec/discard
* keys
* info: Different to redis, this info command accepts a flag argument,
  eg: ``info``, ``info k``, ``info t``, ``info kt``
  
  * default: show leveldb.stat info
  * k: show the count of all keys
  * t: show leveldb.sstables info
    
* select: select db (when redis-leveldb run in multi-db mode, with
  argument ``-M <num>``)

Dependencies
------------------------------------------------------------
1. libev:
   
   install with apt-get or port please.
   
2. gmp(http://gmplib.org/):
   
   install with apt-get or port please.

3. leveldb:
   
  #. git clone git://github.com/appwilldev/redis-leveldb.git
  #. cd redis-leveldb
  #. git submodule init
  #. git submodule update

Compile
------------------------------------------------------------

[LIBEV=LIBEV_PREFIX GMP=GMP_PREFIX DEBUG=1] make

Run
------------------------------------------------------------

``./redis-leveldb -h``

options:

* -d:              run redis-level as a daemon process
* -H <host-ip>:    host addr to listen on(eg: 127.0.0.1)
* -P <port>:	   port to listen on(default 8323)
* -D <data-dir>:   leveldb data dir(default "redis.db" under your work
  directory)
* -M <number>:     run in multi-db mode and set its db count to
  <number>, each db in the server is a separatly leveldb database and
  its data directory is a directory named ``db-<num>`` under the
  directory you specified with the option ``-D``; you can use command
  ``select`` to switch db on the client side while redis-leveldb is
  running in this mode. 

    
