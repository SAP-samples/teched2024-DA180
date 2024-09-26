# Exercise 2 - Data Layer - Prepare Your Data

> :memo: **Note:** This is an Optional Exercise

## :beginner: Detour: SAP Datasphere - Model Types
Before we are going to start with the first exercise in creating a table and creating the first model, let us have a look at the
different asset types that you can create in the Data Builder of SAP Datasphere.

So, let’s now look at the different asset types:
- **Table**: Create a Table to contain data by defining its column structure. You can configure each field of the Table, and already define semantics and associations. You have the ability to upload data to this Table later on.</p>
- **Graphical View**: In the Graphical View you can leverage Tables and Views to prepare data and then create new Views using a graphical no-code/low-code editor. Join datasets as required, add other operators to remove or create columns and filter or aggregate data, and specify measures and other aspects of your output structure in the output node. </p>
- **SQL View**: In the SQL View you can leverage Tables and Views to the create new Views by using SQL or SQL-script (table function) view in a powerful SQL editor.
<br>*Not used in the DA180 exercises.* </p>
- **Entity-Relationship Model**: Here you define the relationships between Tables or Views, which then are being leveraged when you create a new View based on the Tables or Views.</p>
- **Analytic Model**: Analytic models are the analytical foundation for making data ready for consumption in SAP Analytics Cloud. They allow you to create and define multi-dimensional models to provide data for analytical purposes to answer different business questions. </p>
- **Data Flow**: You define Data Flows to use data transformations and leverage the option to load data from a source system and persist it in SAP Datasphere. <br>*Not used in the DA180 exercises.*</p>
- **Replication Flow**: Create a replication flow if you want to copy multiple data assets from the same source to the same target in a fast and easy way and do not require complex projections. <br>*Not used in the DA180 exercises.*</p>
- **Transformation  Flow**: Create a transformation flow if you want to load data from one or more source tables, apply transformations (such as a join), and output the result in a target table. You can load full or delta data sets of data from one or more source tables to a target table.
- **Intelligent Lookup**: Create an intelligent lookup to merge data from two entities even if they do not have a common identifier. <br>*Not used in the DA180 exercises.*</p>
- **Task Chain**: Create a task chain that groups multiple tasks, which can be run in series manually or through a schedule. <br>*Not used in the DA180 exercises.*</p>

## End of Detour

## Start of the exercise

In this section we will start creating the tables for our sample models and then upload the raw data to those tables in [Exercise 5](../ex05/README.md). 

We will start to create the tables in SAP Datasphere.

1. Log On to your SAP Datasphere tenant.</p>
2. Select the menu option Data Builder on the left-hand side. In case you are being asked, select your space (e.g. GE12345)</p>
3. Create a new folder to organize the entities you will create in this jump-start session by navigating to the "+"-icon on the right and enter "TECHED2024-DA180" as business name and confirm. A new folder is displayed in the object list.
<br>![](images/00_00_0001.png)

4. Select the option ***New Table***.
<br>![](images/00_00_0031.png)

5. You are being presented with the details to create a new table.

6. Enter the following details:<br><ul><li>Business Name - Sales Transactions</li><li>Technical Name - Sales_Transactions</li><li>Semantic Type - Relational Dataset
<br>![](images/00_00_0032.png)  
  
7. Scroll down to the area ***Columns*** (you can also use the tabs in the page header for navigation). Here you
define the structure of the table by adding the individual columns.

8. Use the “+” sign in the top right corner of the ***Columns*** area to start the process of creating your first table
column
<br>![](images/00_00_0033.png)

9. You now need to enter a business name, a technical name, and you need to configure the Data Type
10. For the first column, enter the following details:<br><ul><li>Business Name -   Transaction ID</li><li>Technical Name -   Transaction_ID</li><li>Data Type -  Integer64<br>
  
---  

> :bulb: **Tip:** Please note, that you can change the <strong>Data Type</strong> simply by clicking on the default data type (e.g. String(100) in the Data Type column.

---  
  
11. After you entered the details for the first column, please enter the additional columns. All columns of the table are listed as follows:
  
| Key: | Business Name:      | Technical Name:                       | Data Type:          |
|:-----|:--------------------|:--------------------------------------|:--------------------|
| X    | Transaction ID      | Transaction_ID                        | Integer64           |
|      | Transaction Date    | Transaction_Date                      | Date                | 
|      | Store ID            | Store_ID                              | String (6)          | 
|      | Product ID          | Product_ID                            | String (4)          | 
|      | Sales Manager ID    | Sales_Manager_ID                      | String (4)          | 
|      | Profit              | Profit                                | Decimal(15,2)       | 
|      | Discount            | Discount                              | Decimal(15,2)       | 
|      | Revenue             | Revenue                               | Decimal(15,2)       | 
|      | Cost                | Cost                                  | Decimal(15,2)       |   
  
12. After you entered all columns for the table, ensure you enable the Key Column option for the column
Transaction ID.
  
13. Now use the ***Save*** option in the General menu.
<br>![](images/00_00_0035.png) 
  
14. Select the folder "TECHED2024-DA180". On the first time you save the table, you will be asked to confirm the name and technical name.
<br>![](images/00_00_0002.png) 

15. Click ***Save***.
16. After you saved the changes, you also have to deploy the table, so that we can later on upload data to the table.
17. Use the Deploy option from the General menu.  
<br>![](images/00_00_0036.png)   
  
18. We configured, saved, and deployed our first table.
19. Click on the ***"back arrow"*** on the top menu bar to navigate back to the list of tables. 
<br>![](images/00_00_0037.png)  

20. You are back at the home screen of the Data Builder and you should see your table in the list of objects.
21. Use the option ***New Table***.
22. Enter the following details:<br><ul><li>Business Name - Store</li><li>Technical Name - Store</li><li>Semantic Type - Dimension<br>
<br>![](images/00_00_0034.png)
<br>
  
23. Navigate to the ***Attributes*** area.
 
24. Use the “+ sign to create new attributes.
<br>![](images/00_00_0038.png) 
  
---  
 
> :bulb:  **Tip:** You will notice, based on the Type Dimension, we now have two additional options for each Column:
Semantic Type and Text/Association.<br>  
The column Text/Association allows you to specify the purpose of an attribute when your entity is consumed later. For example, you
could have a Product ID and a Product Description in the table and use the Product Description column as
text for the Product ID.<br>  
The Semantic Type option provides you with several option to choose from, so that you can configure an
additional context for the column, such as the option to configure the column as a Currency column or a
language column.

---
  
25. Enter the following ***Attributes*** for the table:  
  
| Key: | Business Name:      | Technical Name:                       | Data Type:          | Semantic Type       | Text/Association   |
|:-----|:--------------------|:--------------------------------------|:--------------------|:--------------------|:---------------|
| X    | Store ID            | Store_ID                              | String (6)          | None                | Store Name     |
|      | Store Name          | Store_Name                            | String (30)         | Text                |
|      | Store City          | Store_City                            | String (20)         | 
|      | State ID            | State_ID                              | String (2)          | 
|      | State Name          | State_Name                            | String(30)          | 
|      | Country             | Country                               | String(30)          | 
|      | Latitude            | Latitude                              | Decimal(15,8)       | 
|      | Longitude           | Longitude                             | Decimal(15,8)       | 
    
---
  
> :bulb: **Tip:** Please note, that you can only select the Store Name for the column <strong>Text/Association</strong> after you entered the details for the Store Name into ***Attributes***.

---

26. After you entered all columns for the table, ensure you enable the Key Column option for the column Store ID.
27. Click ***Save*** in the General menu.
28. You will be asked to confirm the business name as well as the technical name.
29. Click ***Save***.
30. Click ***Deploy*** in the General Menu.
31. Navigate back to the list of tables. 
32. Create a new table.
33. Enter the following details:<br><ul><li>Business Name - Product</li><li>Technical Name - Product</li><li>Semantic Type - Dimension<br>
<br>  

34. Navigate to the ***Attributes*** area.<br>
35. Enter the following attributes for the table:
 
| Key: | Business Name:        | Technical Name:                       | Data Type:          | Semantic Type       | Text/Association          |
|:-----|:----------------------|:--------------------------------------|:--------------------|:--------------------|:----------------------|
| X    | Product ID            | Product_ID                            | String (4)          | None                | Product Name          |
|      | Product Name          | Product_Name                          | String (30)         | Text                |                       |
|      | Product Category ID   | Product_Category_ID                   | String (4)          | None                | Product Category Name |
|      | Product Category Name | Product_Category_Name                 | String (30)         | Text                |                       |  
  
36. After you entered all columns for the table, ensure you enable the Key Column option for the column Product ID.
37. Click ***Save*** in the General menu.
38. You will be asked to confirm the business name as well as the technical name.
39. Click ***Save***.
40. Click ***Deploy*** in the General Menu.
41. Click on ***"back arrow"*** on the top menu bar to navigate back to the list of tables. 
<br>![](images/00_00_0037.png)

42. Use the option ***New Table***.
43. Enter the following details:<br><ul><li>Business Name - Sales Manager</li><li>Technical Name - Sales_Manager</li><li>Semantic Type - Dimension<br>
<br>  

44. Navigate to the ***Attributes*** area.<br>
45. Enter the following attributes for the table:

| Key: | Business Name:        | Technical Name:                       | Data Type:          | Semantic Type       | Text/Association          |
|:-----|:----------------------|:--------------------------------------|:--------------------|:--------------------|:----------------------|
| X    | Sales Manager ID      | Sales_Manager_ID                      | String (4)          | None                | Sales Manager Name    |
|      | Sales Manager Name    | Sales_Manager_Name                    | String (30)         | Text                |                       |

46. After you entered all columns for the table, ensure you enable the Key Column option for the column Sales
Manager ID.
47. Click ***Save*** in the General menu.
48. You will be asked to confirm the business name as well as the Technical Name.
49. Click ***Save***.
50. Click ***Deploy*** in the General Menu.
51. Use the Back option in top menu or as an alternative you can click on your Space name to navigate back to the home screen of the Data Builder.
  
## Summary

You have now created all tables that we need for our model and the overview in the Data Builder when you filter on tables should look
like this:
<br>![](images/00_00_0039.png)

Continue to [Exercise 03 - Creating the Entity Relationship Model ](../ex03/README.md)
