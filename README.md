# db-university

//esercizio del 20/01/2025


//prima pagina 

1. Contare quanti iscritti ci sono stati ogni anno

COUNT(`enrolment_date`) AS `iscrizioni`,
YEAR(`enrolment_date`) AS `anno`
FROM `students`
GROUP BY `anno`
ORDER BY(`anno`) ASC;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

office_address,
COUNT(`name`)
FROM teachers
GROUP BY `office_address`;

3. Calcolare la media dei voti di ogni appello d'esame

`exam_id` as `esame`,
AVG(`vote`) AS `media_voti`
FROM exam_student
INNER JOIN exams ON exam_student.exam_id = exams.id
GROUP BY `esame`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento


//seconda pagina 

1. Selezionare tutti gli studenti nati nel 1990 (160)

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

3. Selezionare tutti gli studenti che hanno più di 30 anni

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
laurea (286)

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
20/06/2020 (21)

6. Selezionare tutti i corsi di laurea magistrale (38)

7. Da quanti dipartimenti è composta l'università? (12)

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
degree_id, inserire un valore casuale)

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9