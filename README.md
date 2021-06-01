# 2 PySpark-DataFrames
1. [Read the dateset ](#schema1)

<hr>

<a name="schema1"></a>

# 1. Read the dateset
~~~python
df_pyspark = spark.read.option("header", "true").csv("./data/test1.csv")
~~~
Another way
~~~python
df_pyspark = spark.read.csv("./data/test1.csv", header = True, inferSchema = True)
~~~

# 2. Check the schema
~~~python
df_pyspark.printSchema()
root
 |-- Name: string (nullable = true)
 |-- age: string (nullable = true)
 |-- Experience: string (nullable = true)
 |-- Salary: string (nullable = true)
~~~

# 3. Selecting Columns And Indexing
~~~python
df_pyspark.head(3)
[Row(Name='Krish', age=31, Experience=10, Salary=30000),
 Row(Name='Sudhanshu', age=30, Experience=8, Salary=25000),
 Row(Name='Sunny', age=29, Experience=4, Salary=20000)]
~~~

# 4. Selecting Columns
~~~python
df_pyspark.select('Name').show()
+---------+
|     Name|
+---------+
|    Krish|
|Sudhanshu|
|    Sunny|
|     Paul|
|   Harsha|
|  Shubham|
+---------+

df_pyspark.select(['Name','Experience']).show()
+---------+----------+
|     Name|Experience|
+---------+----------+
|    Krish|        10|
|Sudhanshu|         8|
|    Sunny|         4|
|     Paul|         3|
|   Harsha|         1|
|  Shubham|         2|
+---------+----------+

~~~

# 5. Check Describe option similar to Pandas

~~~python
df_pyspark.dtypes
[('Name', 'string'), ('age', 'int'), ('Experience', 'int'), ('Salary', 'int')]

df_pyspark.describe().show()
+-------+------+------------------+-----------------+------------------+
|summary|  Name|               age|       Experience|            Salary|
+-------+------+------------------+-----------------+------------------+
|  count|     6|                 6|                6|                 6|
|   mean|  null|26.333333333333332|4.666666666666667|21333.333333333332|
| stddev|  null| 4.179314138308661|3.559026084010437| 5354.126134736337|
|    min|Harsha|                21|                1|             15000|
|    max| Sunny|                31|               10|             30000|
+-------+------+------------------+-----------------+------------------+
~~~

# 6. Adding Columns
~~~python
df_pyspark.withColumn("Experience after 2 year", df_pyspark["Experience"]+2).show()
+---------+---+----------+------+-----------------------+
|     Name|age|Experience|Salary|Experience after 2 year|
+---------+---+----------+------+-----------------------+
|    Krish| 31|        10| 30000|                     12|
|Sudhanshu| 30|         8| 25000|                     10|
|    Sunny| 29|         4| 20000|                      6|
|     Paul| 24|         3| 20000|                      5|
|   Harsha| 21|         1| 15000|                      3|
|  Shubham| 23|         2| 18000|                      4|
+---------+---+----------+------+-----------------------+

~~~

# 7. Dropping columns
~~~python
df_pyspark.drop("Experience after 2 year")
~~~

# 8. Renaming Columns
~~~python
df_pyspark.withColumnRenamed("Name", "New_name").show()
~~~