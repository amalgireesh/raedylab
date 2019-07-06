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
  
1.	Create table mapping  
  ```
   // Create a Json ingestion mapping
.create table SampleTable ingestion json mapping 
"Mapping01" '[{"column":"Timestamp","path":"$.header.time"},
{"column":"ApiVersion","path":"$.header.api_version"},
{"column":"RawHeader","path":"$.header"},{"column":"User","path":"$.payload.user"}]'
```
 
  
 

 
