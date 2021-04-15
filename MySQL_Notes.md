# InnoDB

## ACID Model

-   A: atomicity 原子性

    If any of the statements constituting a transaction fails to complete, the entire transaction fails and the database is left unchanged.

    Related MySQL features: autommit setting, the `COMMIT` statement, the `ROLLBACK` statement.

-   C: consistency 一致性

    A transaction can only bring the database from one valid state to another, maintaining database invariants. This prevents database corruption by an illegal transaction, but does not guarantee that a transaction is *correct*.

    Related MySQL features: doublewrite buffer, crash recovery.

-   I: isolation 隔离性

    Isolation ensures that concurrent execution of transactions leaves the database in the same state that would have been obtained if the transactions were executed sequentially.

    Related MySQL features: autocommit setting, transaction isolation levels and the `SET TRANSACTION` statement, the low-level details of IInnoDB locking.

-   D: durability 持久性

    Once a transaction has been commited, it will remain committed even in the case of a system failure (power outage or crash).

## Multi-Versioning







