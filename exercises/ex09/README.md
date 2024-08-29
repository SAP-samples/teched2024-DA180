# Exercise 9 - Geographic Revenue Distribution

In this exercise, we will set up a story in SAP Analytics Cloud, which allows us to view the measures along a
geographic map.

1. Log On to your SAP Analytics Cloud tenant.
<br>![](images/00_00_0221.png) 
<br>

---

>:bulb: **Tip:** The system will ask you to resign in.

---

2. Select the menu ***Stories*** in the left-hand panel.

3. Select the option ***Canvas*** to create a new story.
<br>![](images/00_00_0201.png) 

4. Select ***Optimized Design Experience*** when asked which design mode to use. Click ***Create***.
<br>![](images/00_00_0222.png) 

5. Under ***Others***, select and drag the ***Geo Map*** onto the canvas.
<br>![](images/00_00_0318.png)
  
19. Resize the map so that it uses the complete canvas. You can accomplish this by opening the ***More*** menu (***...***) and selecting ***Fullscreen***.
<br>![](images/00_00_0321.png)

21. In the Builder panel on the right-hand side, select the option ***Add Layer*** for the Content Layer option.
<br>![](images/00_00_0302.png) 

22. Click on the model icon to choose your data model.
<br>![](images/00_00_0319.png)

23. Click within the search field and choose ***Select other model*** option
<br>![](images/00_00_0320.png)

24. To select the model that you want to reference in your story<br><ul><li>select ***DATASPHERE*** as the connection on the left panel</li><li>select your SPACE e.g. ***GE12345***</li><li>for our first example, select your ***Sales - Analytic Model***</li></ul>
<br>![](images/00_00_0205.png)

25. In the Builder panel, click on ***Location Dimension Required*** for the ***Location Dimension*** area.

26. Select the option ***Store Location***. This is the store location dimension we created previously based on the
longitude and latitude values for the store dimension.
<br>![](images/00_00_0310.png) 

27. Click on ***Add Measure*** for the Bubble Size.

28. Select measure ***Revenue***.
<br>![](images/00_00_0309.png) 


29. Click Add Measure / Dimension for the Bubble Color
30. Select measure ***Profit***.

31. Now open the details for the measure ***Profit*** as part of the Bubble Color
32. Open the list of Color Palette.
<br>![](images/00_00_0316.png) 

33. Select the second entry from the ***continuous*** category (red to green).
<br>![](images/00_00_0312.png) 

34. Now open the details for the Bubble Size definition.
35. Set the size to 35%.
<br>![](images/00_00_0311.png) 

36. Click ***Done*** to save your Layer.

37. Your map should look like this.
<br>![](images/00_00_0314.png) 

38. In the File menu, select ***Save*** to save your story.
39. Select the folder that matches your assigned user number.
40. Enter a Name and Description like ***Geographic Revenue Distribution***.
41. Click OK.
<br>![](images/00_00_0317.png)

## Summary

You've now created your second story based on the DATASPHERE connection to your data models in SAP Datasphere. 

You can continue with one of the optional exercises:
- [Exercise 20: Identify Top-Performing Sales Managers with Just Ask](../ex20/README.md)
- [Exercise 21: Create Row-Level Permissions based on External Hierarchy)](../ex21/README.md)
- [Exercise 22: Explore the Analytic Model](../ex22/README.md)
- [Exercise 23: Create a Transformation Flow)](../ex23/README.md)
