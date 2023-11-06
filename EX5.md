# Ex. No: 5 Creating Triggers using PL/SQL
Date:

### AIM: To create a Trigger using PL/SQL.

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
```
CREATE TABLE employee2( empid NUMBER,empname VARCHAR2(10),dept VARCHAR2(10),salary NUMBER);

CREATE TABLE sal_log (log_id NUMBER GENERATED ALWAYS AS IDENTITY, empid NUMBER, empname VARCHAR2(10), old_salary NUMBER, new_salary NUMBER,update_date DATE);

insert into employee2 values(1,'John','HR',50000);
insert into employee2 values(2,'Joe','IT',60000);
insert into employee2 values(3,'Bob','Finance',55000);
```

### Create employee table
```
CREATE TABLE employed(empid NUMBER, empname VARCHAR2(10), dept VARCHAR2(10), salary NUMBER);
```

### Create salary_log table
```
CREATE TABLE sal_log (log_id NUMBER GENERATED ALWAYS AS IDENTITY,empid NUMBER,empname VARCHAR2(10),old_salary NUMBER,new_salary NUMBER,update_date DATE);
```


### PLSQL Trigger code
```
CREATE OR REPLACE TRIGGER log_salary1_update
  2  BEFORE UPDATE ON employee2
  3  FOR EACH ROW
  4  DECLARE
  5    old_salary NUMBER;
  6    new_salary NUMBER;
  7  BEGIN
  8    old_salary := :OLD.salary;
  9    new_salary := :NEW.salary;
 10    IF old_salary <> new_salary THEN
 11      INSERT INTO sal_log1(empid, empname, old_salary, new_salary, update_date)
 12      VALUES(:OLD.empid, :OLD.empname, old_salary, new_salary, SYSDATE);
 13    END IF;
 14  END;
 15  /

update employee2 set salary= 89000 where empid=2;
```
### Output
![image](https://github.com/SanjithaBolisetti/Ex-No-5-Creating-Triggers-using-PL-SQL/assets/119393633/bca0fce8-b602-4540-81bd-f4eea7dc2fa8)

### Result:
Thus , the output has been successfully verified.
