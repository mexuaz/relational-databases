# CSC 370 - SQL Golf

## Assignment Goals

In this assignment you will:

  * demonstrate data analysis skills with SQL

    + write SQL queries with increasing complexity to extract desired information from a relational database
    + optimise SQL queries towards simplicity

## Task

[Code Golf](https://www.barrymichaeldoyle.com/code-golf/) is a sort of recreational programming activity in which one tries to implement functionality using as few characters as possible. The general goal is to think of alternative solutions to a problem and it derives its name from the sport of _golf_, in which one tries to minimise the number of whacks with an iron shaft to put a tiny ball in a far-flung hole. In this assignment, you will try not just to write SQL queries that are correct, but that also are "minimal." 

As an example, imagine that you have two relations: *Employee(<ins>employee_id</ins>, employee_name, dept_id)* and *Department(<ins>dept_id</ins>, dept_name)* and you would like to find the names of all employees in a department named "Shipping & Receiving". A simple solution would be:

```sql
SELECT `employee_name`
FROM `Employee`
    NATURAL JOIN `Department`
WHERE `dept_name` LIKE 'Shipping \& Receiving';
```

Certainly, another "correct" solution would be:

```sql
SELECT `employee_name`
FROM `Employee`
WHERE `dept_id` IN (
    SELECT `dept_id`
    FROM `Department`
    WHERE `dept_name` LIKE 'Shipping \& Receiving' );
```

Both queries retrieve the same result, but the second query is unnecessarily complex, or at the very least non-idiomatic. I hope that you prefer the first solution. Even if not, this assignment is designed to encourage you to write the first query by rewarding you inversely to the number of times any of the following tokens appears in your SQL query:

  * SELECT (i.e., projection operator)
  * FROM (i.e., the table- or index-scan operator)
  * , (i.e., the cross product operator)
  * JOIN (i.e., a theta-, natural, or outer join or per MySQL an intersection)
  * UNION (i.e., the bag union operator)
  * DISTINCT (i.e., the duplicate elimination operator)
  * GROUP (i.e., the group-by operator)
  * ORDER (i.e., the sort operator)
  * HAVING (i.e., the selection operator applied to groups)
  * WHERE (i.e., the selection operator applied to tuples)
  * LIMIT (i.e., the MySQL top-k operator)

This gives us a metric by which to claim the first query is better: it only uses 4 instances of the above set of operators (SELECT, FROM, JOIN, and WHERE), whereas the second query uses 6 instances (2×SELECT, 2×FROM, 2×WHERE). This is the metric that you should aim to minimise with the SQL queries that you submit. You would receive more marks for the first query than the second one.

It is important to remember that this is an exercise in code simplification and creative thinking, not in performance optimisation. Although you are trying to minimise the number of operator references, SQL is a _declarative language_ and there is no specific reason to assume that the first example query will run faster than the second one. However, simple and idiomatic code is easier for compilers to optimise, so there could be tangential performance benefits to striving for simpler—or at least shorter—queries.

You are given instructions to create (optionally) a MySQL database. Moreover, you are given twenty `.sql` files that are unfortunately empty except for a comment indicating their intended query and their mapping between "SQL Golf" scores (i.e., total instances of the aforementioned operators/tokens) and grade. For example, the above problem would be represented by the following `example.sql` file:

```sql
-- Find the names of all employees in a department named "Shipping & Receiving"
-- 1.1 marks: <4 operators
-- 1.0 marks: <6 operators
-- 0.8 marks: correct answer

-- Replace this comment line with the actual query
```

Alongside the `.sql` file will be a `.csv` file showing the expected result, which you can use for testing.


## Dataset



## Submission

You should submit all of the `.sql` files without renaming them, but after replacing the final comment line with an actual SQL query that achieves the stated objective. Ordinarily, you should submit twenty `.sql` files, though it is okay to submit fewer files if you do not have a solution for all twenty tests.

## Evaluation

Your grade on the assignment will be the sum of your scores on each query, which could be in excess of 20 (the number of tests), particularly if you minimise your queries more effectively than the teaching team has. However, to receive any marks on a particular query, you *must* produce the correct result. We will ascertain this by performing a `diff` between the corresponding `.csv` file and your query results on an up-to-date MySQL instance prior to counting operators.

Above, the first query would score 1.0 marks and the second query would score 0.8 marks. If you can answer the query with fewer operator instances than the first query, you would score 1.1 marks. The following query would obtain 0.0 marks, even though the number of operators is small, because it does not produce the same result (namely, it doesn't filter by department):

```sql
SELECT `employee_name`
FROM `Employee`;
```

## Sources

You are permitted to use sources that you find on the Internet, so long as it is clear that the source existed prior to the creation of this assignment and you provide a citation in your source code. For example, GitHub and StackOverflow content is permitted, so long as they are clearly dated prior to the beginning of this semester. If you do not include a citation in your source code, your work will be considered plagiarism.

You should, however, work through the assignment on your own. You are welcome to prepare for the assignment with peers in the class by working through the ungraded worksheets together.

## Illness Policy

The end date for the assignment is three days later than the due date. This is expected to provide sufficient contingency for most minor illnesses and you should submit by the due date rather than the end date if you are not constrained by illness.

In the event that three days contingency is insufficient, you could contact the instructor in advance of the due date with a brief explanation. If you have submitted all previous, graded assignments, then your quiz for this module will be used as the assessment for these learning outcomes. If, on the other hand, you have a missing assignment due to, for example, prior illness this semester, then a well-justified second absence longer than three days we be accommodated with a make-up assessment in the form of an individual, closed, recorded oral exam over Zoom conducted by the instructor. The use of make-up assessments will help to ensure that there are sufficiently many assessment activities (at least 80% of the grade) for each student to accurately reflect their achievement in this course.

You are encouraged to submit your preliminary progress one week and again three days prior to the assignment deadline to document progress in case of illness. These preliminary submissions can, of course, be overwritten by your final submission.

## Summary

I hope that this assignment is a fun way to learn and/or practice the SQL query language. Good luck!