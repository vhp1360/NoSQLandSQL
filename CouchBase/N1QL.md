<div dir='rtl'>بنام خدا</div>

```sql
SELECT * FROM tutorial WHERE fname = 'Ian';
SELECT children[0].fname AS cname FROM tutorial WHERE fname='Dave';
SELECT META(tutorial) AS meta FROM tutorial;
SELECT DISTINCT orderlines[0].productId,fname, age, ROUND(age/7)  AS age_dog_years FROM tutorial\
  WHERE fname = 'Dave' And age > 30 And  email LIKE '%@yahoo.com' And  children IS NULL;
  WHERE ANY child IN tutorial.children SATISFIES child.age > 10  END;
  WHERE ARRAY_LENGTH(children) > 0;
  
SELECT fname, email FROM tutorial USE KEYS ["dave", "ian"];
SELECT children[0:2] FROM tutorial WHERE children[0:2] IS NOT MISSING;
ORDER BY age LIMIT 10;
SELECT relation, COUNT(*) AS count FROM tutorial GROUP BY relation HAVING COUNT(*) > 1;
SELECT ARRAY child.fname FOR child IN tutorial.children END AS children_names FROM tutorial WHERE children IS NOT NULL;
SELECT t.relation, COUNT(*) AS count, AVG(c.age) AS avg_age 
  FROM tutorial t UNNEST t.children c
  WHERE c.age > 10 GROUP BY t.relation HAVING COUNT(*) > 1 ORDER BY avg_age DESC LIMIT 1 OFFSET 1;
SELECT usr.personal_details, orders FROM users_with_orders usr USE KEYS "Elinor_33313792" 
  NEST orders_with_users orders 
  ON KEYS ARRAY s.order_id FOR s IN usr.shipped_order_history END --Like join but produce reduce result
SELECT * FROM tutorial AS contact UNNEST contact.children WHERE contact.fname = 'Dave';
SELECT  u.personal_details.display_name name, s AS order_no, o.product_details  
  FROM users_with_orders u USE KEYS "Aide_48687583" UNNEST u.shipped_order_history s 
  JOIN users_with_orders o ON KEYS s.order_id;--UNNEST useful when there are nested values in ones keys
CRUD:
INSERT INTO tutorial (KEY, VALUE) VALUES ("baldwin", {"name":"Alex Baldwin", "type":"contact"});
DELETE FROM tutorial t USE KEYS "baldwin" RETURNING t;
DELETE FROM tutorial t WHERE t.title = “Mrs”;
UPDATE tutorial USE KEYS "baldwin" SET type = "actor" RETURNING tutorial.type;
SELECT T.BankCode, sum(to_number(B.Transfered_Credit))
  FROM TestBank B JOIN TestBank T ON KEYS [B.From_Account]
  WHERE T.Tag="Bank_Account_info" and b.Tag="Account_trx"
  GROUP BY T.BankCode;



```

<div dir='rtl'></div>
<div dir='rtl'></div>
<div dir='rtl'></div>
<div dir='rtl'></div>
