## inner join

```sql
SELECT `courses`.`id` 'course_id', `courses`.`name` 'course_name', `degrees`.`id` 'degree_id', `degrees`.`level`, `degrees`.`name` 'degree_name'
FROM `courses`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = 'Corso di Laurea in Informatica';
```

```sql
SELECT `exams`.*,  `courses`.*
FROM `courses`
INNER JOIN `exams`
ON `exams`.`course_id`=`courses`.`id`
WHERE `courses`.`id` =144;
```

```sql
SELECT  `departments`.`name`
FROM `departments`
INNER JOIN `degrees`
ON `degrees`.`department_id`=`departments`.`id`
WHERE `degrees`.`name` LIKE '%Diritto%economia';
```

```sql
SELECT `exams`.* ,`degrees`.`name`
FROM `exams`

INNER JOIN `courses`
ON `exams`.`course_id`=`courses`.`id`

INNER JOIN `degrees`
ON `courses`.`degree_id`=`degrees`.`id`

WHERE `degrees`.`name` LIKE '%Magistrale%fisica' AND `courses`.`year` = 1;
```

```sql
SELECT DISTINCT `teachers`.*
FROM `teachers`

INNER JOIN `course_teacher`
ON `course_teacher`.`teacher_id`=`teachers`.`id`

INNER JOIN `courses`
ON `course_teacher`.`course_id`=`courses`.`id`

INNER JOIN `degrees`
ON `courses`.`degree_id`=`degrees`.`id`

WHERE `degrees`.`name` LIKE '%lettere';

```
