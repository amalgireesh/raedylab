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
   
   ![Screenshot of the Azure Login Credentials.]  
   
      - 	The portal opens with your credentials:  
      
      <image 02>
    
   4.	Open Lab Guide  
   
      xxx
   
   5.	Go to Azure Data Explorer Clusters  
   
    ![Screenshot of Azure Data Explorer Cluster]  
    
   6.	Click on Cluster KustoSUFFIX
   
    ![Screenshot of Azure Data Explorer Cluster2]  
    
   7. Click **data**. Then, choose Databases followed by **+Add Database**.  
    
    ![Screenshot of Azure Data Explorer and add database]  
    
   8. Specify the following properties and confirm creation to continue:
   
      - **Database name** Alias_adxdb 
      - **Retention period-(in days)** : 365
      - **Cache period-(in days)** : 31


   
   
   
    
   
   
     
      
  
  
   

   
   
