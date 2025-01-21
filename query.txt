



1. Selezionare tutti gli studenti nati nel 1990 (160)

SELECT *
FROM `students`
WHERE `date_of_birth` LIKE "1990%";

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT *
FROM `courses`
WHERE `cfu`>10;

3. Selezionare tutti gli studenti che hanno più di 30 anni (3807)

SELECT *
FROM `students`
WHERE TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) > 30 
OR (TIMESTAMPDIFF(YEAR, `date_of_birth`, CURDATE()) = 30 AND DATEDIFF(CURDATE(), `date_of_birth`) > 365 * 30);

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT *
FROM `courses`
WHERE `year`=1 AND `period`='I semestre';

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT *
FROM `exams`
WHERE `date`='2020-06-20' AND TIME(`hour`) > '14:00:00';

6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT *
FROM `degrees`
WHERE `level` ='magistrale';

7. Da quanti dipartimenti è composta l'università? (12)

SELECT count('*') AS numero_dipartimenti
FROM `departments`


8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT count('*') AS numero_insegnanti_senza_telefono
FROM `teachers`
WHERE `phone` IS NULL;

Bonus

1. Contare quanti iscritti ci sono stati ogni anno

SELECT  year(`enrolment_date`) AS anno, count('*') AS numero_iscritti
FROM `students`
GROUP BY anno
ORDER BY anno;

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

SELECT `office_address`, count('*') AS numero_insegnanti
FROM `teachers`
GROUP BY `office_address`
ORDER BY numero_insegnanti DESC;

3. Calcolare la media dei voti di ogni appello d'esame

SELECT `exam_id`, avg(`vote`) AS media_voti
FROM `exam_student`
GROUP BY `exam_id`
ORDER BY `exam_id`;


4. Contare quanti corsi di laurea ci sono per ogni dipartimento

SELECT `department_id`, count('*') AS numero_corsi_di_laurea
FROM `degrees`
GROUP BY `department_id`
ORDER BY `department_id`;