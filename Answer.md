Answer 1 : Relationship between product and product_Category table -  Product table and Product_Category table has many to one relationship means many product belongs to 
a single product category.  
product.category_id > product_category.id (has many to one relation),

Product Table: This  has column product_id, product_name, product_description, category_id, inventory_id , product_price etc.
Each row in the product table represent a unique table.

Product_Category  Table : This table store information about different categories of product. Each row in this table has unique product category.

For Example : If we have category such as electronics multiple products like smartphone, laptops, tablets etc can fall under this category. And each product belong to one category.
Product table includes foreign key column that references the primary key table of th eproduct category table. 

Foreign key column link the two tables, indicating which product belongs  to which category.
Foreign key column in the product table has category_id column which is the indentifier of the product category to which each product belongs.

....................................................................................................................................................
Answer 2: To ensure valid category assigned to the product we can use foreign key. Foreign key constraint enforces referential integrity by 
ensuring that the value in a foreign key column matches a value in another table's primar key column. 

We can use constraints to ensure that category_id entered in the product table
must exist in the product_Category table.

Create the product category table
create table ProductCategory table(
 id int  primary key ,
 name varchar(50) not null,
 desc varchar
);

Create the product table with a foreign key constraint

create table product(
id int primary key,
name varchar(100) not null,
desc varchar(100),
category_id int,
inventroy_id int,
price double,
discount_id int,
foreign key(Category_id) references productCategory(CategoryID)
);

Or 
we can create trigger to enforce the constraint that every product inserted
or updated in the product table includes a valid category ID.


Create trigger validateCategory BEFORE INSERT OR UPDATE ON Product 
For EACH ROW
BEGIN
 DECLARE category_count int;
 
 Select count(*) into category_count from productCategory 
 where category_id  =new.Category_id;

 IF category_count=0 then
 SIGNAL SQLSTATE '45000'
 SET message_text= 'Invalid Category_id'
 END IF;
 END;





