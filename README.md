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
