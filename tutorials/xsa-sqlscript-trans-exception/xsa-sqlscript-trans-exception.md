---
title: Exception Handling, COMMIT & Autonomous Transactions
description: Leveraging SQLScript in Stored Procedures & User Defined Functions
tags: [  tutorial>intermediate, topic>sql, products>sap-hana ]
---
## Prerequisites  
 - **Proficiency:** Intermediate
 - **Tutorials:** [Using Index-based Cell Access](http://go.sap.com/developer/tutorials/xsa-sqlscript-usingindexbased.html)

## Next Steps
 - [Using COMMIT Statement](http://go.sap.com/developer/tutorials/xsa-sqlscript-trans-commit.html)

## Details
### You will learn  
In this example we will exchange the dates of the scalar input parameters to prevent the error in case the start date is larger than the end date. To do so we will rely on exception handling.

### Time to Complete
**15 Min**.

---

1. Return to the `get_product_by_filter` procedure in the procedure editor. Add two additional input parameters for start and end date as shown.

	![procedure editor](1.png)

2. Add a WHERE clause to the third statement which filters the data by the start and end date input parameters.

	![where clause](2.png)

3. The completed code should look very similar to this. If you do not wish to type this code, you can reference the solution web page at `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex2_24`

	```
	PROCEDURE "dev602.procedures::get_product_by_filter" (
	```
	
4. Click "Save".

	![save](4.png)

5. Use what you have learned already and perform a build on your `hdb` module. Then return to the HRTT page and invoke the procedure.

	![HRTT](5.png)

6. Enter the values for the input parameters as shown. Then run the procedure.

	![input parameter values](6.png)

7. Results are shown.

	![results](7.png)

8. Return to the procedure called `get_product_by_filter`. We will include a check for the two scalar input parameters and throw an error in case the check fails. To do so please enter the following code after the BEGIN statement.

	![input parameter check](8.png)

9. Click “Save”.

	![save](9.png)

10. Use what you have learned already and perform a build on your `hdb` module. Then return to the HRTT page and change the input parameters as shown and run the CALL statement again.

	![HRTT](10.png)

11. You should see an error message showing user defined error 10001. If you scroll to the right, you can see the message text as well.

	![error message](11.png)

12. We do not want to stop the procedure execution by throwing a signal. Instead we will handle the exception, write the exception into a log table and continue with the procedure execution. As a prerequisite we need to create a table that we will use for logging. Therefore, go to the data folder and create a new file by right-clicking on the data folder and choosing "New", then "CDS Artifact".

	![handle exception](12.png)

13. Enter the name of the file as "log", select "Text" and click "Create".

	![file name](13.png)

14. Enter the code into the editor as shown. Make sure to substitute your group number where appropriate. If you do not wish to type this code, you can reference the solution web page at `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex2_25`

	```
	namespace dev602.data;
	```
	
15. Click “Save”.

	![save](15.png)

16. Switch back to the procedure called `get_product_by_filter`. Since we will have a DML statement in the procedure we cannot flag it read only. Please remove the "READS SQL DATA" statement.

	![remove read only flag](16.png)

17. Remove the IF statement that you inserted a little earlier.

	![remove IF](17.png)

18. Insert these DECLARE statements as shown.  Notice the last DECLARE statement is declaring a custom condition and assigning error code 10001 in the user defined number range.

	![custom condition](18.png)

19. After the last DECLARE statement, insert the following code.  This code is declaring a custom exit handler for your custom condition.  This exit handler will insert a new record in to the log table and will switch start date and end date accordingly, The surrounding block, marked by the `BEGIN/END` statements ensures that after the exception is caught, execution will continue after the block

	![exit handler](19.png)

20. Change the WHERE clause of SELECT statement for `filtered_items` as shown here. This ensures usage of the local declared date variables which contain the corrected values.

	![where clause](20.png)

21. The completed code should look very similar to the following. If you do not wish to type this code, you can reference the solution web page at `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex2_26`

	```
	PROCEDURE "dev602.procedures::get_product_by_filter" (
	```
	
22. Click “Save”.

	![save](22.png)

23. Use what you have learned already and perform a build on your `hdb` module. Then return to the HRTT page and make sure the input parameters are as shown and run the CALL statement again.

	![HRTT](23.png)

24. Notice the results of the procedure are returned.

	![results](24.png)

25. In the SQL tab, enter a SELECT statements against your `log.errors` and `log.messages` table as shown.

	![sql tab](25.png)

26. Highlight the SELECT statement for `log.errors`, and click "Run".

	![log errors](26.png)

27. You should see an error message in your table. This means that the exception was caught by the handler, and execution was allowed to continue since you saw the results of the procedure call.

	![error message](27.png)

## Next Steps
 - [Using COMMIT Statement](http://go.sap.com/developer/tutorials/xsa-sqlscript-trans-commit.html)