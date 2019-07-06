#  Build massive and lightning-fast analytics solutions with Azure Data Explorer  
 
 Looking to help your customers make business decisions with immediate impact based on real-time terabyte/petabyte of data in seconds? In this session, you will build a near-real-time analytical solution with Azure Data Explorer (ADX), which supports interactive adhoc queries of terabyte/petabyte data.  
 
 Walk away with a solution for your frustrated customers, so they can make immediate and impactful business decisions from their data using ADX.  
 
**Contents**
 
 <!-- TOC -->

- [Infrastructure](#Infrastructure) 
- [Ingestion](#Ingestion) 
- [Exploration](#Exploration)
 - [Questions](#Questions)  
 - [KQL](#KQL) 
 - [Results](#Results)
- [Self-Study](#Self-Study)    
  - [Kusto Query Language (KQL)](#Kusto-Query-Language)) 
  - [Power BI](#Power-BI)   
     - [PBI demo script](#PBI-demo-script)  
     - [Connect to Help cluster](#Connect-to-Help-cluster)  
     - [Create Power BI report](#Create-Power-BI-report)
      
   - [KQL – Results](#KQL–Results)
   
  <!-- TOC -->   
## Infrastructure  
    
1. Open Lab: http://bit.ly/2WCFDdz  
     - **Register Now**: Complete registration information on page  
     - **Select LAUNCH LAB**: Opens the **Environment Details** page  
     - Open the Lab guide: "**LAB GUIDE URL**"
      
2. Open Azure portal in private mode: https://portal.azure.com  

      - Connect with the Azure **Credentials**:  
   
   **<image 01>** 
   
      - The portal opens with your credentials:  
      
      **<image 02>**
    
 3.	Search and select Azure Data Explorer Clusters.
   
      **<image 03>**
   
 4.	In the **Azure Data Explorer Clusters** window, select the **KustoSUFFIX** cluster.
     
     **<image 04>** 
    
 5. Select **Data** from the left-hand menu, under **Databases** , and then select **+Add Database** . 
   
     **<image 05>**  
    
 6.	In the **Azure Data Explorer Database** window:  
    
     **<image 06>** 
    
      - **Database name**: **<alias>_adxdb** 
      - **Retention period** (cold compressed data (Azure Blob Storage) : **365**
      - **Cache period**(hot compressed data (SSD)): **31**
 
 7.	In **Databases**, select your new **alias_adxdb database**
 8. Select **Query**
 
    **<image 07>**
 9. In the Web UI, create a table 
  ```
  // Create a table
  .create table SampleTable
  (Timestamp:datetime, ApiVersion:string, User:string, RawHeader:dynamic)
```  

## Ingestion

  **<image 08>**
  
1. Create table mapping  
 ```
   // Create a Json ingestion mapping
.create table SampleTable ingestion json mapping 
"Mapping01" '[{"column":"Timestamp","path":"$.header.time"},{"column":"ApiVersion","path":"$.header.api_version"},{"column":"RawHeader","path":"$.header"},{"column":"User","path":"$.payload.user"}]'
```

2.	View ingestion mapping 
 ```
    // View ingestion mappings
.show table SampleTable ingestion json mappings  
  ```
3.	Ingestion from public blob 
 ``` 
    // Ingest from public blob
    .ingest into table SampleTable
   @'https://westuskustopublic.blob.core.windows.net/public/SampleData-500-4394582f-668f-4d03-8bba-58f87a7e48a0.json'
   with (jsonMappingReference = "Mapping01")
   ```

## Exploration 
### Questions 
 
 If you skipped the previous step(s), please click on database: **text** . 

1.	How many lines were ingested? 
2.	Add calculated column of Transaction Id from column RawHeader: attribute Id
3.	Take a 10 row sample of RawHeader 
4.	How many records were ingested from version 1 and 2?
5.	Create a time chart with 10 minute bins of RawHeader['time']
6.	Drop table SampleTable
7.	Run.show queries  

## Kusto Query Language (KQL) 
- … | **count**	
  Counts records in input table (e.g. T)  
  
 -	… | **take** 10	
 	Get few records to become familiar with the data. No order ensured.  

-	… | **where** Timestamp > ago(1) and UserId = ‘abdcdef’	
 	Filters on specific fields  
  
-	… | **project** Col1, Col2, …	
 	Select some columns (use if input table has many columns)  
  
-	…| **extend** NewCol1=Col1+Col2		
	Introduces new calculated columns  
 
-	… | **render** timechart		
	Plots the data (in KE and KWE) while exploring  
 
-	… | **summarize** count(), dcount(Id) by Col1, Col2		
	Analytics: aggregations  
 
-	… | **top** 10 by count_ desc 
	Finds the needle in the haystack  
 
-	… | **join** (…) on Key1, Key2 
	Joins data sets 
 
- … | **mvexpand** Col1,Col2 … 
	Turns dynamic arrays to rows (multi-value expansion)  
 
- … | **parse** Col1 with <pattern>…
	Deals with unstructured data  
 
## Results  
1. SampleTable | count 

2. SampleTable | extend TransactionId = RawHeader.id

3.	SampleTable
| extend TransactionId = RawHeader.id
| take 10 

4. Option 1  
  - SampleTable
| extend recordversion =  tostring(RawHeader.api_version)
| summarize count() by recordversion


 



 
  
 

 
