---
title: "Mysql"
permalink: /mysql/
toc: true
---
### Foreign Key
>CONSTRAINT constraint_name  
>FOREIGN KEY foreign_key_name (columns)  
>REFERENCES parent_table(columns)  
>ON DELETE action  
>ON UPDATE action

- omit the ON DELETE, ON DELETE NO ACTION, ON DELETE RESTRICT  
:`will reject the deletion`	
- ON DELETE **CASCADE**: to delete records in the child table
- ON DELETE **SET NULL**: not to delete and set the foreign key column values in the child table to NULL.
	filed must accept null.

- omit the ON , ON UPDATE NO ACTION, UPDATE RESTRICT
	: reject any updates to the rows in the child table
- ON UPDATE CASCADE: action allows you to perform a cross-table update
- ON UPDATE SET NULL: action resets the values in the rows in the child table to NULL values when the rows in the parent table are updated

a -> b  
create f key in b  
a: parent table or referenced table  
b: child table or referencing table