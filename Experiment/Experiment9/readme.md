# experiment 9

**name:** satyam singh  
**uid:** 24bcs12662

## aim

implement a row-level before update trigger on the salary_hike table to restrict salary increases to 15%.

## problem statement

create a before update row-level trigger on salary_hike so that if :new.salary exceeds :old.salary by more than 15%, it raises a user-defined exception with a specific message.

## sql query

### trigger with salary hike validation ([9.sql](9.sql))

```sql
create or replace trigger trg_salary_hike_limit
before update of salary on salary_hike
for each row
declare
    ex_salary_hike_limit exception;
begin
    if :new.salary > :old.salary * 1.15 then
        raise ex_salary_hike_limit;
    end if;
exception
    when ex_salary_hike_limit then
        raise_application_error(-20051, 'salary increase cannot exceed 15% of old salary');
end;
/
```

## result

the trigger was created successfully and now blocks salary updates above the 15% limit with a custom error.
