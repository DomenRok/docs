Doctrine ORM and domain events
==============================

As described in the documentation of the `SimpleBus/DoctrineORMBridge
package <https://github.com/SimpleBus/DoctrineORMBridge>`__ library it
provides:

-  A command bus middleware which `wraps the handling of commands inside
   a database
   transaction <../Components/DoctrineORMBridge.html#transactions>`__
-  A command bus middleware which `collects domain events recorded by
   entities and lets the event bus handle
   them <../Components/DoctrineORMBridge.html#domain-events>`__

    Install SimpleBus/DoctrineORMBridge

    Before you continue, first install the
    ``simple-bus/doctrine-orm-bridge`` package in your project:

    ::

        composer require simple-bus/doctrine-orm-bridge

When you enable the ``DoctrineORMBridgeBundle`` in your project, both
features will be automatically registered as command bus middlewares:

.. code-block::  php

    class AppKernel extends Kernel
    {
        public function registerBundles()
        {
            $bundles = array(
                ...
                new SimpleBus\SymfonyBridge\DoctrineOrmBridgeBundle()
            )
            ...
        }
        ...
    }

You can optionally configure which entity manager and connection should
be used:

.. code-block::  yaml

    # in config.yml

    doctrine_orm_bridge:
        entity_manager: default
        connection: default
