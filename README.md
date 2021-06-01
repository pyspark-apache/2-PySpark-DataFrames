# 2 PySpark DataFrames
1. [Read the dateset ](#schema1)
2. [Check the schema](#schema2)
3. [Selecting Columns And Indexing](#schema3)
4. [Selecting Columns](#schema4)
5. [Check Describe option similar to Pandas](#schema5)
6. [Adding Columns](#schema6)
7. [Dropping columns](#schema7)
8. [Renaming Columns](#schema8)
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
<hr>

<a name="schema2"></a>

# 2. Check the schema
~~~python
df_pyspark.printSchema()
root
 |-- Name: string (nullable = true)
 |-- age: string (nullable = true)
 |-- Experience: string (nullable = true)
 |-- Salary: string (nullable = true)
~~~

<hr>

<a name="schema3"></a>

# 3. Selecting Columns And Indexing
~~~python
df_pyspark.head(3)
[Row(Name='Krish', age=31, Experience=10, Salary=30000),
 Row(Name='Sudhanshu', age=30, Experience=8, Salary=25000),
 Row(Name='Sunny', age=29, Experience=4, Salary=20000)]
~~~

<hr>

<a name="schema4"></a>

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

<hr>

<a name="schema5"></a>

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

<hr>

<a name="schema6"></a>

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

<hr>

<a name="schema7"></a>

# 7. Dropping columns
~~~python
df_pyspark.drop("Experience after 2 year")
~~~

<hr>

<a name="schema8"></a>

# 8. Renaming Columns
~~~python
df_pyspark.withColumnRenamed("Name", "New_name").show()
+---------+---+----------+------+
| New_name|age|Experience|Salary|
+---------+---+----------+------+
|    Krish| 31|        10| 30000|
|Sudhanshu| 30|         8| 25000|
|    Sunny| 29|         4| 20000|
|     Paul| 24|         3| 20000|
|   Harsha| 21|         1| 15000|
|  Shubham| 23|         2| 18000|
+---------+---+----------+------+

~~~