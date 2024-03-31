## ESERCIZIO QUERY JOIN

# QUERY 1 --> Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- - - sql
SELECT `students`.`id`, `students`.`name` AS `name_of_student`, `students`.`surname`, `students`.`date_of_birth`, `students`.`fiscal_code`, `students`.`enrolment_date`, `students`.`registration_number`, `students`.`email`, `degrees`.`name` AS `name_of_degree` 
FROM `students` 
JOIN `degrees` 
ON `students`.`degree_id` = `degrees`.`id` 
WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

- - - .

# QUERY 2 --> Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

- - - sql
SELECT `degrees`.`id`, `degrees`.`name` AS `name_of_degree`, `degrees`.`level`, `degrees`.`address`, `degrees`.`email`, `degrees`.`website`, `departments`.`name` AS `name_of_department` 
FROM `degrees` 
JOIN `departments` 
ON `degrees`.`department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Neuroscienze' 
AND `degrees`.`level` = 'magistrale';

- - - .

# QUERY 3 --> Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- - - sql
SELECT `courses`.`id`, `courses`.`name` AS `name_of_course` , `courses`.`description`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `courses`.`website` 
FROM `course_teacher` 
JOIN `courses` 
ON `course_teacher`.`course_id` = `courses`.`id` 
WHERE `teacher_id` = 44;

- - - .

# QUERY 4 --> Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

- - - sql
SELECT `students`.`id`, `students`.`name` AS `name_of_student`, `students`.`surname`, `students`.`date_of_birth`, `students`.`fiscal_code`, `students`.`enrolment_date`, `students`.`registration_number`, `students`.`email` AS `email_of_student`, 
`degrees`.`id`, `degrees`.`name` AS `name_of_degree`, `degrees`.`level`, `degrees`.`address` AS `address_of_degree`, `degrees`.`email` AS `email_of_degree`, `degrees`.`website` AS `website_of_degree`, 
`departments`.`id`, `departments`.`name` AS `name_of_department`, `departments`.`address` AS `address_of_department`, `departments`.`phone`, `departments`.`email` AS `email_of_department`, `departments`.`website` AS `website_of_department`, `departments`.`head_of_department` 
FROM `students` 
INNER JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id` 
INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
ORDER BY `students`.`name`, `students`.`surname` ASC;

- - - .

# QUERY 5 --> Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

- - - sql
SELECT `degrees`.`id` AS `id_of_degree`, `degrees`.`name` AS `name_of_degree`, `degrees`.`level`, `degrees`.`address` AS `address_of_degree`, `degrees`.`email` AS `email_of_degree`, `degrees`.`website` AS `website_of_degree`,
`courses`.`id` AS `id_of_course`, `courses`.`name` AS `name_of_course`, `courses`.`description`, `courses`.`period`, `courses`.`year`, `courses`.`cfu`, `courses`.`website` AS `website_of_course`,
`teachers`.`id` AS `id_of_teacher`, `teachers`.`name` AS `name_of_teacher`, `teachers`.`surname`, `teachers`.`phone`, `teachers`.`email` AS `email_of_teacher`, `teachers`.`office_address`, `teachers`.`office_number`
FROM `courses`
INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `course_teacher` ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`;
- - - .

# QUERY 6 --> Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)

- - - sql
SELECT `teachers`.`id`, `teachers`.`name`, `teachers`.`surname`, `teachers`.`phone`, `teachers`.`email`, `teachers`.`office_address`, `teachers`.`office_number` 
FROM `teachers` 
INNER JOIN `course_teacher` ON `course_teacher`.`teacher_id` = `teachers`.`id` 
INNER JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id` 
INNER JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id` 
INNER JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` 
WHERE `departments`.`name` = 'Dipartimento di Matematica' 
GROUP BY `teachers`.`id`;

- - - .

# QUERY 7 --> BONUS-1: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. 

- - - sql
SELECT `students`.`id`,`students`.`name`, `students`.`surname`, `students`.`date_of_birth`, `students`.`fiscal_code`, `students`.`enrolment_date`, `students`.`registration_number`, `students`.`email`, COUNT(`exam_student`.`student_id`) AS `total_attemps`, MAX(`exam_student`.`vote`) AS `max_vote`
FROM `exam_student`
INNER JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
GROUP BY `students`.`id`;
- - - .

# QUERY 7 --> BONUS-2: Successivamente, filtrare i tentativi con voto minimo 18.

- - - sql
SELECT `students`.`id`,`students`.`name`, `students`.`surname`, `students`.`date_of_birth`, `students`.`fiscal_code`, `students`.`enrolment_date`, `students`.`registration_number`, `students`.`email`, COUNT(`exam_student`.`student_id`) AS `total_attemps`, MAX(`exam_student`.`vote`) AS `max_vote`
FROM `exam_student`
INNER JOIN `students` ON `exam_student`.`student_id` = `students`.`id`
WHERE `exam_student`.`vote` >= 18
GROUP BY `students`.`id`;
- - - .