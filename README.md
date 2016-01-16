# CMPE-272-Spark-Project
 Extracting Genes responsible for Breast Ovarian Cancer from ClinVar Datasets Using IBM Spark

Step by Step Explanation of work done in project :

Link of Dataset Used: 
http://www.ncbi.nlm.nih.gov/clinvar/?term=breast                                                                                      

Step 1: Entry Point for Spark:                                                                                                        
from pyspark.sql import SQLContext, Row                                                                                               
sqlContext = SQLContext(sc)                                                                                                           
Step 2: Reading data  from CSV  file                                                                                                  
lines = sc.textFile("swift://notebooks.spark/clinvar_result_Final.csv");                                                              
Step 3: Extracting data as required                                                                                                   
parts = lines.map(lambda l: l.split(","))                                                                                             
gene = parts.map(lambda p: Row(name=p[1]))                                                                                            
Step 4: Creating Schema                                                                                                             
schemaGene = sqlContext.createDataFrame(gene)                                                                                         
schemaGene.registerTempTable("gene")                                                                                                  
Step 5: Extracting distinct genes name responsible for Breast-Ovarian cancer                                                          
geneName = sqlContext.sql("SELECT distinct(name) FROM gene")                                                                          
Step 6: Printing Data as Ouput :                                                                                                      
Words=[]                                                                                                            
name = geneName.map(lambda p: p.name)                                                                                                 
for name1 in name.collect():                                                                                                          
    b_1=name1.split('|')                                                                                                            
    for uniqueWord in b_1:                                                                                                            
      if not uniqueWord in Words:                                                                                                     
          print str(uniqueWord);                                                                                                                                                                                                                
Please follow the below steps to setup the project in IBM Bluemix:

Step 1 : Download ClinVar dataset from this Path :

http://www.ncbi.nlm.nih.gov/clinvar/?term=breast

Step 2 : Create a Apache Spark Service in IBM Bluemix.

Step 3 : Upload attached "python_test.ipynb" as Notebook in your service

Step 4 : Create a Object Storage in the same Apache Spark Service Instance and add the upload the clinVar dataset downloaded from :

http://www.ncbi.nlm.nih.gov/clinvar/?term=breast

Step 5 : In notebook,wait for kernel to get start,once kernel get start,do step by step execution of the program.


Note : Change your dataset name accordingly, I have used it as clinvar_result_Final.csv 

