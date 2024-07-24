# Data Faker using Python

If your wondering what this repository is about, it is all about creating faka data for your experiments using python. This repository contains a python script which you can use to create data in csv format. Furthermore there is an sql script which you can use to insert the data fetched into Postgres.

## Prerequisites
1. Python - 3.7+ (I used 3.10 for this script) - [Use this](https://realpython.com/intro-to-pyenv/)
2. Postgres Database setup - [Use this](https://www.postgresql.org/docs/current/tutorial-install.html) - Ignore this if you are only planning to fetch CSV or you are planning to write a acript yourself

**Note:** I have used `python` and `pip`. But use `python3` and `pip3` if your installed python demands so.

## Basic Setup - from Mac/Ubuntu perspective
1. Open Terminal - *Terminal Python*
2. Run `git clone https://github.com/NichuSPN/Data-Faker-Python.git` in the directory of your choice
3. Run `cd Data-Faker-Python` to enter into the directory
4. Run `pip install -r requirements.txt` to install all required packages
5. Open another Terminal - *Terminal SQL*
7. Go into `Data-Faker-Python/data` folder
6. Run `psql` command to connect to the postgres db of your choice

## Navigating through code
### Python Code
This example contains employee information generation code. We are generating name, age, salary, department and email. For generating name and email we use a library called `faker` which is used to generate fake data for experimentations. For generating age, salary and department we use a library named `random`.
Change the ROWS count and add or remove columns based on your usecase

### SQL Script
With the generated CSV we now use the script to insert it into the postgres table of our choice. Now we will see how this script works so that you can modify it based on your usecase
- We create 2 tables `employees_temp` and `employees` where `employees` is my main table and `employees_temp` as the name suggests is a temporary table which we will use to get the initial data into. 
- The temp table is used because my main table has a primary key and there is no way to handle conflict when we copy data from csv to a table. That is the reason we have a temp table and insert into the main table from here
- We first insert the data from CSV into `employees_temp` using `\copy` command and then from that table we insert the data into `employees` where on conflict on primary key, we ignore the incoming data
- Drop the temp table once the insertion is done

## How to run?
Once you confirm that the parameters and queries are correct in both the scripts, follow the below steps to run both the scripts
1. In *Terminal Python* run `python main.py` - This creates the csv file in `data` folder
2. In *Terminal SQL* run `\i script.sql` - This runs the SQL script and copies data from the created csv into the table needed