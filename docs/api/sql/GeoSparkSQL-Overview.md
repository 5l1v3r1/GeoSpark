# Introduction

GeoSparkSQL supports SQL/MM Part3 Spatial SQL Standard. It includes four kinds of SQL operators as follows. All these operators can be directly called through sparkSession.sql("YOUR_SQL").

* Constructor: Construct a Geometry given an input string or coordinates
  * Example: ST_GeomFromWKT (string). Create a Geometry from a WKT String.
  * Documentation: [Here](./GeoSparkSQL-Constructor)
* Function:
  * Example: ST_Distance (A, B). Given two Geometry A and B, return the Euclidean distance of A and B.
  * Documentation: [Here](./GeoSparkSQL-Function)
* Aggregate function
  * Example: ST_Envelope_Aggr (Geometry column). Given a Geometry column, calculate the entire envelope boundary of this column.
  * Documentation: [Here](./GeoSparkSQL-AggregateFunction)
* Predicate
  * Example: ST_Contains (A, B). Check if A fully contains B. Return "True" if yes, else return "False".
  * Documentation: [Here](./GeoSparkSQL-Predicate)

GeoSparkSQL supports SparkSQL query optimizer, documentation is [Here](./GeoSparkSQL-Optimizer)

# Usage

1. Add GeoSpark-core and GeoSparkSQL into your project POM.xml or build.sbt
2. Declare your Spark Session
```
sparkSession = SparkSession.builder().
      config("spark.serializer",classOf[KryoSerializer].getName).
      config("spark.kryo.registrator", classOf[GeoSparkKryoRegistrator].getName).
      master("local[*]").appName("myGeoSparkSQLdemo").getOrCreate()
```
3. Add the following line after your SparkSession declaration:
```
GeoSparkSQLRegistrator.registerAll(sparkSession.sqlContext)
```
