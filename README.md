<p align="center">
  <a href="" rel="noopener">
 <img width=500px height=100px src="https://docs.delta.io/latest/_static/delta-lake-logo.png" alt="Project logo"></a>
</p>

<h3 align="center">Delta lake is an open-source project that enables building a Lakehouse architecture on top of existing storage systems such as S3, ADLS, GCS, and HDFS.</h3>

<div align="center">

[![Status](https://img.shields.io/badge/status-active-success.svg)]()
[![License](https://img.shields.io/badge/license-MIT-blue.svg)](/LICENSE)

</div>

---

## 📝 Table of Contents

- [About](#about)
- [Architeture](#architeture)
- [Usage](#usage)
- [Built Using](#built_using)
- [Authors](#authors)

## 🧐 About <a name = "about"></a>

This project aims to make a simple etl processing, using pyspark with the deltalake framework. The work of pyspark will consume a filesystem titled landing-zone with files in json format. We will use some time travel techniques, writing in delta format for table management control and much more.

## 🔧 Architeture ELT Delta lake <a name = "architeture"></a>

![image](https://live-delta-io.pantheonsite.io/wp-content/uploads/2019/04/Delta-Lake-marketecture-0423c.png)


 work reads data from a filesystem called landing-zone using deltalake dependencies, which are jar packages that are in spark's session config, with which it is possible to use the delta lake framework. after the execution of this script, the data will be written in the directory passed in code, inside the write table will be written a directory called _delta_log, which is responsible for storing incremental files on table metadata, it will be something like
00000000000000000000.json, 0000000000000000000001.json...
Json file under the _delta_log folder will have the information like add/remove parquet files(for Atomicity), stats(for optimized performance & data skipping), partitionBy(for partition pruning), readVersions(for time travel), commitInfo(for audit).

![image](https://miro.medium.com/max/1400/0*5XnRRdbrbuuNGFzJ.png)

reads the data in delta format, which results in a performance gain due to being stored in parquet format and having one of the great advantages of _delta_log metadata management, steps are performed processing in which unnecessary columns are removed and preparation of tables with join for MDW modeling with data normalized in dataset formats.

has the responsibility of enriching the data, in this process it is where we treat the data and refine it to the business area or who will consume the data, in this script I left the example of how to use the time travel using parameter passed in the function that we declared .option("versionAsOf", "0"), below are images after ingestion


This project aims to make a simple etl processing, using pyspark with the deltalake framework. The work of pyspark will consume a filesystem titled landing-zone with files in json format. We will use some time travel techniques, writing in delta format for table management control and much more.

## 🔧 Upserts Delta Lake <a name = "deltalake"></a>

![image](https://i.ytimg.com/vi/R4f6SKOetB4/maxresdefault.jpg)

How the Delta Lake Upserts logic works and how we can make the adoption of the new and modern Lake House Architecture, for this I made available a notebook jupyter, in which we read data in format json, which are related to users of a system. Our main goal is to read these files in Json format and convert them to a Delta Table. After that we can access metadata that is generated inside a directory called _delta_log, which we can access through the DeltaTable.forPath method. After instantiating the Delta Table, we managed to merge the new data using whenMatchedUpdateAll using the condition that we are going to compare and finally update our Delta Table.

## ⛏️ Built Using <a name = "built_using"></a>

- [Pyspark](https://spark.apache.org/docs/latest/api/python/index.html) - 3.1.1
- [Deltalake](https://docs.delta.io/latest/quick-start.html) 

## ✍️ Authors <a name = "authors"></a>

- [@carlosbpy](https://github.com/carlosbpy) - Idea & Initial work