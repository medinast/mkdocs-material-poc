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