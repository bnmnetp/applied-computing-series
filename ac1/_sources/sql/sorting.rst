.. Copyright (C)  Google, Runestone Interactive LLC
   This work is licensed under the Creative Commons Attribution-ShareAlike 4.0
   International License. To view a copy of this license, visit
   http://creativecommons.org/licenses/by-sa/4.0/.


Sorting
=======

Just as you can :ref:`sort data in Sheets<sorting_data>`, you can sort data
using SQL. You can use the ``ORDER BY`` command to sort the rows returned by the
query by whatever criteria you like. As with sorting in Sheets, this applies
primarily to numeric and text columns.

For example, the following query returns the longest 10 bike trips ordered by
duration.


.. activecode:: bikeshare_order_by_duration
   :language: sql
   :dburl: /runestone/books/published/ac1/_static/bikeshare.db

   SELECT
     *
   FROM
     trip_data
   ORDER BY
     duration DESC
   LIMIT
     10


The column name after the ``ORDER BY`` clause specifies which column to use as
the sorting key, in this case ``duration``. In this example, the rows will be
ordered by their ``duration`` column value in decreasing order. To specify
whether you want the rows sorted increasingly (lowest to highest, A-Z) or
decreasingly (highest to lowest, Z-A), use the ``ASC`` (ascending) and ``DESC``
(descending) keywords respectively. In the example above, since you are sorting
by duration from highest to lowest, ``DESC`` is used.

As in Sheets, you can apply filters using ``WHERE`` and sort using ``ORDER BY``
to show the top or bottom rows (sorted by some column) for a given subset of
data. For example, you can return the longest 10 rides by duration just starting
from station 31111.


.. activecode:: bikeshare_order_by_duration_with_where_clause
   :language: sql
   :dburl: /runestone/books/published/ac1/_static/bikeshare.db

   SELECT
     member_type,
     start_date
     end_station
   FROM
     trip_data
   WHERE
     start_station = 31111
   ORDER BY
     duration DESC
   LIMIT
     10


In SQL, you can also order by multiple columns. In this case, the resulting rows
will be ordered by the values in the specified columns, ordered by the first
specified column, then the second specified column, and so forth. For example,
if you ``ORDER BY start_station, end_station, duration``, the rows will first
be sorted by ``start_station``, then within each value of ``start_station`` the
rows will be ordered by ``end_station``, then within each pair of
``start_station`` and ``end_station`` values, the rows will be ordered by
``duration``.


.. activecode:: bikeshare_order_by_multiple_columns
   :language: sql
   :dburl: /runestone/books/published/ac1/_static/bikeshare.db

   SELECT
     start_station,
     end_station,
     duration
   FROM
     trip_data
   ORDER BY
     start_station ASC,
     end_station ASC,
     duration DESC
   LIMIT
     10


Now try to write SQL queries that will answer the following questions.

.. activecode:: bikeshare_most_recent_start_date
   :language: sql
   :dburl: /runestone/books/published/ac1/_static/bikeshare.db

   On what bike number was the most recent (by start date) trip?
   ~~~~

   ====
   assert 0,0 == W00042


.. activecode:: bikeshare_longest_ride_with_same_start_end
   :language: sql
   :dburl: /runestone/books/published/ac1/_static/bikeshare.db

   Write a query using ``ORDER BY`` to find the starting station and duration of
   the longest ride that started and ended at the same station?
   ~~~~

   ====
   assert 0,0 == 31617
   assert 0,1 == 85666
