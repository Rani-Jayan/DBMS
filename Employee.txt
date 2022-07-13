-- Employee Write a PL/SQL block to display total salary of all employees using cursor. --

CREATE TABLE employee (employee_id INT PRIMARY KEY, employee_name VARCHAR(20), salary INT, comm INT);
INSERT INTO employee VALUES(&id, '&name', &salary, '&com');

SELECT * FROM employee;

SET serveroutput on;
DECLARE 
    eid employee.employee_id %type;
    ena employee.employee_name %type;
    esal employee.salary %type;
    ecomm employee.comm%type;
CURSOR eselect IS SELECT employee_id, employee_name, salary, comm FROM employee;
    ts number(8, 2);
BEGIN 
    OPEN eselect;
    dbms_output.put_line('......................');
    LOOP
    FETCH eselect INTO eid, ena, esal, ecomm;
    EXIT WHEN (eselect%notfound);
    ts:= esal+NVL(ecomm,0);
    dbms_output.put_line('Employee Id: '|| to_char(eid));
    dbms_output.put_line('Employee Name: '||ena);
    dbms_output.put_line('Total Salary: '|| to_char(ts));
    dbms_output.put_line('......................');
    END LOOP;
    CLOSE eselect;
END;
/