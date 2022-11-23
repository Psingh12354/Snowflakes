<h1 align='center'>Snowflakes</h1>

### Snowflake

Developed in 2012, Snowflake is a fully managed SaaS (software as a service) that provides a single platform for data warehousing, data lakes, data engineering, data science, data application development, and secure sharing and consumption of real-time / shared data.  A Snowflake database is where an organization’s uploaded structured and semistructured data sets are held for processing and analysis. Snowflake automatically manages all parts of the data storage process, including organization, structure, metadata, file size, compression is done automatically, and statistics. Snowflake optimizes and stores data in a columnar format within the storage layer, organized into databases as specified by the user.

### Snowflake Architecture
Snowflake's architecture is a hybrid of traditional shared-disk and shared-nothing database architectures. Similar to shared-disk architectures, Snowflake uses a central data repository for persisted data that is accessible from all compute nodes in the platform. **Shared-disk** architecture snowflakes use central data repo to make it accessible from all computer nodes. **Shared-nothing-architecture** it use for MPP(massively parallel processing). The combo offere data management simplicity of shared-disk and performance of scale-out.

### Columnar db
A columnar database is a database management system (DBMS) that stores data in columns instead of rows. The purpose of a columnar database is to efficiently write and read data to and from hard disk storage in order to speed up the time it takes to return a query.

### AWS VS SNOWFLAKES

Snowflake is different from AWS in the sense that it does not provide a comprehensive set of services. Snowflake is a relational database management system (RDBMS) that can be used to store data. AWS, on the other hand, provides a wide range of services, such as compute, storage, networking, and applications.
