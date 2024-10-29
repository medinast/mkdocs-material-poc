# Availability via Snowflake

## Overview

Snowflake is a cloud-based data warehouse that pulls in data from the various Velocity microservice databases. The Data Availability Team (DAT) uses a software called DBT as a tool to create different "views" within Snowflake. Each view in Snowflake is a SQL query that has been structured by the DAT to display various data elements in specific ways that are helpful for users when analyzing data.

Currently, views within Snowflake display data from the DBT_VELOCITY_DB database; however, there are other databases that exist outside of Velocity that are maintained by other teams (such as Analytics, Ops Analysts, etc.). There are different types of Snowflake views and each type has associated characteristics, including how often the underlying tables are refreshed with new data.

The Data Dictionary is a comprehensive database of the various data elements that live in Velocity and Snowflake with a description of each data element. Currently, the Data Dictionary exists as an Excel spreadsheet, but efforts are being made to move the Data Dictionary onto the DBT platform for various quality of life reasons, including being able to access the Data Dictionary within Snowflake.

## What is Snowflake?

Snowflake is a cloud-based data warehouse that imports data from a collection of databases that exist in PostgreSQL (Postgres) using AWS Glue and a new tool called Rivery. The Velocity platform is comprised of various microservices that all communicate using various APIs and each microservice contains a collection of tables (or small databases). Velocity has approximately 60 different microservices and corresponding databases in Postgres, which Snowflake can pull from to query different data and then present different data based on the queries.

Additionally, Snowflake currently serves as a data warehouse for entities other than just Velocity, meaning it contains a lot of other data that is not maintained specifically by the DAT. If users wish to find data or information about the other areas and tables within Snowflake, they will need to contact the owner of the specific space.
!!! note "Data Storage History"

    Velocity launched with Access Loans in 2019 and Snowflake became the preferred data warehouse for Velocity in 2021. Due to this timeline, there is approximately 1.5 years worth of data that exists in Velocity that does not exist in Snowflake at this time. There is an old RDS environment (Redshift Postgres) that acted as a temporary solution prior to adopting Snowflake that is still active and houses this older data as well.

    The earliest records in Snowflake have a timestamp of around March of 2021.

## What is DBT?

DBT is the software that the Data Availability Team uses as a development environment. Each view that is created by the DAT, and then used by Nelnet users in Snowflake, is developed in DBT. DBT interfaces with Github, allowing the team to use all of the quality of life features that Github has to offer.

DBT also acts as a data transformation tool, allowing users to take source data and model it in ways that materialize different views and tables. So, while the DAT uses it primarily for creating and developing different views, its functionality goes beyond simply creating different views.

Additionally, DBT serves as the central location for all of the Data Availability Team's column-level documentation. This documentation is currently being added as the DAT touches each column and/or works on new tickets and projects.

To learn more about DBT, you can visit the DBT website.

## What is the Data Dictionary?

The Data Dictionary is a project with the primary goal of providing helpful descriptions for all of the various data elements that exist within Velocity today. For example, if a user were to query one of the Velocity APIs and was returned a JSON payload full of data, the Data Dictionary could be used to look up the different data element names and their descriptions.

While the Data Dictionary currently exists in Excel spreadsheets, there are efforts underway to move the existing data element descriptions into a DBT repository. Doing this would centralize the Data Dictionary for all users, allow data element descriptions to be updated in a live database, allow Snowflake users to access the Data Dictionary within Snowflake, and allow DBT users to see the relationships between data elements and the different views they are used in (otherwise known as their lineage).

## Snowflake Views and Table Refresh Times

!!! info
    The views in Snowflake are non-materialized, meaning each view will re-run the SQL query that generates it and display the current data when called.<br><br>Creating Snowflake views is necessary because people need to see the various pieces of data without having access to the actual tables where the data is housed.
    
| View / Type Name | Scheduled Table Refresh Times | Description |
| ---------------- | ----------------------------- | ----------- |
| **(VW)** View        | Financial data updates as new data comes in from Velocity.<br>Non-financial data updates during the scheduled table refresh times.<br><br>**Starts**: 5:00a UTC / 11:00p CST<br>**Ends**: 11:20a UTC / 5:20a CST     | Views that have "VW" in their name represent queries that are pulling data in near real-time. The data in these views are updated as the data in Velocity changes.<br><br>Non-financial related data changes (ie. address changes, phone number changes, e-correspondence/SCRA status changes, etc.) do not update automatically when changes to those pieces of data are made in Velocity. Changes to these pieces of information will only update in the Snowflake views during the refresh cycle each morning.             |
| **(DS)** Daily snapshot | **Starts**: 5:00a UTC / 11:00p CST<br>**Ends**: 11:20a UTC / 5:20a CST | Views that have "DS" in their name represent queries that are snapshotting data elements at a scheduled time, meaning the information is going to be accurate as of the time it was last queried. These views are built from AWS Glue (and Rivery) tables brought over nightly. |
| **(RP)** Reports | **Starts**: 5:00a UTC / 11:00p CST<br>**Ends**: 11:20a UTC / 5:20a CST | Views that have "RP" in their name are reporting views based off of "VW" and "DS" views. |
| **(CRP)** Citizens reports | **Starts**: 5:00a UTC / 11:00p CST<br>**Ends**: 11:20a UTC / 5:20a CST | Views that have "CRP" in their name are the same as "RP" views, but are specific to Citizens. |