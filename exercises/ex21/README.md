# Exercise 21 - Create Row-Level Permissions based on an External Hierarchy

>:memo: **Note:** This is an OPTIONAL exercise.

---

## :beginner: Detour: SAP Datasphere - Hierarchies and Data Access Controls

You can specify the following types of hierarchies:

**Parent-Child** - the hierarchy is recursive, may have any number of levels, and is defined by specifying a parent column and a child column within the dimension. For example, a departmental hierarchy could be modeled with the Parent Department ID and Department ID columns.

**Level-Based** - the hierarchy is non-recursive, has a fixed number of levels, and is defined by specifying two or more level columns within the dimension. For example, a time hierarchy could be modeled with the: Year, Quarter, Month, Week, and Day columns.

**External Hierarchy** - the parent-child hierarchy information is contained in a separate entity, which needs to be associated with the dimension (see Create an External Hierarchy for Drill-Down).

**Data access controls** allow you to apply row-level security to your objects. There are different options how to specify criteria which user is allowed to see which user. One option is the definition based on a hierarchy. Each user can only see the records that match the hierarchy values she is authorized for in the permissions entity, along with any of their descendents. Only external hierarchies with a single pair of parent-child columns are supported. 

## End of Detour

## Create a Parent-Child Hierarchy

1. Log On to your SAP Datasphere tenant.
2. Select the menu option Data Builder on the left-hand side
3. Select the option ***New Table***.

4. Enter the following details:<br><ul><li>Business Name - Hierarchy_ProductCategory</li><li>Technical Name - Hierarchy_ProductCategory</li><li>Semantic Usage - Hierarchy<br>
<br>  

5. Warnings are displayed as no parent and child columns are defined yet which represent the hierarchy. The child column must be a key column and the parent and child columns must have the same data type.

6. Enter the following attributes for the table:
 
| Key: | Business Name:        | Technical Name:                       | Data Type:          |
|:-----|:----------------------|:--------------------------------------|:--------------------|
| X    | Child Category         | Child_Category                       | String (30)         | 
|      | Parent Category       | Parent_Category                       | String (30)          | 



7. Ensure that ***Child Category*** is set as key.
<br>![](images/00_00_002.png)   
  
8. Now select the column ***Parent Category*** as parent and the column ***Child Category*** as child. Notice that the validation icon in the upper right corner turns green. 
<br>![](images/00_00_0003.png) 

9. Save and deploy your hierarchy table in the folder TECHED2024-DA180. 

10. Download the :file_folder: [CSV file data_hierarchy_productcategories.csv](data/data_hierarchy_productcategories.csv) and upload the data to the table. 
<br><br>![](images/00_00_0004.png) 

11. Confirm the data entries in the data preview.
<br>![](images/00_00_0005.png) 

## Create a Permission Entity
A permission entity (view or table) lists SAP Datasphere user IDs (in the form required by your identity provider) and assigns them to one or more criteria. In this example, you will define criteria for your own user so that you only see products belonging to the category/sub-categories of non-alcoholic beverages.

1. Select the option ***New Table*** in the Data Builder.

2. Enter the following details:<br><ul><li>Business Name - Permission Entity Product Category </li><li>Technical Name - PE_ProductCategory</li><li>Semantic Usage - Relational Dataset<br>
<br>  

3. Enter the following columns:
 
| Key: | Business Name:        | Technical Name:                       | Data Type:          | Text/Association          |
|:-----|:----------------------|:--------------------------------------|:--------------------|:----------------------|
| X    | Record ID         | Record_ID                     | Integer         |                | 
|      | User ID         | User_ID                       | String (50)         |                |      
|      | Product Category      | Parent_Category                       | String (30)          |                 |      


4. Verify your configuration.
<br>![](images/00_00_0007.png) 

5. Save and deploy the table in the folder TECHED2024-DA180.

6. After the table is deployed, open the data editor to add records.
<br>![](images/00_00_0007.5.png) 

7. Add the following record to the table. Replace the first part of the email address below for user id with the name of your user (same name as the space). You could also copy your email address if you go to ***Profile*** in the upper right corner and select ***Settings***.

<br>![](images/00_00_0008.png) 

| Record ID                 	| User ID        	| Product Category        | 
|-----------------------	|---------------	| ---------------	|
|          1      	| geXXXXXX@sapexperienceacademy.com     	|  Non-Alcoholic     	| 

8. Save the added record.



## Create a Data Access Control Entity

We want to protect the data of our sales transactions based on this parent-child hierarchy. Reporting users should only see sales of the product categories they have permissions to. We define the permissions based on the nodes "Alcohol", "Non-Alcoholic" and "Others".

1. In the side navigation area, select ***Data Builder*** and click ***New Data Access Control*** to open the editor.
<br>![](images/00_00_0006.png) 

2. Enter the following details in the ***General*** section and select the permission entity which you created in the previous step:<br><ul><li>Business Name - DAC Product Category</li><li>Technical Name - DAC_ProductCategory</li><li>Structure - Hierarchy</li><li>Permissions Entity - PE_ProductCategory<li>Identifier Column - User ID<br>
<br>

3. Enter the following details in the ***Criteria*** section and select the hierarchy table which you created in the first step of this exercise:<br><ul><li>Business Name - Product Category</li><li>Technical Name - Product_Category</li><li>Hierarchy Entity - Hierarchy_ProductCategory</li><li>Criterion Column - Product Category<br>
<br>

4. Verify that your settings look like in the screenshot below:
<br>![](images/00_00_0009.png)

5. Save and deploy your new Data Access Control entity in the folder TECHED2024-DA180.

## Apply the Data Access Control Entity to a View
1. Open your previously created view ***Sales View – Fact***(***Sales_View__Fact***).

2. The attributes which are authorization-relevant need to be part of the fact view. Drag the table ***Product*** into the editor (join).

3. Set the Join Type to ***Left*** and the cardinality to Many (***Sales Transactions***) to Exactly One (***Product***). Map the columns ***Product ID***.
<br>![](images/00_00_0012.png)

4. Open the Projection Node. The column ***Product ID*** of the table ***Sales Transactions*** is hidden while the column derived from the table ***Product*** (dimension) is visible. We do not want to keep ***Product ID*** as a key, therefore exclude the column ***Product ID*** (Key from ***Products***) and restore ***Product ID*** (***Sales Transactions***).
<br>![](images/00_00_0016.png)

>:bulb: If you select the column in any diagram node you can trace the lineage back to the source.

5. Go to the association which points to the dimension ***Product*** and maintain the mapping (Product ID to Product ID) as this has been removed because of the join.

6. In the model properties, add a new Data Access Control.
<br>![](images/00_00_0010.png)

7. Select the previously created DAC ***DAC_ProductCategory***.
<br>![](images/00_00_0011.png)

8. Map the two columns named ***Product Category Name*** (enter the name in the **Search** Field).
<br>![](images/00_00_0013.png)

9. Set the Alias of the table ***Product*** to ***ProductDim_DAC***.
<br>![](images/00_00_0017.png)

10. Save and deploy the view ***Sales_View -  Fact***. If you see the validation message warning that an association has been changed, click ***Deploy Anyway***.
<br>![](images/00_00_0017.png)

11. Open the data preview and validate that you can only see sales for non-alcoholic data products. 
<br>![](images/00_00_0018.png)

12. Add a filter for ***Product Category Name***.
<br>![](images/00_00_0019.png)

13. Filter on records which contain values equal to ***Alcohol***. This search should not display any value.
<br>![](images/00_00_0020.png)

> :boom: **Important:** :boom: <br>
Please consider that you will now only see a limited amount of records due to the assigned data access control. You can modify the data record of the permission table ***PE_ProductCategory*** and replace the value in the column ***Product Category*** (Non-Alcoholic) with Beverages so that you see all records again when going through other exercises.

14. You can open the previously created reports in SAP Analytics Cloud. You will only see the records your user is authorized to access.


## Summary

You've now protected the transactional records of the fact view with a Data Access Control based on product categories. If you would like to recreate authorizations from the source system, you can import analysis authorizations from SAP BW and SAP BW/4HANA.

You can continue with one of the optional exercises:
- [Exercise 20: Identify Top-Performing Sales Managers with Just Ask](../ex20/README.md)
- [Exercise 22: Explore the Analytic Model](../ex22/README.md)
- [Exercise 23: Create a Transformation Flow](../ex23/README.md)
