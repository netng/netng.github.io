---
layout: post
title: "MySQL query export to csv"
categories: bashscript
---

Below is an example exporting the result from mysql select query to csv.

```
MariaDB [my_db]> select a.fullname, a.code_group, b.title,  jml_q as total_questions, d.terisi as pertanyaan_terisi from user a inner join respondent_category b on a.category_id = b.id left outer join questionnaire_user c on a.id = c.userid left outer join (select userid, count(*) as terisi from questionnaire_user_answer group by userid) d on a.id = d.userid inner join (select id, title, respondentcategoryid,jml_q from questionnaire x inner join(select questionnaireid, count(*) jml_q from questionnaire_question group by questionnaireid) y on x.id = y.questionnaireid ) xx on a.category_id = xx.respondentcategoryid where role = 12 and a.deleted = 0 into outfile '/tmp/export_file.csv' FIELDS TERMINATED BY ',' ENCLOSED BY '"' LINES TERMINATED BY '\n';
Query OK, 333 rows affected, 1 warning (0.043 sec)

MariaDB [my_db]> exit
```

Above lots of queries, but just focus to the last on `into outfile '/tmp/export_file.csf'...`
