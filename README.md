# SQL Data Definition Language (DDL): ALTER Command

## Introduction to DDL

Data Definition Language (DDL) is a subset of SQL used to define and modify the structure of database objects. The main DDL commands are:

1. CREATE
2. ALTER
3. DROP
4. TRUNCATE

This document focuses on the ALTER command, particularly its application to tables.

## The ALTER Command

ALTER is used to modify the structure of existing database objects. While it can be applied to various objects like views, functions, and stored procedures, we'll concentrate on its usage with tables.

### ALTER TABLE Operations

ALTER TABLE can perform three main operations:

1. Add new elements
2. Modify existing elements
3. Delete elements

Let's explore each of these operations with examples.

#### 1. Adding a New Column

To add a new column to a table:

```sql
ALTER TABLE Employees 
ADD Test int;
```

This command adds a new column named "Test" of type integer to the Employees table.

#### 2. Modifying an Existing Column

To modify an existing column:

```sql
ALTER TABLE Employees 
ALTER COLUMN Test bigint;
```

This command changes the data type of the "Test" column from int to bigint.

#### 3. Deleting a Column

To delete a column from a table:

```sql
ALTER TABLE Employees 
DROP COLUMN Test;
```

This command removes the "Test" column from the Employees table.

## Summary Table

| Operation | Syntax | Description |
|-----------|--------|-------------|
| Add | `ALTER TABLE table_name ADD column_name datatype;` | Adds a new column to the table |
| Modify | `ALTER TABLE table_name ALTER COLUMN column_name new_datatype;` | Changes the data type of an existing column |
| Delete | `ALTER TABLE table_name DROP COLUMN column_name;` | Removes a column from the table |

## ALTER Command Flow

```mermaid
graph TD
    A[ALTER TABLE] --> B{Operation}
    B -->|Add| C[ADD COLUMN]
    B -->|Modify| D[ALTER COLUMN]
    B -->|Delete| E[DROP COLUMN]
    C --> F[New structure]
    D --> F
    E --> F
```

This diagram illustrates the flow of the ALTER TABLE command and its operations.

## Best Practices

1. **Backup**: Always backup your database before performing ALTER operations, especially in production environments.
2. **Testing**: Test ALTER operations in a development environment before applying them to production.
3. **Performance**: Be aware that ALTER operations on large tables can be time-consuming and may lock the table.
4. **Dependencies**: Consider the impact of your changes on dependent objects like views, indexes, or constraints.

## Conclusion

The ALTER command is a powerful tool for modifying database structures. While this document focused on ALTER TABLE, remember that ALTER can be used on various database objects, with syntax and available operations varying depending on the object type.

Always consider the implications of structural changes to your database, and follow best practices to ensure data integrity and system stability.


# SQL: Foreign Keys and DROP Command

## 1. Foreign Key Relationships

### 1.1 Understanding Foreign Keys

Foreign keys are used to establish relationships between tables in a relational database. In our example:

- We have an Employees table and a Departments table.
- This forms a one-to-many relationship: one department can have many employees.
- The Employees table (the "many" side) has a foreign key that references the Departments table (the "one" side).

### 1.2 Implementing Foreign Keys

#### In Table Design:

The foreign key relationship is represented as:

```sql
DepartmentNumber int REFERENCES Departments(DNumber)
```

#### Using ALTER TABLE:

To add a foreign key constraint to an existing table:

```sql
ALTER TABLE Employees
ADD FOREIGN KEY (DepartmentNumber) REFERENCES Departments(DNumber)
```

### 1.3 Visualizing Relationships in SSMS

To view and manage relationships in SQL Server Management Studio (SSMS):

1. Open your database diagram in SSMS.
2. Locate the relationship line between Employees and Departments tables.
3. Right-click on the relationship line.
4. Select "Properties" from the context menu.
5. Review the relationship details in the Properties window.

Note: Always save your diagram before making changes.

To refresh the diagram after making changes:
1. Close the current diagram window.
2. Right-click on "Database Diagrams" in the Object Explorer.
3. Select "Refresh".
4. Reopen your diagram to see the updates.

## 2. The DROP Command

The DROP command is used to remove database objects entirely. It's a powerful command that should be used with caution.

### 2.1 Dropping a Database

To remove an entire database:

```sql
DROP DATABASE CompanyG02
```

Warning: This will delete all tables, data, and other objects within the database.

### 2.2 Dropping a Table

To remove a specific table:

```sql
DROP TABLE Employees 
```

Caution: This will delete the table structure and all data within the table.

### 2.3 Dropping a Column

Unlike dropping databases or tables, dropping a column requires the ALTER TABLE command:

```sql
ALTER TABLE Employees
DROP COLUMN ColumnName
```

This removes the specified column and its data from the table.

## 3. Best Practices and Considerations

1. **Backup**: Always create a backup before performing DROP or ALTER operations, especially in production environments.

2. **Dependencies**: Before dropping objects, check for dependencies. Dropping a table or column might affect views, indexes, or constraints.

3. **Cascading Effects**: Be aware of cascading delete rules when dropping tables with foreign key relationships.

4. **Testing**: Test DROP and ALTER operations in a development environment before applying them to production.

5. **Permissions**: Ensure you have the necessary permissions to perform these operations.

6. **Documentation**: Keep your database schema documentation up-to-date after making structural changes.

## Conclusion

Understanding how to manage foreign key relationships and use the DROP command effectively is crucial for maintaining database integrity and structure. Always approach these operations with caution, especially in production environments, and ensure you understand the full implications of your actions.
