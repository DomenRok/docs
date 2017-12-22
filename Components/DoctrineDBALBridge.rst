DoctrineDBALBridge
==================

This package provides a command bus middleware that can be used to
integrate
`SimpleBus/MessageBus <https://github.com/SimpleBus/MessageBus>`__ with
`Doctrine DBAL <https://github.com/doctrine/dbal>`__.

It provides an easy way to wrap command handling in a database
transaction.

@TODO The intro should explain what it does.

Getting started
---------------

Installation
............

Using `Composer <https://getcomposer.org/>`__:

.. code-block::  bash

    composer require simple-bus/doctrine-dbal-bridge

Preparations
............

To use the middleware provided by the library, set up a `command
bus <../Guides/command_bus.html>`__, if
you didn't already do this:

.. code-block::  php

    use SimpleBus\Message\Bus\Middleware\MessageBusSupportingMiddleware;

    $commandBus = new MessageBusSupportingMiddleware();
    ...

Make sure to also properly set up a Doctrine connection:

.. code-block::  php

    // $connection is an instance of Doctrine\DBAL\Driver\Connection
    $connection = ...;

Transactions
------------

It is generally a good idea to wrap command handling in a database
transaction. If you want to do this, add the
``WrapsMessageHandlingInTransaction`` middleware to the command bus.
Provide an instance of the Doctrine ``Connection`` interface that you
want to use.

.. code-block::  php

    use SimpleBus\DoctrineDBALBridge\MessageBus\WrapsMessageHandlingInTransaction;

    // $connection is an instance of Doctrine\DBAL\Driver\Connection
    $connection = ...;

    $transactionalMiddleware = new WrapsMessageHandlingInTransaction($connection);

    $commandBus->addMiddleware($transactionalMiddleware);

When an exception is thrown, the transaction will be rolled back. If
not, the transaction is committed.
