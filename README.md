ESTABLISHING DATASET RELATIONSHIP
The first step I took is narrowing down the inventory which means combining related tables together and picking
relevant columns to better ensure the relationship of the dataset.
I understand how finding relationship between data can further improve the speed and integrity of the data, 
so the next thing I did was establishing relationships in the data with the query below;

           CREATE TABLE inventories
           SELECT * 
           FROM mintclassics.customers c
           JOIN orders o ON c.customerNumber = o.customerNumber
           JOIN orderdetails od ON o.orderNumber = od.orderNumber
           JOIN products p ON od.productCode = p.productCode
           JOIN payments pm ON c.customerNumber = pm.customerNumber
           JOIN productlines pl ON p.productLine = pl.productLine
           JOIN warehouses w ON p.warehouseCode = w.warehouseCode


CLEANING DATASET FOR ANALYSIS
I started by cleaning and filtering missing values or characters and integers that are out of place like phone 
number or an incomplete street address. This allowed the dataset to be fully ready for analysis.

#Explain how you were able to exonerate more than one warehouse
I exonerated multiple warehouses by sorting the newly established inventory not by warehouse code but warehouse name which means
a warehouse is assigned for each category of inventory

POSSIBLE BUSINESS SOLUTIONS
-Extract related orders i.e orders that belong to the same customer
-Extract orders proximity i.e orders that are placed in the same city, state or country.
-Extract orders with the most quantity demand.
-Extract orders of customers with the highest credit limit.
-Extract orders with the highest amount
-Extract orders and sort by order date
-Extract orders with their required shipped date.
-Specify warehouse for orders


 SORTING IN-PROCESS ORDERS
Sorting orders in process of shipment and creating a table to sustain it is and should be the first solution to 
reducing inventory by allocating them to specific warehouse for processing and equally assigning a manager
to oversee the process. I created a table called 
'ordersinprocess' to execute this plan. These items can be stored in warehouse code 'b' and warehouse name 'North'. 
This was achieved by the query below;

               CREATE TABLE ordersinprocess
               SELECT distinct * 
               FROM mintclassics.inventories
               WHERE status = 'In process'

        SORTING SHIPPED ORDERS
Sorting shipped orders is another important step we have to take in order to manage our shipped inventory by assining a
manager to oversee the process. This is crucial to managing the orders that has left our inventory. These items information
can be stored in warehouse code 'b' and warehouse name 'East'. This was achieved by the query below;

              CREATE TABLE shippedorders
              SELECT distinct * 
              FROM mintclassics.inventories
              WHERE status = 'shipped'


      SORTING CANCELLED ORDERS
To further break down the inventory, I collated all cancelled orders and kept them in a table named 'cancelledorders'
and also assinged an employee to oversee development happening around there. These orders can be stored in warehouse
code 'a' and warehouse name 'North'. This was achieved by the query below;

              CREATE TABLE cancelledorders
              SELECT distinct * 
              FROM mintclassics.inventories
              WHERE status = 'cancelled'



    SORTING ORDERS ON HOLD
To get a clearer view of the inventory, it is essential to separate orders that are on hold and assign and employee
to oversee any development that might occur. These orders can be stored in warehouse code 'b' and warehouse name
'East'. This was achieved by the query below
        
             CREATE TABLE ordersonhold
             SELECT distinct * 
             FROM mintclassics.inventories
             WHERE status = 'On Hold'

   SORTING RESOLVED ORDERS
Sorting orders that has passed the vetting system can make it easier to processed and reduce the inventory. These 
orders can be stored in warehouse code 'c' and warehouse name 'West'. This was achieved by the query below;

            CREATE TABLE
            SELECT distinct * 
            FROM mintclassics.inventories
            WHERE status = 'Resolved'




