## ESERCIZIO QUERY

# QUERY 1 --> Selezionare tutti gli studenti nati nel 1990 (160)

- - - sql
SELECT * FROM `students` WHERE YEAR(date_of_birth) = '1990';
- - - .

# QUERY 2 --> Selezionare tutti i corsi che valgono più di 10 crediti (479)

- - - sql
SELECT * FROM `courses` WHERE `cfu` > 10;
- - - .

# QUERY 3 --> Selezionare tutti gli studenti che hanno più di 30 anni

- - - sql
SELECT * FROM `students` WHERE YEAR(NOW()) - YEAR(`date_of_birth`) > 30;
- - - .

# QUERY 4 --> Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

- - - sql
SELECT * FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;
- - - .

# QUERY 5 --> Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

- - - sql
SELECT * FROM `exams` WHERE `date` = '2020-06-20' AND `hour` > '14:00:00';
- - - .

# QUERY 6 --> Selezionare tutti i corsi di laurea magistrale (38)

- - - sql
SELECT * FROM `degrees` WHERE `level` = 'magistrale';
- - - .

# QUERY 7 --> Da quanti dipartimenti è composta l'università? (12)

- - - sql
SELECT COUNT(*) AS total_departments FROM `departments`;
- - - .

# QUERY 8 --> Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

- - - sql
SELECT COUNT(*) AS teachers_no_phone FROM `teachers` WHERE `phone` IS NULL;
- - - .