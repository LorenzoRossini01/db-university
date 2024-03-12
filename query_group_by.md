### 1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT year(`enrolment_date`) 'anno_di_iscrizione',
COUNT(*) 'numero_iscritti'
FROM `students`
GROUP BY year(`enrolment_date`);
```

### 2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT `office_address` 'office_address',
COUNT(*) 'numero_insegnanti_per_indirizzo'
FROM `teachers`
GROUP BY `office_address`;
```

### 3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT `exam_id` 'esame',
AVG(`vote`) 'media_voti'
FROM `exam_student`

GROUP by `exam_id`;
```

### 4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT `department_id` 'department_id',
COUNT(*) 'n_corsi_di_laure'
FROM `degrees`

GROUP by `department_id`;
```
