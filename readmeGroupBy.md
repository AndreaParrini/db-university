## ESERCIZIO QUERY GROUP BY

# QUERY 1 --> Contare quanti iscritti ci sono stati ogni anno

- - - sql
SELECT COUNT(*) AS `number_of_students`, YEAR(`enrolment_date`) AS `iscription_date` FROM `students` GROUP BY `iscription_date`;
- - - .

# QUERY 2 --> Contare gli insegnanti che hanno l'ufficio nello stesso edificio

- - - sql
SELECT COUNT(*) AS `number_of_techers`, `office_address` FROM `teachers` GROUP BY `office_address`;
- - - .

# QUERY 3 --> Calcolare la media dei voti di ogni appello d'esame

- - - sql
SELECT AVG(`vote`) AS `AVG_of_exam`, `exam_id` FROM `exam_student` GROUP BY `exam_id`;
- - - .

# QUERY 4 --> Contare quanti corsi di laurea ci sono per ogni dipartimento

- - - sql
SELECT COUNT(*) AS `number_of_degrees`, `department_id` FROM `degrees` GROUP BY `department_id`;
- - - .

