# **Problem Statement 2**

> Methods and solutions are well explained here. Highly recommended to go through `Readme.md` to understand the methods and solutions of the project.

## Introduction

As a data analysis intern, you have to analyse sports data for a client. You are given two datasets related to IPL (Indian Premier League) cricket matches. One dataset contains ball-by-ball data and the other contains match-wise data. You have to import the datasets into an SQL database and perform the tasks given in this assignment to find important insights from this dataset.

## *_Quick Access_*

**DataSets**

[IPL_matches.csv](https://github.com/rh540640/Sports-Analytics/blob/master/IPL_matches.csv)

[IPL_Ball.csv](https://raw.githubusercontent.com/rh540640/Sports-Analytics/master/IPL_Ball.csv)


**Code**

[sports_data_analytics.sql](https://github.com/rh540640/Sports-Analytics/blob/master/sports_data_analytics.sql)

**Read File**

[Readme.md](https://github.com/rh540640/Sports-Analytics/blob/master/Readme.md)


## About the Data

Download Postgres sql: https://www.postgresql.org/

#### The "IPL_Ball.csv" file is for ball-by-ball data and it has information of all the 19,3468 balls bowled between the years 2008 and 2020. It has 17 columns.
#### The "IPL_matches.csv" file contains match-wise data and has data of 816 IPL matches. This table has 17 columns.
---------------------------------------------------------------------------------------------
## **Project**

### *__Prerquisites before solving the problem statement__*


* Creating a database in postgre Commandline Client
```sql
CREATE DATABASE ipl;
```
* Using the database

use ipl;


**1. Create a table named `matches` with appropriate data types for columns.**

`id` is used as `PRIMARY KEY` here
`
CREATE TABLE matches(
    id INT PRIMARY KEY,
    city VARCHAR(40),
    date DATE,
    player_of_match VARCHAR(40),
    venue VARCHAR(80),
    neutral_venue INT,
    team1 VARCHAR(80),
    team2 VARCHAR(80),
    toss_winner VARCHAR(80),
    toss_decision VARCHAR(20),
    winner VARCHAR(80),
    result VARCHAR(40),
    result_margin INT,
    eliminator VARCHAR(10),
    method VARCHAR(10),
    umpire1 VARCHAR(40),
    umpire2 VARCHAR(40)
);

Then describe the table.

DESCRIBE matches;

![Alt text](describe_matches.png)

**2. Create a table named `deliveries` with appropriate data types for columns.**

Here `id` is used as a `FOREIGN KEY`.


CREATE TABLE deliveries (
    id INT,
    inning INT,
    over INT,
    ball INT,
    batsman VARCHAR(40),
    non_striker VARCHAR(40),
    bowler VARCHAR(40),
    batsman_runs INT,
    extra_runs INT,
    total_runs INT,
    is_wicket INT,
    dismissal_kind VARCHAR(40),
    player_dismissed VARCHAR(40),
    fielder VARCHAR(40),
    extras_type VARCHAR(40),
    batting_team VARCHAR(40),
    bowling_team VARCHAR(40),
     FOREIGN KEY(id) REFERENCES matches(id)
);

Describing the Table.

DESCRIBE deliveries;

![Alt text](describe_deliveries.png)

**3. Import data from CSV file 'IPL_matches.csv' attached in resources to `matches`.**



![Alt text](check_directory.png)

* Apply show all hidden files > search the directory in pc > paste the files in the directory.
Right click on Table name -
1.Importing 'IPL_matches.csv'.
2. Select import/export
3. Give your file name



![Alt text](import_ipl.png)

**4. Import data from CSV file ’IPL_Ball.csv’ attached in resources to ‘deliveries’**


Right click on Table name -
1.Importing 'IPL_matches.csv'.
2. Select import/export
3. Give your file name
![Alt text](import_ball.png)

**5. Select the top 20 rows of the deliveries table.**


SELECT * FROM deliveries
LIMIT 20;
![Alt text](limit20_deliveries.png)

**6. Select the top 20 rows of the matches table.**


SELECT * FROM matches
LIMIT 20;


![Alt text](limit20_matches.png)

**7. Fetch data of all the matches played on 2nd May 2013.**


SELECT * FROM matches
WHERE date = '2013-05-02';

![2013-05-02](https://user-images.githubusercontent.com/106378212/173740430-6b1755c6-9a7f-4dea-a2b1-e9a3df390384.png)

**8. Fetch data of all the matches where the margin of victory is more than 100 runs.**


SELECT * FROM matches
WHERE result_margin > 100;

![Alt text](resultmargin_100.png)

**9. Fetch data of all the matches where the final scores of both teams are tied and order it in descending order of the date.**


SELECT * FROM matches
WHERE result = 'tie'
ORDER BY date DESC;

![Alt text](tie_desc.png)

**10. Get the count of cities that have hosted an IPL match.**

SELECT COUNT(DISTINCT city) 
FROM matches;


![Alt text](count_city.png)

**11. Get the count of venues that have hosted IPL matches.**


SELECT COUNT(DISTINCT venue)
FROM matches;

![Alt text](count_venue.png)








