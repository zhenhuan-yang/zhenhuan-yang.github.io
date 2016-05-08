---
layout: single
title: "Datums: A PostgreSQL Pipeline for Reporter"
modified:
categories: projects
excerpt:
tags: [python, sqlalchemy, postgres, reporter, data]
date: 2015-04-12T13:37:43-04:00
share: false
---
[Reporter](http://www.reporter-app.com/) is an iPhone application that will ping you randomly throughout the day with a survey of questions designed by you. Among others, Reporter is used by [@georgialupi](https://twitter.com/giorgialupi) and [@stefpos](https://twitter.com/stefpos) in their project [Dear Data](http://www.dear-data.com/).   

I started using Reporter because I'm anxious. At first, I just had Reporter ask me how anxious I was on a scale of 1 to 10. That was it. The trend was interesting (there was a time when it looked like a perfect sine wave), but the numbers by themselves, as you probably could've guessed, are little better than meaningless. So I started adding questions: Where are you? Who are you with? What are you working on? What tools are you using? Did you have sex today? (My full survey is [below](#survey).)  

After about a year, I had amassed enough reports that I was ready to go [Feltron](http://feltron.com/) on myself.[^1] I have Reporter set up to automatically export your data as JSON to a folder in Dropbox, and I needed an easy way to get the data into PostgreSQL because KEEP CALM AND JUST ALWAYS USE POSTGRES.

So I built [Datums](https://www.github.com/thejunglejane/datums). Datums is a pipeline for Reporter that will take the JSON files exported by Reporter and load them into a PostgreSQL database. The datums data model is defined using the [SQLAlchemy ORM](http://www.sqlalchemy.org/), and the datums library handles adding, updating, and deleting reports. The datums command line tool makes it super easy to insert records in batches. I have a cron job that runs every morning that inserts the reports from the day before with  

`yesterday=$(date -v -1d +"%Y-%m-%d")`  
`datums --add $REPORTER_PATH/$yesterday-reporter-export.json`

You can download and install datums from [github](https://www.github.com/thejunglejane/datums).

### Survey

##### Wake
+ How anxious are you? (Number)

##### Day
+ How anxious are you? (Number)
+ How happy are you? (Number)
+ How tired are you? (Number)
+ Where are you? (Location)
+ Who are you with? (People)
+ What are you doing? (Tokens)
+ What are you working on, making, or building? (Tokens)
+ What tools are you using? (Tokens)
+ What are you reading? (Tokens)
+ What are you writing? (Tokens)
+ What are you listening to? (Tokens)
+ What are you watching? (Tokens)
+ What are you cooking? (Tokens)
+ What are you eating? (Tokens)
+ What are you drinking? (Tokens)

##### Sleep
+ Are you on your period? (Yes/No)
+ Did you do this today? (Multiple choice)
    + Exercise
    + Meditate
    + Have sex
    + Drink
    + See art
    + Take iron[^2]


[^1]: Nicholas Felton helped build Reporter.
[^2]: I’m pretty anemic, and whether or not I take iron seems to have a big impact on how tired I am. Things you learn when you use Reporter.
