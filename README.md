# EX - CON QUERY CON SELECT

1. Selezionare tutti gli studenti nati nel 1990 (160)

- SELECT `id`,`name`,`surname`,`date_of_birth` FROM `students` WHERE YEAR(`date_of_birth`) = 1990;

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

- SELECT `id`,`name`,`cfu` FROM `courses` WHERE `cfu` > 10;

3. Selezionare tutti gli studenti che hanno più di 30 anni

- SELECT \* FROM `students` WHERE TIMESTAMPDIFF(year,`date_of_birth`, "2023-10-10") > 30;

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286)

- SELECT \* FROM `courses` WHERE `period` = 'I semestre' AND `year` = 1;

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21)

- SELECT \* FROM `exams` WHERE `date` = "2020-06-20" AND `hour` > "14:00:00";

6. Selezionare tutti i corsi di laurea magistrale (38)

- SELECT \* FROM `degrees` WHERE `level` = "magistrale";

7. Da quanti dipartimenti è composta l'università? (12)

- SELECT COUNT(\*) FROM `departments`;

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

- SELECT \* FROM `teachers` WHERE `phone` IS NULL;

# EX GROUP BY E JOIN

## GROUP BY

1. Contare quanti iscritti ci sono stati ogni anno

- SELECT COUNT(\*) AS `iscritti`, YEAR ( `enrolment_date` ) AS `anno_iscrizione` FROM `students` GROUP BY `anno_iscrizione`;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

- SELECT COUNT(\*) AS `insegnanti`,`office_address` AS `ufficio` FROM `teachers` GROUP BY `ufficio`;

3. Calcolare la media dei voti di ogni appello d'esame

- SELECT AVG(`vote`) AS `media` FROM `exam_student` GROUP BY `exam_id`;

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

- SELECT COUNT(\*) AS `corsi_di_laurea`, `department_id` AS `dipartimento` FROM `degrees` GROUP BY `dipartimento`;

## JOIN

1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

- SELECT `students`.`name`, `students`.`surname`,`students`.`date_of_birth`,`students`.`fiscal_code`,`students`.`enrolment_date` FROM `students` JOIN `degrees` ON `students`.degree_id = `degrees`.id WHERE `degrees`.name = "corso di laurea in economia";

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze

- SELECT \* FROM `degrees` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` WHERE `departments`.`name` = "Dipartimento di Neuroscienze" && `degrees`.`level` = "magistrale";

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

- SELECT \* FROM `courses` JOIN `course_teacher` ON `courses`.`id`= `course_teacher`.`course_id` JOIN `teachers` ON `course_teacher`.`teacher_id` = `teachers`.`id` WHERE `teachers`.`name` = "Fulvio" && `teachers`.`surname` = "Amato";

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cuisono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome

- SELECT `students`.\* FROM `students` JOIN `degrees` on `students`.`degree_id` = `degrees`.`id` JOIN `departments` ON `degrees`.`department_id` = `departments`.`id` ORDER BY `students`.`surname`,`students`.`name`;
