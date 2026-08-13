# Chapter 1: Trade Off in Data Systems Architecture

OLAP -> ETL -> OLAP 

From what I have read in this chapter, they started discussing the difference between an OLAP system and a OLTP system. 

OLTP stands for Online Transaction Processing, this part of the system sits on the back end. This is the infrastructure that captures the row by row data.

OLAP stands for Online Analytics Processing. This part of the data layer sits in front of the OLTP. It holds a read only copy of the modified data captures by OLTP. 

The way I understood both terms is that OLTP happens at the Athena level at my job, every appointment, transaction, bill, etc is captures by this system. Then it is transformed and loaded into our Snowflake warehouse. The warehouse is the OLAP system, we can't modify the data that is already in there, but we can perform high cost queries. 

Another important point of the OLTP is that the capturing of data needs to happen fast. So these systems have a high throughput, mili second pace. That is another reason why we don't query (analysts) these systems, a part from the fact that the data is not ready, not in the right format. 

There's also HTAP, this is a hybrid between OLAP and OLTP. Usually used for fraud detection when you need to quickly review the data being captured.  

Enterprises have multiple OLAP and OLTP systems working together. Usually maintained independently. 