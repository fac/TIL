# InnoDB Lock Monitor

The output of `SHOW ENGINE INNODB STATUS \G` is useful but doesn't always cut it when you dealing with gnarly deadlock issues for instance.

## Big hairy warning

*Only do this on your dev machines as there can be significant perfmance implications!*


## Enabling the Lock Monitor

```sql
use fac_dev;
CREATE TABLE innodb_lock_monitor (a INT) ENGINE=INNODB;
```


## Disabling it

```sql
use fac_dev;
DROP TABLE innodb_lock_monitor;
```

## How to use it

By default it dumps the output of `SHOW ENGINE INNODB STATUS` to the mysql log every 15 seconds or so with extra locking information. This is useful but you can also just run `SHOW ENGINE INNODB STATUS` in your client to see the same information on demand.

Here is an example of the transactions section both without and with it enabled:

*Without*

```
------------
TRANSACTIONS
------------
Trx id counter 0 1838
Purge done for trx's n:o < 0 1821 undo n:o < 0 0
History list length 36
LIST OF TRANSACTIONS FOR EACH SESSION:
---TRANSACTION 0 0, not started, process no 7613, OS thread id 1169783104
MySQL thread id 9, query id 1099 localhost root
---TRANSACTION 0 1837, ACTIVE 9 sec, process no 7613, OS thread id 1170049344
3 lock struct(s), heap size 368, 3 row lock(s), undo log entries 1
MySQL thread id 10, query id 1119 localhost root
SHOW ENGINE INNODB STATUS
```


*With*

```
------------
TRANSACTIONS
------------
Trx id counter 0 1856
Purge done for trx's n:o < 0 1839 undo n:o < 0 0
History list length 8
LIST OF TRANSACTIONS FOR EACH SESSION:
---TRANSACTION 0 0, not started, process no 7613, OS thread id 1169783104
MySQL thread id 9, query id 1099 localhost root
---TRANSACTION 0 1855, ACTIVE 7 sec, process no 7613, OS thread id 1170049344
3 lock struct(s), heap size 368, 3 row lock(s), undo log entries 1
MySQL thread id 10, query id 1133 localhost root
SHOW ENGINE INNODB STATUS
TABLE LOCK table `testing`.`payroll_errors` trx id 0 1855 lock mode IX
RECORD LOCKS space id 0 page no 52 n bits 72 index `payroll_period_id_fk` of table `testing`.`payroll_errors` trx id 0 1855 lock_mode X
Record lock, heap no 1 PHYSICAL RECORD: n_fields 1; compact format; info bits 0
 0: len 8; hex 73757072656d756d; asc supremum;;

Record lock, heap no 3 PHYSICAL RECORD: n_fields 2; compact format; info bits 32
 0: len 4; hex 80000002; asc     ;; 1: len 4; hex 80000002; asc     ;;

RECORD LOCKS space id 0 page no 51 n bits 72 index `PRIMARY` of table `testing`.`payroll_errors` trx id 0 1855 lock_mode X locks rec but not gap
Record lock, heap no 3 PHYSICAL RECORD: n_fields 5; compact format; info bits 32
 0: len 4; hex 80000002; asc     ;; 1: len 6; hex 00000000073f; asc      ?;; 2: len 7; hex 000000003618bb; asc     6  ;; 3: len 4; hex 80000002; asc     ;; 4: len 5; hex 4572726f72; asc Error;;
```

This is very useful if you're stepping through a transaction trying to work out when it gets its various locks.

## Other InnoDB Monitors

There are various other ones you can enable. See https://dev.mysql.com/doc/refman/5.1/en/innodb-monitors.html for detail.
