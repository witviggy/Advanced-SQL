# Advanced-SQL
HackerRank SQL Problems and queries....
You are given a table, Projects, containing three columns: Task_ID, Start_Date and End_Date. It is guaranteed that the difference between the End_Date and the Start_Date is equal to 1 day for each row in the table.

If the End_Date of the tasks are consecutive, then they are part of the same project. Samantha is interested in finding the total number of different projects completed.

Write a query to output the start and end dates of projects listed by the number of days it took to complete the project in ascending order. If there is more than one project that have the same number of completion days, then order by the start date of the project.

Sample Input

Sample Output

2015-10-28 2015-10-29
2015-10-30 2015-10-31
2015-10-13 2015-10-15
2015-10-01 2015-10-04

Explanation

The example describes following four projects:

Project 1: Tasks 1, 2 and 3 are completed on consecutive days, so these are part of the project. Thus start date of project is 2015-10-01 and end date is 2015-10-04, so it took 3 days to complete the project.
Project 2: Tasks 4 and 5 are completed on consecutive days, so these are part of the project. Thus, the start date of project is 2015-10-13 and end date is 2015-10-15, so it took 2 days to complete the project.
Project 3: Only task 6 is part of the project. Thus, the start date of project is 2015-10-28 and end date is 2015-10-29, so it took 1 day to complete the project.
Project 4: Only task 7 is part of the project. Thus, the start date of project is 2015-10-30 and end date is 2015-10-31, so it took 1 day to complete the project.

LINK: https://www.hackerrank.com/challenges/sql-projects/problem?isFullScreen=true&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen&h_r=next-challenge&h_v=zen

Query: 

WITH CTE1 AS (
    SELECT start_date, RANK() OVER (ORDER BY start_date) AS Rank_Start_date
    FROM projects
    WHERE start_date NOT IN (SELECT End_date FROM projects)
),
CTE2 AS (
    SELECT end_date, RANK() OVER (ORDER BY end_date) AS Rank_End_Date
    FROM projects
    WHERE end_date NOT IN (SELECT start_date FROM projects)
)
SELECT start_date, end_date
FROM CTE1, CTE2
WHERE Rank_Start_date = Rank_End_Date
ORDER BY DATEDIFF(end_date, start_date), start_date;
