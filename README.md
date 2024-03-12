# nome repo: db-university

Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:

- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente.

Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni. Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.

Utilizzare https://www.diagrams.net/ per la creazione dello schema.

Esportare quindi il diagramma in jpg e caricarlo nella repo.

---

## Parte 2

Dopo aver creato un nuovo database nel vostro phpMyAdmin e aver importato lo schema allegato, eseguite le query del file allegato.

Cosa consegnare?

Dopo aver testato le vostre query con phpMyAdmin, riportatele in un file txt e caricatelo nella vostra repo.

### 1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql
SELECT *
FROM `students`
WHERE YEAR(`date_of_birth`) LIKE '1990%';

```

### 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT *
FROM `courses`
WHERE `cfu`>10;

```

### 3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT *
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) >30;

```

### 4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

```sql
SELECT *
FROM `courses`
WHERE `period` Like 'I %' AND `year` =1;

```

### 5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

```sql
SELECT *
FROM `exams`
WHERE `date`='2020-06-20' AND HOUR(`hour`) >= 14;
```

### 6. Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT *
FROM `degrees`
WHERE `level` = 'magistrale';

```

### 7. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT COUNT(*) AS n_dipartimenti
FROM `departments`;

```

### 8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT COUNT(*) as 'insegnanti_senza_telefono'
FROM `teachers`
WHERE `phone` IS NULL;
```

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
