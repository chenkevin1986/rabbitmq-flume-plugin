rabbitmq-flume-plugin
=====================
A Flume plugin that provides a RabbitMQ *Source*, *Sink*, and *Interceptors*. While
there are other Flume(ng) plugins that do this as well, this implementation aims
to be highly performant and provide tools for mapping message properties to Flume
event headers.

Download
--------
No downloads available, this has yet to be released. The intention is to provide
a **jar** file for download in the releases page on GitHub.

Installation Instructions
-------------------------
To install the plugin, copy the *jar* file to the ``$FLUME_LIB`` directory. For
example, the ``$FLUME_LIB`` directory for Cloudera (CDH4) installed Flume, the
``$FLUME_LIB`` is ``/usr/lib/flume/lib``.

Configuration
-------------
Each component has its own configuration directives, but the **Source** and **Sink**
share common RabbitMQ connection parameters.

### Source

Variable          | Default       | Description
----------------- | ------------- | -----------
host              | ``localhost`` | The RabbitMQ host to connect to
port              | ``5672``      | The port to connect on
virtual_host      | ``/``         | The virtual host name to connect to
username          | ``guest``     | The username to connect as
password          | ``guest``     | The password to use when connecting
queue             |               | **Required** field specifying the name of the queue to consume from
no_ack            | ``false``     | Toggle ``Basic.Consume`` no_ack mode
prefetch_count    | ``0``         | The ``Basic.QoS`` prefetch count to specify for consuming
prefetch_size     | ``0``         | The ``Basic.QoS`` prefetch size to specify for consuming
ssl               | ``false``     | Connect to RabbitMQ via SSL
exclude_protocols | ``SSLv3``     | A comma separated list of SSL protocols to exclude/ignore
threads           | ``1``         | The number of consumer threads created.

#### Example

.. code::

    a1.sources.r1.channels = c1
    a1.sources.r1.type = com.aweber.flume.source.rabbitmq.RabbitMQSource
    a1.sources.r1.hostname = localhost
    a1.sources.r1.port = 5672
    a1.sources.r1.virtual_host = /
    a1.sources.r1.username = flume
    a1.sources.r1.password = rabbitmq
    a1.sources.r1.queue = events_for_s3
    a1.sources.r1.prefetch_count = 10

### Interceptors

### Sink

Build Instructions
------------------
To build from source, use ``maven``:

.. code:: bash

    mvn package

This will download all of the dependencies required for building the plugin and
provide a **jar** file in the ``target/`` directory.
