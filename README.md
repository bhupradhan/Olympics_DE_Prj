# Olympics_DE_Prj
## **Problem Statement**
Create a data pipeline by leveraging Azure Synapse Analytics, Azure Storage, and an Azure Synapse SQL pool to execute data analysis on the 2021 Olympics dataset.
- The dataset contains information on more than 11,000 athletes representing 743 Teams and competing in 47 sports at the Tokyo Olympics in 2021. This dataset contains data on the teams, athletes, coaches, and entries that participated, subdivided by gender.
- The first step in this project is to create an azure storage account and import data files into a container.
- Next, build an azure synapse analytics workspace and an SQL pool.
- Create a data pipeline to feed data into Power BI from SQL pool tables once you load it into Azure storage.
- The final step is creating the dashboard in Power BI and publishing it to an Azure Synapse workspace.
- Find insights among the data

## **Requirements** : Olympics 2021 dataset
- Azure subscription
- Azure Synapse Analytics
- Power BI Desktop
- Azure blob storage

![image.png](Olympics_DE_Prj/image-32ff418f-a136-428d-8e8a-c9b4ea44e7da.png)

### System Requirements
- Windows 8.1 / Windows Server 2012 R2, or later
- .NET 4.6.2 or later
- Internet Explorer 11 or later
- Memory (RAM): At least 2 GB available, 4 GB or more recommended.
- Display: At least 1440x900 or 1600x900 (16:9) required. Lower resolutions such as 1024x768 or 1280x800 aren't supported, as certain controls (such as closing the startup screen) display beyond those resolutions.
- Windows display settings: If you set your display settings to change the size of text, apps, and other items to more than 100%, you may not be able to see certain dialogs that you must interact with to continue using Power BI Desktop. If you encounter this issue, check your display settings in Windows by going to Settings > System > Display, and use the slider to return display settings to 100%.
- CPU: 1 gigahertz (GHz) 64-bit (x64) processor or better recommended.
- WebView2, if not automatically installed with Power BI Desktop or uninstalled.

# 2021 Olympics in Tokyo
Data about Athletes, Teams, Coaches, Events

### Details
This contains the details of over 11,000 athletes, with 47 disciplines, along with 743 Teams taking part in the 2021(2020) Tokyo Olympics.
This dataset contains the details of the Athletes, Coaches, Teams participating as well as the Entries by gender. It contains their names, countries represented, discipline, gender of competitors, name of the coaches.

Will update the dataset with medals(gold, silver, bronze), more details about the athletes after few weeks.

### Credits
Source: Tokyo Olympics 2020 Website

### About Dataset

## Athletes 

|Table|	Total Rows|	Total Columns|
|--|--|--|
|Details|	11085|	3|

## Coaches
|Table|	Total Rows|	Total Columns|
|--|--|--|
|Details|	394|	4|

##EntriesGender
|Table	|Total Rows|	Total Columns|
|--|--|--|
|Details|	46|	4|

##Medals
|Table|	Total Rows|	Total Columns|
|--|--|--|
|Details|	93|	7|

##Teams
|Table|	Total Rows|	Total Columns|
|--|--|--|
|Details|	743|	4|



# Import Dataset into azure blob storage

## Create a storage account
A storage account is an Azure Resource Manager resource. Resource Manager is the deployment and management service for Azure. For more information, see Azure Resource Manager overview.

Every Resource Manager resource, including an Azure storage account, must belong to an Azure resource group. A resource group is a logical container for grouping your Azure services. When you create a storage account, you have the option to either create a new resource group, or use an existing resource group. This how-to shows how to create a new resource group.

Basics tab
On the Basics tab, provide the essential information for your storage account. After you complete the Basics tab, you can choose to further customize your new storage account by setting options on the other tabs, or you can select Review + create to accept the default options and proceed to validate and create the account.

Create new container 

Upload datasets

- Athletes.csv
- Coaches.csv
- Teams.csv
- EntriesGender.csv
- Medals.csv


![Screenshot (532).png](Olympics_DE_Prj/Screenshot%20(532)-c6373faf-1aae-4315-953b-cce11d6eb5be.png)



# Architecture 

![image.png](Olympics_DE_Prj/image-71d20157-04aa-44c4-9447-c6505fb9858f.png)


# Azure Synapse Analytics:
Synapse Analytics is an integrated platform service from Microsoft Azure that combines the capabilities of data warehousing, data integrations, ETL pipelines, analytics tools & services, the scale for big-data capabilities, visualization & dashboards.

Open the Azure portal, in the search bar enter Synapse without hitting enter.
In the search results, under Services, select Azure Synapse Analytics.

## Here are the following steps performed 

Create and setup a Synapse workspace

- Your Azure Synapse workspace will use this storage account as the "primary" storage account and the container to store workspace data
- Workspace name - Pick any globally unique name. we'll use myworkspace.
- Region - Pick the region where you have placed your client applications/services
- By Account name, select Create New and name the new storage account contosolake or similar as the name must be unique.

<IMG  src="https://lh5.googleusercontent.com/3eAyfTS4-EyI0y1kXx_9yPGwzQv_8FoNLUXsrQhhDghL4uVwMBkWs-R5xzDKTAMcdO9HFOU32EbazdDI31i57o7y37jYsBPkfn7NDpbom-MZY6bBx92tBwsMNs5sAsDol_Resxhe7ioHOFE8q1quaz921AZ_OGXg7KtnEyamUEC1Ek5fo2K466YtjQ"  width="444"  height="276" style="margin-left:0px;margin-top:0px"/></SPAN></SPAN>

- By File system name, select Create New and name it users. This will create a storage container called users. The workspace will use this storage account as the "primary" storage account to Spark tables and Spark application logs.
- Check the "Assign myself the Storage Blob Data Contributor role on the Data Lake Storage Gen2 account" box.
- Open your Synapse workspace in the Azure portal, in the Overview section of the Synapse workspace, select Open in the Open Synapse Studio box.
- Go to the https://web.azuresynapse.net and sign in to your workspace.

# To create pipeline to copy data from azure blob storage to SQLPOOL1

## Creating pipeline in a cloud based solution like Synapse makes it easier to perform ETL / ELT Jobs.
- In Synapse Studio, go to the Integrate hub.
- Select + > Pipeline to create a new pipeline. Click on the new pipeline object to open the Pipeline designer.
- Under Move and Transform drag copy activity in pipeline
- select 5 copy activities and join them 
- in source:
- select file from azure blob storage(delimited text)
- in sink:
- select dedicated sql pool


![Screenshot (534).png](Olympics_DE_Prj/Screenshot%20(534)-b1fce0ec-a0f8-4d5b-a932-03e69a3e0128.png)

# Analyze using a dedicated SQL pool

- Select Create a resource in the upper left-hand corner of the Azure portal
- In the search bar type "dedicated SQL pool" select dedicated SQL pool (formerly SQL DW). Select Create on the page that opens.
- Under Performance level, select Select performance level to optionally change your configuration with a slider.
- Select Additional Settings, under Use existing data, choose Sample so that AdventureWorksDW will be created as the sample database.
- Now that you've completed the Basics tab of the Azure Synapse Analytics form, select Review + Create and then Create to create the SQL pool. Provisioning takes a few minutes.

![Screenshot (531).png](Olympics_DE_Prj/Screenshot%20(531)-56c82cc9-fd41-4853-9dac-49da95c1c21e.png)

![Screenshot (533).png](Olympics_DE_Prj/Screenshot%20(533)-39489863-382c-4fd7-8788-672a9587e75b.png)

# Visualize data with Power BI

Power BI is a collection of software services, apps, and connectors that work together to turn your unrelated sources of data into coherent, visually immersive, and interactive insights. The data may be an Excel spreadsheet, or a collection of cloud-based and on-premises hybrid data warehouses
Linking a Power BI workspace to a Synapse workspace
 
- Starting from Synapse Studio, click Manage.
- Under External Connections, click Linked services.
- Click + New.
- Click Power BI and click Continue.
- Enter a name for the linked service and select a workspace from the dropdown list.
- Click Create.

![Screenshot (535).png](Olympics_DE_Prj/Screenshot%20(535)-3d3a2235-1082-4471-ab4a-c5edd7c553e2.png)


# PowerBI visualisation

Visualizations are used to effectively present your data and are the basic building blocks of any Business Intelligence tool. Power BI contains various default data visualization components that include simple bar charts to pie charts to maps, and also complex models such as waterfalls, funnels, gauges, and many other components.

## You can create visualization in two ways. 

- First is by adding from the right side pane to Report Canvas. By default, it is the table type visualization, which is selected in Power BI.
-  Another way is to drag the fields from right side bar to the axis and value axis under Visualization.
-  You can add multiple fields to each axis as per the requirement.
- In the value fields, you can see that it accepts values axis such as gender and country and or you can also add longitude and latitude values. To change the bubble size, you need to add a field to the value axis
- You can also use a filled map in data visualization, just by dragging the filled map to the Report Canvas.
-  In data visualization, it is also required to plot multiple measures in a single chart. Power BI supports various combination chart types to plot measure values
- Combination chart in Power BI is Line and Stacked column charts
- Once you add a data source, it will be added to the list of fields on the right side. We can add units to the column axis
- when you add a dataset to your visualization, it adds a table chart to the Report canvas. You can drag the fields that you want to add to the report. You can also select the checkbox in front of each field to add those to the Report area.
- With the numerical values in a table, you can see a sum of values at the bottom.
-  Create dashboard for all the visualizations





# View Power BI workspace in Synapse Studio

Once workspaces are linked, the browse your Power BI datasets, edit/create new Power BI Reports from Synapse Studio.

- Click Develop.
-   Expand Power BI and the workspace you wish to use
-  New reports can be created clicking + at the top of the Develop tab.
-  Existing reports can be edited by clicking on the report name. Any saved changes will be written back to the Power BI workspace 

![Screenshot (539).png](Olympics_DE_Prj/Screenshot%20(539)-ffa06f17-ac3d-490e-ad43-3e735ad0dc67.png)

## Insights

- Sum of medals by country

![Screenshot (538).png](Olympics_DE_Prj/Screenshot%20(538)-56bbf388-374b-4a78-ab9c-986de3859082.png)

## Insights

- Count of discipline by country

### Example:

Afghanistan is performing in 4 kind of discipline 

- Athletics 2
- Shooting 1
- Taekwondo 1 
- Swimming 1 

![Screenshot (537).png](Olympics_DE_Prj/Screenshot%20(537)-81b4409e-907f-4310-b7ba-6a8527d4d1d7.png)

## Insights

Pie chart

Total Medals won by the team
- USA is highest
- NorthMatridonia is Least

Stat column chart

Number of females and males performed

###Donut Chart
- Sum of male and females

# Report
Sum of medals by country, Count of discipline by country is obtained, Afghanistan is performing in 4 kind of discipline, Athletics 2, Shooting 1, Taekwondo 1,  Swimming 1. In Pie chart Total Medals won by the team USA is highest and NorthMatridonia is Least. In Stat column chart, Number of females and males performed is displayed and using Donut Chart Sum of male and females is obtained.




# Azure Synapse Analytics

### Error code: 3250
Message: There are not enough resources available in the workspace, details: '%errorMessage;'

Cause: Insufficient resources

Recommendation: Try ending the running job(s) in the workspace, reducing the numbers of vCores requested, increasing the workspace quota or using another workspace.

### Error code: 3251
Message: There are not enough resources available in the pool, details: '%errorMessage;'

Cause: Insufficient resources

Recommendation: Try ending the running job(s) in the pool, reducing the numbers of vCores requested, increasing the pool maximum size or using another pool.

### Error code: 3252
Message: There are not enough vcores available for your spark job, details: '%errorMessage;'

Cause: Insufficient vcores

Recommendation: Try reducing the numbers of vCores requested or increasing your vCore quota. For more information, see Apache Spark core concepts.

### Error code: 3253
Message: There are substantial concurrent MappingDataflow executions which is causing failures due to throttling under the Integration Runtime used for ActivityId: '%activityId;'.

Cause: Throttling threshold was reached.

Recommendation: Retry the request after a wait period.

### Error code: 3254
Message: AzureSynapseArtifacts linked service has invalid value for property '%propertyName;'.

Cause: Bad format or missing definition of property '%propertyName;'.

Recommendation: Check if the linked service has property '%propertyName;' defined with correct data.

## Common
### Error code: 2103
Message: Please provide value for the required property '%propertyName;'.

Cause: The required value for the property has not been provided.

Recommendation: Provide the value from the message and try again.

### Error code: 2104
Message: The type of the property '%propertyName;' is incorrect.

Cause: The provided property type isn't correct.

Recommendation: Fix the type of the property and try again.

### Error code: 2105
Message: An invalid json is provided for property '%propertyName;'. Encountered an error while trying to parse: '%message;'.

Cause: The value for the property is invalid or isn't in the expected format.

Recommendation: Refer to the documentation for the property and verify that the value provided includes the correct format and type.

### Error code: 2106
Message: The storage connection string is invalid. %errorMessage;

Cause: The connection string for the storage is invalid or has incorrect format.

Recommendation: Go to the Azure portal and find your storage, then copy-and-paste the connection string into your linked service and try again.

### Error code: 2110
Message: The linked service type '%linkedServiceType;' is not supported for '%executorType;' activities.

Cause: The linked service specified in the activity is incorrect.

Recommendation: Verify that the linked service type is one of the supported types for the activity. For example, the linked service type for HDI activities can be HDInsight or HDInsightOnDemand.

### Error code: 2111
Message: The type of the property '%propertyName;' is incorrect. The expected type is %expectedType;.

Cause: The type of the provided property isn't correct.

Recommendation: Fix the property type and try again.

### Error code: 2112
Message: The cloud type is unsupported or could not be determined for storage from the EndpointSuffix '%endpointSuffix;'.

Cause: The cloud type is unsupported or couldn't be determined for storage from the EndpointSuffix.

Recommendation: Use storage in another cloud and try again.
