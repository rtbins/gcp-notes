# DAT229x Introduction to Big Data

## Introduction to Data

- lots of way to generate data, smart speakers, video games etc
- need is to capture and bring this data together to a same place
- **Data formats**

  - Text data (unstructured), hard to process them in a structured format
  - Delimited text (csv, tab delimited)
  - XML, parent-child relationship, hierarchical relationship
  - JSON, less text compared to xml, efficient way to send data over network

- **Encoding**

  - Reading and writing in consistent encoding makes sure that we don't loose the data while moving it.
  - file formats that are optimized for high performance in the distributed storage and processing environments typical of big data scenarios

    - To learn about the Avro format, see <http://avro.apache.org/>.
    - To learn about the ORC format, see <https://orc.apache.org/>.
    - To learn about the Parquet file format, see <https://parquet.apache.org/>

- Data files in Azure

  - allows to store blobs and access them.
  - azure data lake store, massive quantity of data, allows permissions to be set at different folder hierarchy.
  - containers are like disk volumes
  - block blob allows file to be split and makes it easy to transfer it over network.
  - To learn more about Azure Storage, see the documentation at <https://docs.microsoft.com/en-us/azure/storage/index>.
  - To learn more about Azure Data Lake Store, see <https://docs.microsoft.com/en-us/azure/data-lake-store/index>.
  - azure-cli <https://docs.microsoft.com/en-us/cli/azure/get-started-with-azure-cli>

- Relational database

  - Azure sql db requires a azure sql server
  - datawarehouses has de-normalized form of the data
  - Azure DataWarehouses has ability to dynamically scale based on the workloads.

- NoSql database

  - flexible schema
  - key-value pair
  - value can be text type, string, json or a table object
  - Azure table storage, achieves scalability by partitioning the data, _partition key_ and _row key_
  - Azure cosmos db, API (to deal with different data)
  - JSON data, Azure cosmos document db and mongo db
  - Graph database
  - Cosmos DB documentation at <https://docs.microsoft.com/en-us/azure/cosmos-db/>.

- Big Data

  - High volume
  - Many varities
  - High velocity
