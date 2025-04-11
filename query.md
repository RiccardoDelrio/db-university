1. Selezionare tutti gli studenti nati nel 1990 (160)


SELECT * FROM db_university.students
WHERE date_of_birth LIKE '1990%'

            3	6	14:13:53	SELECT * FROM db_university.students
            WHERE date_of_birth LIKE '1990%'
            LIMIT 0, 1000	160 row(s) returned	0.000 sec / 0.000 sec


 2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

SELECT * FROM db_university.courses
where cfu > 10 ;

            3	8	14:17:05	SELECT * FROM db_university.courses
            where cfu > 10
            LIMIT 0, 1000	479 row(s) returned	0.000 sec / 0.000 sec


 3. Selezionare tutti gli studenti che hanno più di 30 anni

 SELECT * FROM db_university.students
WHERE YEAR(date_of_birth) < 1995;

            3	17	14:23:46	SELECT * FROM db_university.students
            WHERE YEAR(date_of_birth) < 1995
            LIMIT 0, 1000	1000 row(s) returned	0.000 sec / 0.000 sec

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di laurea (286)

SELECT * FROM db_university.courses
WHERE period like "I semestre" AND year LIKE "1"

            3	20	14:37:25	SELECT * FROM db_university.courses
            WHERE period like "I semestre" AND year LIKE "1"
            LIMIT 0, 1000	286 row(s) returned	0.000 sec / 0.015 sec


5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del 20/06/2020 (21)

SELECT * FROM db_university.exams
WHERE hour > "14:00:00" AND date LIKE "2020-06-20";

            3	28	14:43:05	SELECT * FROM db_university.exams
            WHERE hour > "14:00:00" AND date LIKE "2020-06-20"
            LIMIT 0, 1000	21 row(s) returned	0.000 sec / 0.000 sec


6. Selezionare tutti i corsi di laurea magistrale (38)

SELECT * FROM db_university.degrees
WHERE level LIKE "magistrale";

            3	38	14:50:09	SELECT * FROM db_university.degrees
            WHERE level LIKE "magistrale"
            LIMIT 0, 1000	38 row(s) returned	0.000 sec / 0.000 sec

7. Da quanti dipartimenti è composta l'università? (12)

SELECT count(id) as total_departments
FROM departments;


            3	47	15:01:17	SELECT name FROM db_university.departments
            LIMIT 0, 1000	12 row(s) returned	0.000 sec / 0.000 sec

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

SELECT * FROM db_university.teachers
WHERE phone  IS NULL;

3	55	15:06:33	SELECT * FROM db_university.teachers
 WHERE phone  IS NULL
 LIMIT 0, 1000	50 row(s) returned	0.000 sec / 0.000 sec