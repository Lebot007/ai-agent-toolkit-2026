# Oracle Database - Administracao e Desenvolvimento

## O que e
Sistema de gerenciamento de banco de dados relacional enterprise da Oracle.

## SQL Oracle Especifico

### ROWNUM (Pagination)
SELECT * FROM (
    SELECT a.*, ROWNUM rnum FROM (
        SELECT * FROM employees ORDER BY employee_id
    ) a WHERE ROWNUM <= 20
) WHERE rnum >= 10;

### FETCH FIRST (12c+)
SELECT * FROM employees
ORDER BY salary DESC
FETCH FIRST 10 ROWS ONLY;

### MERGE (Upsert)
MERGE INTO target_table t
USING source_table s
ON (t.id = s.id)
WHEN MATCHED THEN
    UPDATE SET t.name = s.name, t.value = s.value
WHEN NOT MATCHED THEN
    INSERT (id, name, value)
    VALUES (s.id, s.name, s.value);

### PIVOT
SELECT * FROM (
    SELECT department, job_id, salary
    FROM employees
) PIVOT (
    AVG(salary)
    FOR job_id IN ('IT_PROG' AS IT, 'SA_REP' AS Sales, 'ST_CLERK' AS Clerk)
);

### UNPIVOT
SELECT * FROM sales
UNPIVOT (
    amount FOR quarter IN (q1, q2, q3, q4)
);

## PL/SQL

### Procedura Basica
CREATE OR REPLACE PROCEDURE update_salary(
    p_employee_id IN NUMBER,
    p_increase_pct IN NUMBER
) AS
    v_current_salary NUMBER;
BEGIN
    SELECT salary INTO v_current_salary
    FROM employees
    WHERE employee_id = p_employee_id;
    
    UPDATE employees
    SET salary = v_current_salary * (1 + p_increase_pct/100)
    WHERE employee_id = p_employee_id;
    
    COMMIT;
EXCEPTION
    WHEN NO_DATA_FOUND THEN
        DBMS_OUTPUT.PUT_LINE('Employee not found');
    WHEN OTHERS THEN
        ROLLBACK;
        RAISE;
END;

### Funcao
CREATE OR REPLACE FUNCTION calculate_bonus(
    p_employee_id IN NUMBER
) RETURN NUMBER AS
    v_salary NUMBER;
    v_bonus NUMBER;
BEGIN
    SELECT salary INTO v_salary
    FROM employees
    WHERE employee_id = p_employee_id;
    
    IF v_salary > 10000 THEN
        v_bonus := v_salary * 0.10;
    ELSE
        v_bonus := v_salary * 0.05;
    END IF;
    
    RETURN v_bonus;
END;

### Cursor
DECLARE
    CURSOR emp_cursor IS
        SELECT employee_id, name, salary
        FROM employees
        WHERE department_id = 10;
    v_emp emp_cursor%ROWTYPE;
BEGIN
    OPEN emp_cursor;
    LOOP
        FETCH emp_cursor INTO v_emp;
        EXIT WHEN emp_cursor%NOTFOUND;
        DBMS_OUTPUT.PUT_LINE(v_emp.name || ': ' || v_emp.salary);
    END LOOP;
    CLOSE emp_cursor;
END;

### Triggers
CREATE OR REPLACE TRIGGER emp_audit_trigger
AFTER INSERT OR UPDATE OR DELETE ON employees
FOR EACH ROW
BEGIN
    IF INSERTING THEN
        INSERT INTO audit_log (action, employee_id, timestamp)
        VALUES ('INSERT', :NEW.employee_id, SYSTIMESTAMP);
    ELSIF UPDATING THEN
        INSERT INTO audit_log (action, employee_id, timestamp)
        VALUES ('UPDATE', :NEW.employee_id, SYSTIMESTAMP);
    ELSIF DELETING THEN
        INSERT INTO audit_log (action, employee_id, timestamp)
        VALUES ('DELETE', :OLD.employee_id, SYSTIMESTAMP);
    END IF;
END;

## Performance Tuning

### Execution Plan
EXPLAIN PLAN FOR
SELECT * FROM employees WHERE department_id = 10;

SELECT * FROM TABLE(DBMS_XPLAN.DISPLAY);

### Hints
SELECT /*+ INDEX(employees emp_dept_idx) */ *
FROM employees
WHERE department_id = 10;

### Indexes
CREATE INDEX emp_name_idx ON employees(last_name, first_name);
CREATE BITMAP INDEX emp_dept_bmp_idx ON employees(department_id);
CREATE INDEX emp_salary_idx ON employees(salary) WHERE salary > 50000;

### Partitioning
CREATE TABLE sales (
    sale_id NUMBER,
    sale_date DATE,
    amount NUMBER
) PARTITION BY RANGE (sale_date) (
    PARTITION sales_q1 VALUES LESS THAN (TO_DATE('2024-04-01', 'YYYY-MM-DD')),
    PARTITION sales_q2 VALUES LESS THAN (TO_DATE('2024-07-01', 'YYYY-MM-DD')),
    PARTITION sales_q3 VALUES LESS THAN (TO_DATE('2024-10-01', 'YYYY-MM-DD')),
    PARTITION sales_q4 VALUES LESS THAN (MAXVALUE)
);

## Administracao

### Users e Privileges
CREATE USER app_user IDENTIFIED BY password;
GRANT CONNECT, RESOURCE TO app_user;
GRANT SELECT, INSERT, UPDATE ON employees TO app_user;

### Tablespaces
CREATE TABLESPACE app_data
DATAFILE '/u01/app/oracle/oradata/app_data01.dbf'
SIZE 100M
AUTOEXTEND ON NEXT 10M MAXSIZE UNLIMITED;

### Backup (RMAN)
RMAN> BACKUP DATABASE;
RMAN> BACKUP ARCHIVELOG ALL;
RMAN> RESTORE DATABASE;
RMAN> RECOVER DATABASE;

## Best Practices

### SQL
- Usar bind variables
- Evitar SELECT *
- Usar EXISTS ao inves de IN
- Analisar execution plans

### PL/SQL
- Tratar exceptions adequadamente
- Usar BULK COLLECT para performance
- Modularizar codigo

### Performance
- Criar indexes apropriados
- Usar partitioning para tabelas grandes
- Monitorar AWR reports

## Quando Usar
- Aplicacoes enterprise
- Sistemas transacionais de alto volume
- Data warehousing
- Ambientes que requerem suporte Oracle