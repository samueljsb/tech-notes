Databases
=========

Advice for working with databases. This advice pertains to relational
databases; it's possible that some of it is specific to Postgres becasue that's
the system I use most.

Transactions
------------

When we enter a transaction, the queries are sent to the database but their
effects are not visible outside the transaction. The transaction can either be
*committed* (``COMMMIT``), in which case the changes are saved, or *rolled
back* (``ROLLBACK``), in which case they are discarded.

Transactions allow multiple operations to be commited *atomically* and
*durably*. If no transaction is open, we are considered to be in 'auto-commit
mode' -- each query is executed in its own transaction. Transactions can be
nested; Postgres does this with savepoints.

locking
^^^^^^^

A row can be locked so that no other transaction may read/write to it (there
are different kinds of lock for different contexts).

Locks can only be acquired in a transaction.

atomicity and durability
^^^^^^^^^^^^^^^^^^^^^^^^

Atomic
   Either all of the updates are committed, or none of them are.

Durable
   If the transaction is committed, it cannot be rolled back (i.e. this is the
   outermost transaction and is not nested).

These are different properties and are used to acheive different behaviours,
often together.


resources
^^^^^^^^^

- `The trouble with transaction.atomic
  <https://seddonym.me/2020/11/19/trouble-atomic/>`_ by David Seddon
