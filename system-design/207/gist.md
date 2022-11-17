To handle trillions of data points and petabytes of data every single day, Discord needs a simple yet robust Data Platform.

Here's a quick overview of their arch and key design decisions 👇‍

## What is a Data Platform?

A data platform comprises a set of services that ensures data is replicated from various databases, put in central storage, and making it available for consumption by internal teams, and services.

Discord needs to analyze the data to

- make strategic business decisions
- power their machine learning models
- understand how people are using their product

### Why replicate data in one place?

- data is split across microservices
- firing queries that span multiple databases infeasible
- each microservice has its own flavor of database (SQL and NoSQL)

For example, firing queries across orders (MongoDB) and payments (MySQL) to get the items that generated the most revenue.

## Discrod's Data Platform - Derived

Discord uses Google's BigQuery as its Data Warehouse (a place to keep and query large volumes of data). The data is stored, processed, and consumed across 3 layers

1. Transactional Layer
2. Core Tables
3. Derived Tables

Let's understand each layer in detail.

### Transactional Layer

The transactional layer comprises the transactional databases used in powering the microservices. These databases typically act as a source of truth for the services.

Microservices are free to choose the flavor of the database - SQL or NoSQL to power their usecase.

### Core Tables

The core layer holds the series of tables in BigQuery that are populated using the transactional layer.

Data pipelines replicate the data from various transactional databases, like MongoDB, MySQL, etc into a set of structured core tables, and become the input for the subsequent Derived Layer.

### Derived Tables

Derived Tables are the actual consumable tables created from a set of core tables. Each team can create its own set of derived tables by joining a set of core tables as per their need.

Each derived table is essentially a SQL query on core tables. The specified SQL query is fired periodically to join and replicate the unprocessed data into a derived table.

Each derived table has its own configuration file that holds

- columns of the derived table
- schedule and window
- partition key, cluster key,
- dataset and SQL query

A replication strategy is also specified in the YAML file that implies if the output of the SQL query should append to, merge with, or replace the existing derived data.

A separate K8S pod is run for each derived table that ensures an isolated continuous data replication to the derived tables.

Thus, each team can define its own set of derived tables using just a SQL query, enabling teams to make data-driven decisions.