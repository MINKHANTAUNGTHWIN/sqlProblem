-------create table------
--create mainShop
create table mainShop( 
mainId int unique not null primary key,
mainName varchar(255) unique not null );

--insert main shop
insert into mainShop(mainId,mainName) values
(1,'UNION');

--create mainshoplist
create table mainShopList( 
MainId int,
MainName varchar(255),
branchshopId int primary key not null unique,
branchShopName varchar(255) unique,  
phNo varchar(255) unique, 
fax varchar(255) unique
)

--insert mainShopList
insert into mainShopList(MainId,branchshopId,branchshopname,phNo,fax) values 
(1,1,'Makishi','090-090-090','010-010-010'),
(1,2,'tsuboya','080-080-080','020-020-020'),
(1,3,'tomari','070-070-070','030-030-030');

--join mainShop and mainShopList
select mainshop.mainId,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax
from mainshop
join mainShopList
on mainshop.mainId = mainShopList.MainId;

--branchshoplist
create table branchShop(
MainId int,
MainName varchar(255),
branchshopId int,
branchshopname varchar(255) not null,
staff_id bigint unique primary key,
staff_name varchar(255) unique
);

--insert branchshoplist
insert into branchShop(mainId,branchshopid,branchshopname,staff_id,staff_name) values 
(1,1,'Makishi',6,'momonosuke');
select * from branchShop;

--join mainShop and mainShopList and branchshop
select mainShop.mainid,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchshop.mainid,
branchshop.mainname,
branchshop.branchshopid,
branchshop.branchshopname,
branchShop.staff_id,
branchShop.staff_name
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on branchshop.branchshopid = mainShopList.branchshopid;

--create product
CREATE TABLE product ( 
  MainId int,
  MainName varchar(255),
  branchshopid int,
  branchshopname varchar(255),
  staff_id int,
  staff_name varchar(255),
  productId  bigint primary key unique,
  productName varchar(255) unique not null, 
  productQuan int,
  productPrice DECIMAL(10, 2), 
  productPriceTax DECIMAL(5, 2), 
  productTotal_exclude_tax DECIMAL(10, 2),
  productTotal_include_tax decimal(10, 2)
  ) 

  -- insert product name,price and tax
  INSERT INTO product 
  (mainid,branchShopId,staff_id,productId,productName,productQuan,productPrice,productPriceTax) VALUES
  (1,1,1,1,'orange', 1, 300.00, 0.08),-- Assuming tax rate of 8%
  (1,1,1,2,'mango',1,1200.00, 0.08),
  (1,1,1,3,'banana',1,150.00,0.08),
  (1,1,1,4,'apple',1,100.00,0.08),
  (1,1,1,5,'guava',1,400.00,0.08),
  (1,1,1,6,'pineapple',1,500.00,0.08),
  (1,1,1,7,'lychee',1,600.00,0.08),
  (1,1,1,8,'strawberry',1,700.00,0.08),
  (1,1,1,9,'grape',1,800.00,0.08),
  (1,1,1,10,'kiwi',1,400.00,0.08);

  --update products and calculate excludeTax and inculdeTax 
  UPDATE product SET 
  productTotal_exclude_tax = productQuan * productPrice,
  productTotal_include_tax = (productQuan * productPrice) + (productQuan * productPrice * productPriceTax);

  --------can join here
--join mainShop and mainShopList and branchshop and product
select mainShop.mainid,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchshop.mainid,
branchshop.mainname,
branchshop.branchshopid,
branchshop.branchshopname,
branchShop.staff_id,
branchShop.staff_name,
product.MainId,
product.MainName,
product.branchshopid,
product.branchshopname,
product.staff_id,
product.staff_name,
product.productId,
product.productName, 
product.productQuan,
product.productPrice, 
product.productPriceTax, 
product.productTotal_exclude_tax,
product.productTotal_include_tax
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on mainshoplist.branchshopid = branchshop.branchshopid
join product on branchshop.branchshopid = product.branchshopid;

--can join here
--create customer
create table customer (
    MainId int,
    MainName varchar(255),
    branchshopid int,
    branchshopname varchar(255),
    phno varchar(255),
    fax varchar(255),
    staff_id bigint,
    staff_name varchar(255),
    transaction_id bigint primary key unique,
    customerId bigint,
    productId bigint,
    productName varchar(255),
    productQuan int,
    productPrice decimal(10, 2),
    productPriceTax decimal(5, 2),
    productTotal_exclude_tax decimal(10, 2),
    productTotal_include_tax decimal(10, 2)
  )


--insert customer
insert into customer
(MainId,branchshopid,staff_id,customerId,transaction_id,productId,productQuan) values 
(1,1,6,1,1,1,3);

--update customer info
UPDATE customer SET 
  productTotal_exclude_tax = productQuan * productPrice,
  productTotal_include_tax = (productQuan * productPrice) + (productQuan * productPrice * productPriceTax);

--join

--can join this
-- --join mainShop and mainShopList and branchshop and product and customer
select mainShop.mainid,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchshop.mainid,
branchshop.mainname,
branchshop.branchshopid,
branchshop.branchshopname,
branchShop.staff_id,
branchShop.staff_name,
product.MainId,
product.MainName,
product.branchshopid,
product.branchshopname,
product.staff_id,
product.staff_name,
product.productId,
product.productName, 
product.productQuan,
product.productPrice, 
product.productPriceTax, 
product.productTotal_exclude_tax,
product.productTotal_include_tax,
customer.mainid,
customer.mainname,
customer.branchshopid,
customer.branchshopname,
customer.phno,
customer.fax,
customer.staff_id,
customer.staff_name,
customer.transaction_id,
customer.customerid,
customer.productid,
customer.productname,
customer.productquan,
customer.productprice,
customer.productpricetax,
customer.producttotal_exclude_tax,
customer.producttotal_include_tax
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on branchshop.branchshopid = mainShopList.branchshopid
join product on branchshop.branchshopid = product.branchshopid
join customer on product.branchshopid  = customer.branchshopid;


--create transactions
CREATE TABLE transactions (
mainid int,
mainname varchar(255),
branchshopid int,
branchshopname VARCHAR(255),
branchshopphno varchar(255),
fax VARCHAR(255),
staff_id BIGINT,
staff_name VARCHAR(255),
transaction_id BIGINT ,
date TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
customerid BIGINT not null PRIMARY KEY unique,
productid BIGINT,
productname VARCHAR(255),
productquan INT,
productprice DECIMAL(10, 2),
productpricetax DECIMAL(5, 2),
producttotal_exclude_tax DECIMAL(10, 2),
producttotal_include_tax DECIMAL(10, 2),
paymentRecieve DECIMAL(10,2),
paymentChanges DECIMAL(10,2)
);

--insert into transactions
insert into transactions (
  mainid,
  branchShopId,
  staff_id,
  customerId,
  productId,
  productquan,
  transaction_id,
  paymentrecieve
  )
values
(1, 1, 6, 1, 1, 2, 1,2000.00) ;
-- -- (1, 1, 6, 1, 2, 1, 1),
-- -- (1, 1, 6, 1, 3, 1, 1),
-- -- (1 ,1, 6, 1, 4, 1, 1),


--upadate transaction total price,payment and change
UPDATE transactions SET 
  productTotal_exclude_tax = productQuan * productPrice,
  productTotal_include_tax = (productQuan * productPrice) + (productQuan * productPrice * productPriceTax),
  paymentchanges = paymentrecieve - producttotal_include_tax;

---- --join mainShop and mainShopList and branchshop and product and customer and transaction
select mainShop.mainid,
mainShop.mainName,
mainshoplist.mainid,
mainshoplist.mainname,
mainshoplist.branchshopid,
mainshoplist.branchshopname,
mainshoplist.phno,
mainshoplist.fax,
branchshop.mainid,
branchshop.mainname,
branchshop.branchshopid,
branchshop.branchshopname,
branchShop.staff_id,
branchShop.staff_name,
product.MainId,
product.MainName,
product.branchshopid,
product.branchshopname,
product.staff_id,
product.staff_name,
product.productId,
product.productName, 
product.productQuan,
product.productPrice, 
product.productPriceTax, 
product.productTotal_exclude_tax,
product.productTotal_include_tax,
customer.mainid,
customer.mainname,
customer.branchshopid,
customer.branchshopname,
customer.phno,
customer.fax,
customer.staff_id,
customer.staff_name,
customer.transaction_id,
customer.customerid,
customer.productid,
customer.productname,
customer.productquan,
customer.productprice,
customer.productpricetax,
customer.producttotal_exclude_tax,
customer.producttotal_include_tax,
transactions.mainid,
transactions.mainname,
transactions.branchshopid,
transactions.branchshopname,
transactions.branchshopphno,
transactions.fax,
transactions.staff_id,
transactions.staff_name,
transactions.transaction_id,
transactions.date,
transactions.customerid,
transactions.productid,
transactions.productname,
transactions.productquan,
transactions.productprice,
transactions.productpricetax,
transactions.producttotal_exclude_tax,
transactions.producttotal_include_tax,
transactions.paymentRecieve,
transactions.paymentChanges
from mainshop
join mainshoplist on mainshop.mainid = mainshoplist.mainid
join branchshop on branchshop.branchshopid = mainShopList.branchshopid
join product on branchshop.branchshopid = product.branchshopid
join customer on product.branchshopid  = customer.branchshopid
join transactions on customer.branchshopid = transactions.branchshopid;

