## Spark Session -04  

-- All the remaining concepts of spark will be continued while pratical execution.  
-- to launch the spark, go to neuro lab and select pyspark + hadoop  
-- **There are 2 ways, in which we try to run our spark applications:-**  
                                                              1. In Devlopment  
                                                              2. In Production  
-- **URL to view data in UI:**  
Spark Master - <your_app_name>.ineuron.app:8080  (basically spark runs at port 7077 in neuro-lab, spark master is just a port mapping)  

History Server - <your_app_name>.ineuron.app:18080

Spark Worker Node - <your_app_name>.ineuron.app:8081

**for eg.:-** https://purple-electrician-aszai.ineuron.app:8080/
-------------------------------------------------------------------------------------------------------------------------------

We can use the pyspark utility to submit our application to the nodes.
we can use the pyspark shell to run our application in the development phase.

In the industry also, we get the environment like neuro-lab, means we will be getting some access to the machines where our spark
is installed. We generally connect to that machines and run our code on pycharm or vs-code.
After making our production grade application, we publish our application to the github, and from there we might use container
and airflow.
To connect to pyspark we can either run the spark shell where we can run our commands interpreted manner(1 command runs at 1 time).
We can also connect to the spark with python using some drivers.

----------------------------------------------------------------------------------------------------------------------------------

**Ques. Do we need to create any session in the spark session in the cli??**  
Ans.    No, spark session automatically gets created when we runs the command <pyspark> in the pyspark shell.  


**Ques. whenever we run the command <pyspark>, in the cli, we can see that the master = local[*] is mentioned,  
but whenever we create a spark session via code, we try to mension the master = 'spark://localhost:7077' something like this? explain.**  
Ans.  This is because, when we run a spark commands on the cli the job is not submitted on the spark-cluster, meanwhile it is submitted
      on the our local machine.  
      due to the spark cli, our machine which may be suppose 8 cores, is converted to a stand-alone spark cluster. 
      so, when we run our spark jobs on the cli, it can manage small data let say (500mb-800mb) etc.  
      In the spark cli also we can read our data from hdfs in the distributed manner,  
      and suppose if we apply any transformation like group by etc. it will also happen in the distributed manner.  
      so we can change this star to any integer, so that all our cores are not used.  

-- if we don't have any data, we can even create our own data and define a schema on top of it.  
-- for this we need to import a library and we can also define the datatype there:-  
  from pyspark.sql.types import StructType,StructField, StringType, IntegerType
  
**Struct:-** it is a custom datatype(mainly from the c,c++), which is a combination of multiple data-type.
  
  ### import necessary module
  from pyspark.sql.types import StructType,StructField, StringType, IntegerType  
      person_list = [("Berry","","Allen",1,"M"),
        ("Oliver","Queen","",2,"M"),
        ("Robert","","Williams",3,"M"),
        ("Tony","","Stark",4,"F"),
        ("Rajiv","Mary","Kumar",5,"F")
    ]  
  
  ### define a schema on top of our data, even we can define the schema if we are reading a csv file and it does not have a header.  
  
  -- here True means nullable = True.  
  
  
  schema = StructType([
        StructField("firstname",StringType(),True),  
        StructField("middlename",StringType(),True),  
        StructField("lastname",StringType(),True),   
        StructField("id", IntegerType(), True),  
        StructField("gender", StringType(), True)])    
  
    ### creating spark dataframe  
    df = spark.createDataFrame(data=person_list,schema=schema)  
  
   ### df.show() is an action.  
   if we use df.show(truncate = False) .. it will forcefully show all the records.  

 **df.printSchema()**
