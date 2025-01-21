# db-university

//esercizio del 20/01/2025


//prima pagina 

1. Contare quanti iscritti ci sono stati ogni anno

COUNT(`enrolment_date`) AS `iscrizioni`,
YEAR(`enrolment_date`) AS `anno`
FROM `students`
GROUP BY `anno`
ORDER BY(`anno`) ASC;
___________________________________________________________________________

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

office_address,
COUNT(`name`)
FROM teachers
GROUP BY `office_address`;
___________________________________________________________________________

3. Calcolare la media dei voti di ogni appello d'esame

`exam_id` AS `esame`,
AVG(`vote`) AS `media_voti`
FROM exam_student
INNER JOIN exams ON exam_student.exam_id = exams.id
GROUP BY `esame`;
___________________________________________________________________________

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT `department_id`, COUNT(*) AS `number_courses`
FROM `degrees`
GROUP BY `department_id`;
___________________________________________________________________________

//seconda pagina 

1. Selezionare tutti gli studenti nati nel 1990 (160)

SELECT * 
FROM students
WHERE YEAR(`date_of_birth`) = 1990;
___________________________________________________________________________

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT * FROM courses LIMIT 10;
___________________________________________________________________________

3. Selezionare tutti gli studenti che hanno più di 30 anni
SELECT * 

FROM students
WHERE `date_of_birth` <= '1995-01-01';
___________________________________________________________________________

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

SELECT * FROM courses
WHERE `period` = "I semestre" AND `year` = 1 
;
___________________________________________________________________________

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)

SELECT * FROM exams
WHERE `hour` >= "14:00:00" AND `date` = "2020-06-20";
___________________________________________________________________________

6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT * FROM degrees
WHERE `level` = "magistrale"
;
___________________________________________________________________________

7. Da quanti dipartimenti è composta l'università? (12)

SELECT COUNT(*) FROM departments;
___________________________________________________________________________

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT * FROM db_university.teachers
WHERE `phone` IS NULL;
___________________________________________________________________________

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
degree_id, inserire un valore casuale)

INSERT INTO db_university.students (`name`, `surname`, `email`, `degree_id`, `date_of_birth`, `fiscal_code`, `enrolment_date`, `registration_number`)
VALUES ('Alessio', 'Tinaglia', 'email@pippo.it', 1, '1998-01-11', 'ABC12345D', '2023-09-01', '205');

SELECT *
FROM db_university.students
WHERE `name` = "Alessio"
___________________________________________________________________________

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

UPDATE `teachers` SET `office_number` = 126
WHERE `id` = 58
___________________________________________________________________________

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

DELETE FROM `students`
WHERE `id` = 5300
___________________________________________________________________________


// esercizio del 21/01/2025

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

SELECT `students`.`name`, `students`.`surname`,`degrees`.`name` AS `degree_name` FROM `students`
JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
WHERE `degrees`.`name` = "Corso di Laurea in Economia"
___________________________________________________________________________

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
Neuroscienze

SELECT `degrees`.`name` AS `degree_name`
FROM `degrees`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `degrees`.`level` = "magistrale"
AND `departments`.`name` = "Dipartimento di Neuroscienze";
___________________________________________________________________________

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

SELECT `courses`.`name` AS `course_name`
FROM `courses`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`
WHERE `teachers`.`id` = 44;
___________________________________________________________________________

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

SELECT `students`.`name` AS `student_name`, `students`.`surname` AS `student_surname`,  `degrees`.`name` AS `degree_name`,  `departments`.`name` AS `department_name`
FROM `students`
JOIN `degrees` ON `students`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname` ASC, `students`.`name` ASC;
___________________________________________________________________________

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

SELECT  `degrees`.`name` AS `degree_name`,  `courses`.`name` AS `course_name`, `teachers`.`name` AS `teacher_name`,  `teachers`.`surname` AS `teacher_surname`
FROM `degrees`
JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id`
JOIN `course_teacher` ON `courses`.`id` = `course_teacher`.`course_id`
JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id`
ORDER BY `degrees`.`name`, `courses`.`name`, `teachers`.`surname`, `teachers`.`name`;
___________________________________________________________________________

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
Matematica (54)

SELECT DISTINCT `teachers`.`name`, `teachers`.`surname`
FROM `teachers`
JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id`
JOIN `courses` ON `course_teacher`.`course_id` = `courses`.`id`
JOIN `degrees` ON `courses`.`degree_id` = `degrees`.`id`
JOIN `departments` ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`name` = 'Dipartimento di Matematica';
___________________________________________________________________________

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
per ogni esame, stampando anche il voto massimo. Successivamente,
filtrare i tentativi con voto minimo 18.

