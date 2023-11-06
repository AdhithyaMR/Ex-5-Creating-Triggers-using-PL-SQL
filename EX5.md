# Ex. No: 5 Creating Triggers using PL/SQL
## DATE: 31/08/23
### AIM:
To create a Trigger using PL/SQL.

### Steps:
1. Create employee table with following attributes (empid NUMBER, empname VARCHAR(10), dept VARCHAR(10),salary NUMBER);
2. Create salary_log table with following attributes (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER,empname VARCHAR(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
3. Create a trigger named as log_salary-update.
4. Inside the trigger block, Insert the values into the salary_log table whenever the salary is updated.
5. End the trigger.
6. Update the salary of an employee in employee table.
7. Whenever a salary is updated for the employee it must be logged into the salary_log table with old salary and new salary.
8. Display the employee table, salary_log table.

### Program:
```sql
CREATE TABLE employed(
  empid NUMBER,
  empname VARCHAR2(10),
  dept VARCHAR2(10),
  salary NUMBER
);

CREATE TABLE sal_log (
  log_id NUMBER GENERATED ALWAYS AS IDENTITY,
  empid NUMBER,
  empname VARCHAR2(10),
  old_salary NUMBER,
  new_salary NUMBER,
  update_date DATE
);
-- Insert the values in the employee table
insert into employed values(1,'Nagul','AIDS',1000000);
insert into employed values(2,'Santhosh','CSE',500000)
```
### Create employee table

![270734960-ab8e1001-ad81-4cee-b147-9e6ccbffe6b7](https://github.com/AdhithyaMR/Ex-5-Creating-Triggers-using-PL-SQL/assets/118834761/1259c63f-8050-4a80-a4a9-1578bf2db666)


### Create salary_log table

![270735026-86466cf5-53f7-4063-9ccc-e364e7072d5e](https://github.com/AdhithyaMR/Ex-5-Creating-Triggers-using-PL-SQL/assets/118834761/0e61bdfa-429e-4d13-a8d7-7ae506437b09)


### PLSQL Trigger code
```sql
-- Create the trigger
CREATE OR REPLACE TRIGGER log_sal_update
BEFORE UPDATE ON employed
FOR EACH ROW
BEGIN
  IF :OLD.salary != :NEW.salary THEN
    INSERT INTO sal_log (empid, empname, old_salary, new_salary, update_date)
    VALUES (:OLD.empid, :OLD.empname, :OLD.salary, :NEW.salary, SYSDATE);
  END IF;
END;
/
-- Insert the values in the employee table
insert into employed values(1,'Nagul','AIDS',1000000);
insert into employed values(2,'Santhosh','SALES',500000);

-- Update the salary of an employee
UPDATE employed
SET salary = 60000
WHERE empid = 1;
-- Display the employee table
SELECT * FROM employed;

-- Display the salary_log table
SELECT * FROM sal_log;
```

### Output:

![270736789-98d6405f-b231-485b-b7c5-38e605977906](https://github.com/AdhithyaMR/Ex-5-Creating-Triggers-using-PL-SQL/assets/118834761/7ab39cc6-7be6-47fd-b94f-873aac551b04)


### Result:
The program has been implemented sucessfully.
