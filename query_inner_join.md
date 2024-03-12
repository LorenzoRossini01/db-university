### 1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT
`students`.`id` 'id_studente',
`students`.`name` 'nome',
`students`.`surname` 'cognome',
`degrees`.`name` 'nome_dipartimento'

FROM `students`

INNER JOIN `degrees`
ON `degrees`.`id`=`students`.`degree_id`

WHERE `degrees`.`name` ='Corso di Laurea in Economia';
```

### 2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

```sql
SELECT *
FROM `degrees`

INNER JOIN `departments`
ON `departments`.`id` =`degrees`.`department_id`

WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
 AND `degrees`.`level` = 'magistrale';
```

### 3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT *
FROM `courses`

INNER JOIN `course_teacher`
ON `course_teacher`.`course_id`=`courses`.`id`

INNER JOIN `teachers`
ON `teachers`.`id`=`course_teacher`.`teacher_id`

WHERE `teachers`.`id` =44;
```

### 4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

```sql
SELECT
`students`.*,
`degrees`.*,
`departments`.*
FROM `students`

INNER JOIN `degrees`
ON `degrees`.`id` = `students`.`degree_id`

INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`


ORDER BY `students`.`surname` ASC;
```

### 5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT `degrees`.*,
`courses`.*,
`teachers`.*
FROM `degrees`

INNER JOIN `courses`
ON `courses`.`degree_id`=`degrees`.`id`

INNER JOIN `course_teacher`
ON `course_teacher`.`course_id`=`courses`.`id`

INNER JOIN `teachers`
ON `teachers`.`id`=`course_teacher`.`teacher_id`;
```

### 6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

```sql
SELECT DISTINCT `teachers`.* ,`departments`.`name`
FROM `teachers`

INNER JOIN `course_teacher`
ON `teachers`.`id`=`course_teacher`.`teacher_id`

INNER JOIN `courses`
ON `course_teacher`.`course_id`=`courses`.`id`

INNER JOIN `degrees`
ON `courses`.`degree_id`=`degrees`.`id`

INNER JOIN `departments`
ON `departments`.`id` = `degrees`.`department_id`

WHERE `departments`.`name` ='Dipartimento di Matematica';
```

### 7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.

```sql
SELECT DISTINCT
`students`.`name` ,`students`.`surname`,
`courses`.`name` 'nome_corso',

`student_id`,`exam_id`,
COUNT(`exam_id`),
COUNT(`student_id`),
MAX(`vote`)

FROM `exam_student`

INNER JOIN `students`
ON `students`.`id`= `exam_student`.`student_id`

INNER JOIN `exams`
ON `exams`.`id`= `exam_student`.`exam_id`

INNER JOIN `courses`
ON `courses`.`id`= `exams`.`course_id`

GROUP BY `student_id`,`exam_id`
HAVING MAX(`vote`) >18
ORDER BY `nome_corso` ASC
```
