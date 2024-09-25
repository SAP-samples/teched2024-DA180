# Exercise 23 - Create a Transformation Flow

>:memo: **Note:** This is an OPTIONAL exercise.

---

## :beginner: Detour: SAP Datasphere - Transformation Flows

Transformation Flows load data from one or more sources and persist the result in a target table. This integration entity can detect delta changes when reading data from a local table which is enabled for delta.
Transformation Flows are also useful in scenarios when utilizing Replication Flows for Outbound Integration: Replication Flows can access local tables (delta enabled) which are updated by a transformation flow and transfer the data records in a delta mode.

## End of Detour

## Start of the exercise
In this exercise, we will access a shared local table which is delta enabled for sales transactions. New sales transactions are generated in a source system and transferred to SAP Datasphere using a Replication Flow. This happens in a separate admin space of the free trial. 
Assume that the STORE_ID includes the prefix ***US*** which we remove so that we can map the store id to the dimensions available in the view dimensions.
We will create a new Analytic Model which accesses the regularly updated data and use the replace model feature in SAC to have a second story accessing the new Analytic Model.


1. Log On to your SAP Datasphere tenant.
2. Select the menu option ***Data Builder*** on the left-hand side.
3. Click ***New Transformation Flow***.
<br>![](images/00_00_0001.png)  

4. You see the Transformation Flow editor with options to define view transformation and create a new table.
<br>![](images/00_00_0002.png)  

5. Click on the ***View Transform*** node and select the ***Graphical View Transform*** option.
<br>![](images/00_00_0003.png)  

6. Drag and drop the table ***TECHED2024_SALES_TRANSACTIONS*** into the editor. The details on the right-hand side display that this shared table is capturing delta. (If you don't see this table, ensure that you are in the ***Graphical View Editor***.)
<br>![](images/00_00_0004_1.png)  

7. If you scroll down, ensure that ***Load from Table*** is set to ***Delta Capture***. As the delta capture setting is enabled for the source table, the columns ***Change Date*** and ***Change Type*** are automatically mapped to these columns in the target table. Mapping these columns (or a calculated column that contains the content of these columns) to any other target column is not permitted. 
<br>![](images/00_00_0005.png)  

8. Add a new node for ***Calculated Columns***. Choose the existing column ***STORE_ID*** and enter the expression ***RIGHT(STORE_ID,6)*** as we will exclude the prefix of the STORE_ID so that it can be mapped to the dimension IDs. Adjust the length to 6 characters.
<br>![](images/00_00_0006.png)  

9. Exit the graphical view editor and go back to the transformation flow overview.
<br>![](images/00_00_0007.png)  

10. Click on ***Create New Target Table***.
<br>![](images/00_00_0008.png)  

11. Set the business name to "Updated Sales Transactions". Verify that ***Delta Capture*** is turned on.
<br>![](images/00_00_0009.png)  

12. Deselect the target table by clicking somewhere else in the editor field. The properties for the Transformation Flow will appear on the right-hand side. Set the business name to ***TF_SalesTransactions*** and the Load Type to ***Initial and Delta***.
<br>![](images/00_00_0010.png)  

13. Save and deploy the Transformation Flow in the folder TECHED2024-DA180, afterward click on ***Run***.
<br>![](images/00_00_0011.png)  

14. Open the Data Integration Monitor to have a look at the Transformation Flow run.
<br>![](images/00_00_0012.png)

15. The Data Integration Monitor details display of the Transformation Flow run. Have a look at the messages and the section ***Metrics*** to check the number of processed records.
<br>![](images/00_00_0013.png)  

16. The Transformation Flow run should run scheduled. User consent is required to run scheduled tasks or task chains. Authorize SAP Datasphere to run these tasks.
<br>![](images/00_00_0020.png)  

17. Schedule the Transformation Flow to run once a day. It will retrieve the newest and changed records and add them to the local table. Click ***Create Schedule***.
<br>![](images/00_00_0014.png)  

18. Define the scheduling as ***Simple Schedule*** which is repeated every 10 minutes. Choose a time and select ***Create***.
<br>![](images/00_00_0015_1.png)  

19. You can go back to this monitor after new runs to see that new records are written to the target table.
<br>![](images/00_00_0021.png)  

20. The Analytic Model used until now (Sales__Analytic_Model) is based on data of local tables. We will copy the fact model and replace the source so that the sales transaction data is coming from the table updated via the transformation flow instead of data imported once via CSV. Copy the view ***Sales View - Fact***. Name it ***Sales View - Fact (Updated)***.
<br>![](images/00_00_0022.png)  

---
>:bulb: **Tip:** We create a copy of the fact view to preserve tge previously created models (view, Analytic Model, SAC Story) based on the CSV files. You will copy the existing SAC story and replace the model so that you don't need to recreate a full story. Another option would also be switching the source table of the currently used fact view so that the updated records are displayed in the already existing SAC story. 
---

21. Open the copied view ***Sales View - Fact (Updated)***. If you previously did the exercise about data access controls, the view will look as displayed on the screenshot. The approach for the view without data access control assigned and join with the product dimension is similar.
<br>![](images/00_00_0022.png)  

22. Drag and drop the table ***TECHED2024_SALES_TRANSACTIONS*** into the canvas and replace the original source table. 
<br>![](images/00_00_0024.png)  

23. Map the columns from the old source to the new source by dragging them from the left to the right side. Ensure that all nine columns are mapped and click ***Replace***.
<br>![](images/00_00_0025.png)  

24. Now the source table is replaced with the local table which is enabled for delta capture. Ensure that the view validation of ***Sales View - Fact (Updated)*** displays a green status.
<br>![](images/00_00_0019.png)  

25. Save and deploy ***Sales View - Fact (Updated)***.

26. Select ***Create Analytic Model*** (in the view properties of ***Sales View - Fact (Updated)***).

27. Save the Analytic Model as ***Sales - Analytic Model (Updated)*** and deploy it. Is now accessing delta enabled local table which is receiving updated records. 

28. We will reuse the previously created SAC Story and map it to the new updated Analytic Model accessing regularly updated data. The same is the case for the SAC story accessing the Analytic Model. 

29. Use the product switch button in the upper right corner to switch to SAC.
<br>![](images/00_00_0027.png)  

30. Switch to the ***Files*** application and copy the previously created story ***Revenue Analysis - Products***. Copy it to the same folder and name it ***Revenue Analysis - Products (Updated)***.
<br>![](images/00_00_0029.png)  

31. Open the story  ***Revenue Analysis - Products (Updated)*** and switch to the ***Edit*** mode.

32. To replace the model, access ***...*** -> ***Sales__Analytic_Model*** -> ***Replace***.
<br>![](images/00_00_0030.png)  

33. Read the warning displayed and click ***Continue***.
<br>![](images/00_00_0031.png)  

34. Read the warning displayed and click ***Continue***.
<br>![](images/00_00_0031.png)  

35. Select ***select other model***. You can replace a model in your SAC story with another compatible model. Choose the connection ***DATASPHERE*** and click on the folder with your user's ID. Select the folder ***TECHED2024-DA180*** and click on the Analytic Model ***Sales - Analytic Model (Updated)***.

36. The replace model dialog displays the objects from the replacement model and the objects that need to be mapped. Some objects will automatically be mapped if they are similar to the original objects or if they are mandatory objects. Then they will be disabled (greyed out) in this panel. Check that the mappings are done correctly like displayed in the screenshot.
<br>![](images/00_00_0032.png)

27. When you have finished mapping objects, select ***Review***. Verify that no issues have been found and click ***Replace Model***.
<br>![](images/00_00_0033.png)

## Summary

You have now created and deployed your first Transformation Flow to transform and access changing records in a scheduled approach.

You can continue with one of the optional exercises:
- [Exercise 20: Identify Top-Performing Sales Managers with Just Ask](../ex20/README.md)
- [Exercise 21: Create Row-Level Permissions based on External Hierarchy](../ex21/README.md)
- [Exercise 22: Explore the Analytic Model](../ex22/README.md)
