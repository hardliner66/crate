.. highlight:: psql

.. _comparison-operators:

====================
Comparison operators
====================

A comparison operator tests the relationship between two values and returns a
corresponding value of ``true``, ``false``, or ``null``.

The following operators can be used for all simple data types:

========  ==========================
Operator  Description
========  ==========================
``<``     Less than
--------  --------------------------
``>``     Greater than
--------  --------------------------
``<=``    Less than or equal to
--------  --------------------------
``>=``    Greater than or equal to
--------  --------------------------
``=``     Equal
--------  --------------------------
``<>``    Not equal
--------  --------------------------
``!=``    Not equal (same as ``<>``)
========  ==========================

When comparing strings, a lexicographical comparison is performed. For
example::

    cr> select name from locations where name > 'Argabuthon' order by name;
    +------------------------------------+
    | name                               |
    +------------------------------------+
    | Arkintoofle Minor                  |
    | Bartledan                          |
    | Galactic Sector QQ7 Active J Gamma |
    | North West Ripple                  |
    | Outer Eastern Rim                  |
    +------------------------------------+
    SELECT 5 rows in set (... sec)

.. SEEALSO::

    For more details, refer to the *Apache Lucene* `TermRangeQuery`_ documentation.

When comparing dates, strings using ISO date formats can be used::

    cr> select date, position from locations where date <= '1979-10-12' and
    ... position < 3 order by position;
    +--------------+----------+
    | date         | position |
    +--------------+----------+
    | 308534400000 |        1 |
    | 308534400000 |        2 |
    +--------------+----------+
    SELECT 2 rows in set (... sec)

.. SEEALSO::

    For more details, refer to the *Joda Time* `dateOptionalTimeParser`_
    documentation.

.. TIP::

    Comparison operators are commonly used to filter rows (e.g., in the
    ``WHERE`` and ``HAVING`` clauses of a :ref:`sql_reference_select`
    statement). However, basic comparison operators can be used as value
    expressions in any context. For example::

        cr> SELECT 1 < 10 as my_column;
        +--------------+
        | my_column    |
        +--------------+
        | true         |
        +--------------+
        SELECT 1 rows in set (... sec)

Within a :ref:`sql_dql_where_clause`, the following operators are also
available:

==========================  ===================================================
Operator                    Description
==========================  ===================================================
``~``                       Matches regular expression (case sensitive)
--------------------------  ---------------------------------------------------
``!~``                      Matches regular expression (case insensitive)
--------------------------  ---------------------------------------------------
``!~``                      Does not match regular expression (case sensitive)
--------------------------  ---------------------------------------------------
``!~*``                     Does not match regular expression (case
                            insensitive)
--------------------------  ---------------------------------------------------
:ref:`sql_dql_like`         Matches a part of the given value
--------------------------  ---------------------------------------------------
:ref:`sql_dql_not`          Negates a condition
--------------------------  ---------------------------------------------------
:ref:`sql_dql_is_null`      Matches a null value
--------------------------  ---------------------------------------------------
:ref:`sql_dql_is_not_null`  Matches a non-null value
--------------------------  ---------------------------------------------------
``ip << range``             True if IP is within the given IP range (using
                            `CIDR notation`_)
--------------------------  ---------------------------------------------------
``x BETWEEN y AND z``       Shortcut for ``x >= y AND x <= z``
==========================  ===================================================

.. SEEALSO::

    - :ref:`sql_array_comparisons`
    - :ref:`sql_subquery_expressions`


.. _CIDR notation: https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing#CIDR_notation
.. _dateOptionalTimeParser: http://joda-time.sourceforge.net/api-release/org/joda/time/format/ISODateTimeFormat.html#dateOptionalTimeParser%28%29
.. _TermRangeQuery: https://lucene.apache.org/core/6_6_0/core/org/apache/lucene/search/TermRangeQuery.html
