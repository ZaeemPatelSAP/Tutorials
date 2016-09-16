---
title: Intermediate Table Variables
description: Leveraging SQLScript in Stored Procedures & User Defined Functions
tags: [  tutorial>intermediate, topic>sql, products>sap-hana ]
---
## Prerequisites  
 - **Proficiency:** Intermediate
 - **Tutorials:** [Parallel Processing and Parameters](http://go.sap.com/developer/tutorials/xsa-sqlscript-parallel.html)

## Next Steps
 - [Creating Scalar User Defined Functions](http://go.sap.com/developer/tutorials/xsa-sqlscript-scalar.html)

## Details
### You will learn  
In this exercise you will modify the code of procedure `get_po_header_data` again to use a single tabular output. Existing queries will be reused based on intermediate table variables.

### Time to Complete
**15 Min**.

---

1. Return to your procedure called `get_po_header_data`.

	![Existing Procedure](1.png)
	
2. Delete the output parameters which you defined in the last section.

	![Define output](2.png)

3. Define a new output parameter as shown

	![New output](3.png)

4. Rename `EX_PO_CREATE_CNT` to `PO_CREATE_CNT`. Also rename `EX_PO_CHANGE_CNT` to `PO_CHANGE_CNT`

	![change name](4.png)

5. Modify the two SELECT statements and add `AS EID` after the `EMPLOYEEID` field.

	![modify select](5.png)

6. Next, add another SELECT statement after the 2 previous SELECT statements as shown. This statement uses the previously defined table variables.

	![add another select](6.png)

7. The completed code should be very similar to this. If you do not wish to type this code, you can reference the solution web page at `http://<hostname>:51013/workshop/admin/ui/exerciseMaster/?workshop=dev602&sub=ex2_12`

	```	
	PROCEDURE "dev602.procedures::get_po_header_data" (

8. Save the procedure

	![save Procedure](7.png)

9. Use what you have learned already and perform a build on your `hdb` module. Then return to the HRTT page and invoke the procedure.

	![HRTT](8.png)

10. Click "Run".

	![Run](9.png)

11. The results are then shown.

	![Results](10.png)
	

## Next Steps
 - [Creating Scalar User Defined Functions](http://go.sap.com/developer/tutorials/xsa-sqlscript-scalar.html)