<h1 align='center'>Snowflakes</h1>

### Snowflake

Developed in 2012, Snowflake is a fully managed SaaS (software as a service) that provides a single platform for data warehousing, data lakes, data engineering, data science, data application development, and secure sharing and consumption of real-time / shared data.  A Snowflake database is where an organization’s uploaded structured and semistructured data sets are held for processing and analysis. Snowflake automatically manages all parts of the data storage process, including organization, structure, metadata, file size, compression is done automatically, and statistics. 

- In layman snowflake is a tool which is to perform operation on structured and semi-structured data which is sitting on a cloud.
- It follow mult-clustered shared architecture.
- Snowflake support standard sql
- Snowflake optimizes and stores data in a columnar format within the storage layer, organized into databases as specified by the user.
- We have 2 types of Architecture-: 
  - Shared-disk architecture **-:** There is multiple compute node connected to 1 centralized database.
  - Shared-nothing architecture **-:** All compute node have it's own database so they shared nothing with other compute node.

### Snowflake Architecture [Refer](https://hevodata.com/blog/snowflake-architecture-cloud-data-warehouse/)
Snowflake's architecture is a hybrid of traditional shared-disk and shared-nothing database architectures. Similar to shared-disk architectures, Snowflake uses a central data repository for persisted data that is accessible from all compute nodes in the platform. **Shared-disk** architecture snowflakes use central data repo to make it accessible from all computer nodes. **Shared-nothing-architecture** it use for MPP(massively parallel processing). The combo offere data management simplicity of shared-disk and performance of scale-out.
![](https://res.cloudinary.com/hevo/images/f_auto,q_auto/v1591729876/hevo-blog/Snowflake-Architecture-3/Snowflake-Architecture-3.png?_i=AA)

- Storage layer is the central area where all data is stored including(view and schema).
- In compute layer we create **virtual warehouses** to connect the deployement like if connected to gcp it use gcp.
- Virtual warehouse is the place where query is executed.
- Service layer manage end-to-end operations on security, metadata management and optimization.
- Service layer arch-:
  - Authenicaiton-: check for the legitimate user.
  - Manager-: The one who manage all task warehouse. 

### Columnar db
A columnar database is a database management system (DBMS) that stores data in columns instead of rows. The purpose of a columnar database is to efficiently write and read data to and from hard disk storage in order to speed up the time it takes to return a query.

### AWS VS SNOWFLAKES

Snowflake is different from AWS in the sense that it does not provide a comprehensive set of services. Snowflake is a relational database management system (RDBMS) that can be used to store data. AWS, on the other hand, provides a wide range of services, such as compute, storage, networking, and applications.

### Data loading 
- Bulk load.
  - It copy command which use for batch processing.
  - Batch loading already available in cloud storage or interna l storage
  - Copy command use virtual warehouse which need to manage manually
  - Allow basic transformations such as re-ordering columns, excluding columns, data typing, truncations string.
  - COPY INTO command is common mechanism to load data in bulk in snowflakes.
  
- Continuous Load-:
  - Snowpipe use for loading streaming data
  - Uses a serveless architecture scalling is automatic.
  - Doesn't use the virtual warehouse compute resources.
  
- External Tables (Data Lake)
  - External tables enable querying existing data stored in external cloud storage for analysis without first loading it into Snowflake. The source of truth for the data remains in the external cloud storage. Data sets materialized in Snowflake via materialized views are read-only.

### Continuous Loading Using Snowpipe
- Real time data update
- Snowpipe uses compute resources provided by Snowflake (i.e. a serverless compute model). These Snowflake-provided resources are automatically resized and scaled up or down as required, and are charged and itemized using per-second billing. Data ingestion is charged based upon the actual workloads.

### Time Travel

In snowflakes we can undo the accidental changes upto 90days in enterprise edition and 1 day in standard edition.
- UTC(Universal Coordinate time)
**example**
```
-- undropping a table
DROP TABLE CUSTOMER;
SELECT * FROM CUSTOMER;

UNDROP TABLE CUSTOMER;
SELECT * FROM CUSTOMER;
SELECT COUNT(*) FROM CUSTOMER;

-- undropping a schema
DROP SCHEMA PROD_CRM.PUBLIC;
SELECT * FROM CUSTOMER;

UNDROP SCHEMA PROD_CRM.PUBLIC;
SELECT * FROM CUSTOMER;
SELECT COUNT(*) FROM CUSTOMER;

-- undropping a database
DROP DATABASE PROD_CRM;
SELECT * FROM CUSTOMER;

UNDROP DATABASE PROD_CRM;
SELECT * FROM CUSTOMER;
SELECT COUNT(*) FROM CUSTOMER;
```
### Metadata [Refer](geeksforgeeks.org/metadata-in-dbms-and-its-types/)
Metadata is simply defined as data about data. It means it is a description and context of the data. It helps to organize, find and understand data.

### FailSafe Sql
```

-- you can check storage usage through the ACCOUNT_USAGE.STORAGE_USAGE
-- view which will give you information about storage used by data,
-- storage used by internal stages & storage used by failsafe

SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.STORAGE_USAGE ORDER BY USAGE_DATE DESC;

-- let's convert the above information into GBs
SELECT 	USAGE_DATE, 
		STORAGE_BYTES / (1024*1024*1024) AS STORAGE_GB,  
		STAGE_BYTES / (1024*1024*1024) AS STAGE_GB,
		FAILSAFE_BYTES / (1024*1024*1024) AS FAILSAGE_GB

FROM SNOWFLAKE.ACCOUNT_USAGE. ORDER BY USAGE_DATE DESC;



-- You can also check on failsafe storage usage by querying the 
-- TABLE_STORAGE_METRICS view
SELECT * FROM SNOWFLAKE.ACCOUNT_USAGE.TABLE_STORAGE_METRICS;

--let's improve the result & convert to GBs as well
SELECT 	ID, 
		TABLE_NAME, 
		TABLE_SCHEMA,
		ACTIVE_BYTES / (1024*1024*1024) AS STORAGE_USED_GB,
		TIME_TRAVEL_BYTES / (1024*1024*1024) AS TIME_TRAVEL_STORAGE_USED_GB,
		FAILSAFE_BYTES / (1024*1024*1024) AS FAILSAFE_STORAGE_USED_GB
	
	
FROM SNOWFLAKE.ACCOUNT_USAGE.TABLE_STORAGE_METRICS
	
ORDER BY STORAGE_USED_GB DESC,TIME_TRAVEL_STORAGE_USED_GB DESC, FAILSAFE_STORAGE_USED_GB DESC;
```

### Zero Copy Cloning
- Cloning is the process of creating exact copy of data, metadata operation doesn't actually copy the data it take a snapshot and modification of original and clone table are independent to each other.
