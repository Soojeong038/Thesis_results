
Relationship between docs
LOAD CSV WITH HEADERS FROM 'file:///doc_ent_freq_1.csv' AS row
WITH row.id AS id, row.doc_id AS docid, row.org_name AS org, toInteger(row.freq) AS freq
WHERE (docid = "2022011" or docid = "2022015" or docid = "2022014") and (org <> "stadt wien" and org <> "Stadtrechnungshofes Wien") 
MERGE (orgname:Organization {name: org})
MERGE (docu:Document {id: docid})
CREATE (orgname)-[r: related {weights:freq}] -> (docu)
return docu, r, orgname

![image](https://user-images.githubusercontent.com/97410949/214197030-41d0e61e-356c-44d9-a4c8-41a0ea3862c9.png)
