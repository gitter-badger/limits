.. currentmodule:: limits
.. _storage-scheme:

Storage url scheme
------------------

**limits** uses a url style storage scheme notation (similar to the JDBC driver
connection string notation) for configuring and initializing
storage backends. This notation additionally provides a simple
mechanism to both identify and configure the backend implementation based on
a single string argument.

The storage scheme follows the format :code:`{scheme}://{parameters}`

:func:`limits.storage.storage_from_string` is provided to
lookup and construct an instance of a storage based on the storage scheme. For example::

 import limits.storage
 uri = "redis://localhost:9999"
 options = {}
 redis_storage = limits.storage.storage_from_string(uri, **options)


Examples
========

In-Memory
 The in-memory storage takes no parameters so the only relevant value is :code:`memory://`

Memcached
 Requires the location of the memcached server(s). As such
 the parameters is a comma separated list of :code:`{host}:{port}` locations such as
 :code:`memcached://localhost:11211` or
 :code:`memcached://localhost:11211,localhost:11212,192.168.1.1:11211` etc...

Redis
 Requires the location of the redis server and optionally the database number.
 :code:`redis://localhost:6379` or :code:`redis://localhost:6379/1` (for database `1`)

Redis with Sentinel
 Requires the location(s) of the redis sentinal instances and the `service-name`
 that is monitored by the sentinels.
 :code:`redis+sentinel://localhost:26379/my-redis-service`
 or :code:`redis+sentinel://localhost:26379,localhost:26380/my-redis-service`
