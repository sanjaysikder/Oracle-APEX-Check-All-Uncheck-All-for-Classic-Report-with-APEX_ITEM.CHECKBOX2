## Oracle APEX: Check All/Uncheck All for Classic Report with APEX_ITEM.CHECKBOX2
mplementation for Check All/Uncheck All in Oracle APEX

In some cases, a user's password may be reset to a known default (e.g., 'Welcome123') or may have expired. To force these users to change their password immediately after login, follow these steps.

---

### 🔧 Implementation Steps

#### 1. Clasic Report SQL Query

Calssic report SQL query:

``` SQL 
SELECT APEX_ITEM.CHECKBOX2(ST.TERM_ID)"SELECT",
    
       ST.TERM_ID,
       ST.TERMS_CONDITION,
       ST.SL_NO
  FROM SC_TERM ST
  
```
### 2. Chenge select column label

column Heading
```
<input type="checkbox" id="checkAll" >
```
---
### 3. Added below javascript code to page Function and Global Variable Declaration

column Heading
```
 $('#checkAll').click(function () { 
   $('input:checkbox').prop('checked', this.checked); 
});
```

### 4. Create a 'ADD' button and Create a PL/SQL Process


```Plsql process

DECLARE
  l_selected_term_ids APEX_APPLICATION_GLOBAL.VC_ARR2;
BEGIN
  l_selected_term_ids := APEX_APPLICATION.G_F01;
  
  FOR i IN 1..l_selected_term_ids.COUNT LOOP
    BEGIN
       INSERT INTO CM_PITERM (PI_ID,TERMS_NAME )
    SELECT 
      :P18_PI_ID,	
      TERMS_CONDITION
    FROM SC_TERM
      WHERE TERM_ID = l_selected_term_ids(i);
    EXCEPTION
      WHEN OTHERS THEN
        -- Log errors (e.g., to a table or APEX debug)
        APEX_DEBUG.ERROR('Error inserting TERM_ID: ' || l_selected_term_ids(i) || ' - ' || SQLERRM);
    END;
  END LOOP;
END;

```
- Refrsh the terget Region/Report


 # Thank you
 ## Sanjay Sikder

 You can connect with me on [LinkedIn](https://www.linkedin.com/in/sanjay-sikder/)!
