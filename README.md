# SQL-Assessment

//Question 1

CREATE TABLE XXBCM_ORDER_MGT 
   (	
	ORDER_REF 			VARCHAR(2000), 
	ORDER_DATE 			VARCHAR(2000), 
	SUPPLIER_NAME 		VARCHAR(2000), 
	SUPP_CONTACT_NAME 	VARCHAR(2000), 
	SUPP_ADDRESS 		VARCHAR(2000), 
	SUPP_CONTACT_NUMBER VARCHAR(2000), 
	SUPP_EMAIL 			VARCHAR(2000), 
	ORDER_TOTAL_AMOUNT 	VARCHAR(2000), 
	ORDER_DESCRIPTION 	VARCHAR(2000), 
	ORDER_STATUS 		VARCHAR(2000), 
	ORDER_LINE_AMOUNT 	VARCHA(2000), 
	INVOICE_REFERENCE 	VARCHAR2(2000), 
	INVOICE_DATE 		VARCHAR(2000), 
	INVOICE_STATUS 		VARCHAR(2000), 
	INVOICE_HOLD_REASON VARCHAR(2000), 
	INVOICE_AMOUNT 		VARCHAR(2000), 
	INVOICE_DESCRIPTION VARCHAR(2000)
   ) ;
   
   
//Question2

CREATE TABLE `db_prequisite`.`order_table` (
  `order_Ref` VARCHAR(200) NOT NULL,
  `order_Date` VARCHAR(200) NULL,
  `order_TotalAmount` VARCHAR(200) NULL,
  `order_Description` VARCHAR(200) NULL,
  `order_LineAmount` VARCHAR(200) NULL,
  PRIMARY KEY (`order_Ref`));

CREATE TABLE `db_prequisite`.`supplier_table` (
  `supplier_Name` VARCHAR(200) NULL,
  `supplier_ContactName` VARCHAR(200) NULL,
  `supplier_Address` VARCHAR(200) NULL,
  `supplier_Email` VARCHAR(200) NOT NULL,
  PRIMARY KEY (`supplier_Email`));

ALTER TABLE `db_prequisite`.`supplier_table` 
ADD COLUMN `supplier_ContactNo1` VARCHAR(200) NULL AFTER `supplier_Email`,
ADD COLUMN `supplier_ContactNo2` VARCHAR(200) NULL AFTER `supplier_ContactNo1`;

ALTER TABLE `db_prequisite`.`supplier_table` 
ADD COLUMN `supplier_StreetName` VARCHAR(200) NULL AFTER `supplier_ContactNo2`,
ADD COLUMN `supplier_Region` VARCHAR(200) NULL AFTER `supplier_StreetName`,
CHANGE COLUMN `supplier_Address` `supplier_StreetNo` VARCHAR(200) NULL DEFAULT NULL ;

ALTER TABLE `db_prequisite`.`supplier_table` 
CHANGE COLUMN `supplier_StreetName` `supplier_StreetName` VARCHAR(200) NULL DEFAULT NULL AFTER `supplier_StreetNo`,
CHANGE COLUMN `supplier_Region` `supplier_Region` VARCHAR(200) NULL DEFAULT NULL AFTER `supplier_StreetName`;

ALTER TABLE `db_prequisite`.`supplier_table` 
CHANGE COLUMN `supplier_Email` `supplier_Email` VARCHAR(200) NOT NULL AFTER `supplier_ContactNo2`;



CREATE TABLE `db_prequisite`.`invoice_table` (
  `invoice_Ref` VARCHAR(200) NOT NULL,
  `invoice_Date` VARCHAR(200) NULL,
  `invoice_Status` VARCHAR(200) NULL,
  `invoice_Hold` VARCHAR(200) NULL,
  `invoice_Amount` VARCHAR(200) NULL,
  `invoice_Description` VARCHAR(200) NULL,
  PRIMARY KEY (`invoice_Ref`));
  
  
  //Question 3
  
  CREATE PROCEDURE GetInvoice
AS
BEGIN
SET NOCOUNT ON
 
SELECT invoice_REF,invoice_Date,invoice_Status,invoice_Hold,invoice_Amount,invoice_Description  FROM 
invoice_table I
INNER JOIN xxbcm_order_mgt B ON I.invoice_REF=B.INVOICE_REFERENCE 
END


CREATE PROCEDURE GetOrder
AS
BEGIN
SET NOCOUNT ON
 
SELECT order_REF,order_Date,order_TotalAmount,order_Description,order_Status,order_LineAmount  FROM 
order_table O
INNER JOIN xxbcm_order_mgt B ON O.order_REF=B.ORDER_REF
 
END


//Question4

//Question5

CREATE PROCEDURE `procedurehighest` ()
BEGIN
Select COUNT(order_TotalAmount),supplier_Name,invoice_Ref 
AS TOTAL_ORDER 
from order_table ,supplier_table,invoice_table
Group By FORMAT (order_TotalAmount, ???99,999,990.00??? )
order by COUNT(order_TotalAmount) desc;
END

//Question6



