JOIN  
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia  
```sql
SELECT studenti.* 
FROM studenti 
JOIN corsi_laurea ON studenti.CorsoLaureaID = corsi_laurea.CorsoLaureaID 
WHERE corsi_laurea.Nome = 'Economia';
```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di Neuroscienze  
```sql
SELECT corsi_laurea.* 
FROM corsi_laurea 
JOIN dipartimenti ON corsi_laurea.DipartimentoID = dipartimenti.DipartimentoID 
WHERE dipartimenti.Nome = 'Neuroscienze' AND corsi_laurea.Nome LIKE '%Magistrale%';
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)  
```sql
SELECT corsi.* 
FROM corsi 
JOIN corsi_insegnanti ON corsi.CorsoID = corsi_insegnanti.CorsoID 
WHERE corsi_insegnanti.InsegnanteID = 44;
```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome  
```sql
SELECT studenti.Nome, studenti.Cognome, corsi_laurea.Nome AS CorsoLaurea, dipartimenti.Nome AS Dipartimento 
FROM studenti 
JOIN corsi_laurea ON studenti.CorsoLaureaID = corsi_laurea.CorsoLaureaID 
JOIN dipartimenti ON corsi_laurea.DipartimentoID = dipartimenti.DipartimentoID 
ORDER BY studenti.Cognome, studenti.Nome;
```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti  
```sql
SELECT corsi_laurea.Nome AS CorsoLaurea, corsi.Nome AS Corso, insegnanti.Nome AS Insegnante, insegnanti.Cognome 
FROM corsi_laurea 
JOIN corsi ON corsi.CorsoLaureaID = corsi_laurea.CorsoLaureaID 
JOIN corsi_insegnanti ON corsi.CorsoID = corsi_insegnanti.CorsoID 
JOIN insegnanti ON corsi_insegnanti.InsegnanteID = insegnanti.InsegnanteID;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)  
```sql
SELECT DISTINCT insegnanti.* 
FROM insegnanti 
JOIN corsi_insegnanti ON insegnanti.InsegnanteID = corsi_insegnanti.InsegnanteID 
JOIN corsi ON corsi.CorsoID = corsi_insegnanti.CorsoID 
JOIN corsi_laurea ON corsi.CorsoLaureaID = corsi_laurea.CorsoLaureaID 
WHERE corsi_laurea.DipartimentoID = 54;
```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.  
```sql
SELECT studenti.StudenteID, appelli.CorsoID, COUNT(*) AS Tentativi, MAX(iscrizioni_appelli.Voto) AS VotoMassimo 
FROM iscrizioni_appelli 
JOIN studenti ON iscrizioni_appelli.StudenteID = studenti.StudenteID 
JOIN appelli ON iscrizioni_appelli.AppelloID = appelli.AppelloID 
GROUP BY studenti.StudenteID, appelli.CorsoID 
HAVING VotoMassimo >= 18;
```

GROUP BY  
1. Contare quanti iscritti ci sono stati ogni anno  
```sql
SELECT YEAR(DataIscrizione) AS Anno, COUNT(*) AS NumeroIscritti 
FROM studenti 
GROUP BY YEAR(DataIscrizione);
```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio  
```sql
SELECT Edificio, COUNT(*) AS NumeroInsegnanti 
FROM insegnanti 
GROUP BY Edificio;
```

3. Calcolare la media dei voti di ogni appello d'esame  
```sql
SELECT appelli.AppelloID, AVG(iscrizioni_appelli.Voto) AS MediaVoti 
FROM iscrizioni_appelli 
JOIN appelli ON iscrizioni_appelli.AppelloID = appelli.AppelloID 
GROUP BY appelli.AppelloID;
```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento  
```sql
SELECT dipartimenti.Nome AS Dipartimento, COUNT(corsi_laurea.CorsoLaureaID) AS NumeroCorsiLaurea 
FROM dipartimenti 
JOIN corsi_laurea ON dipartimenti.DipartimentoID = corsi_laurea.DipartimentoID 
GROUP BY dipartimenti.Nome;
```

:puntare_a_destra: RIPASSINO SELECT (extra bonus opzionale per il weekend):  
1. Selezionare tutti gli insegnanti  
```sql
SELECT * FROM insegnanti;
```

2. Selezionare tutti i referenti per ogni dipartimento  
```sql
SELECT dipartimenti.Nome AS Dipartimento, referenti.* 
FROM referenti 
JOIN dipartimenti ON referenti.DipartimentoID = dipartimenti.DipartimentoID;
```

3. Selezionare tutti gli studenti il cui nome inizia per "E" (373)  
```sql
SELECT * FROM studenti 
WHERE Nome LIKE 'E%';
```

4. Selezionare tutti gli studenti che si sono iscritti nel 2021 (734)  
```sql
SELECT * FROM studenti 
WHERE YEAR(DataIscrizione) = 2021;
```

5. Selezionare tutti i corsi che non hanno un sito web (676)  
```sql
SELECT * FROM corsi 
WHERE website IS NULL;
```

6. Selezionare tutti gli insegnanti che hanno un numero di telefono (50)  
```sql
SELECT * FROM insegnanti 
WHERE Telefono IS NOT NULL;
```

7. Selezionare tutti gli appelli d'esame dei mesi di giugno e luglio 2020 (2634)  
```sql
SELECT * FROM appelli 
WHERE YEAR(Data) = 2020 AND MONTH(Data) IN (6, 7);
```

8. Qual è il numero totale degli studenti iscritti? (5000)  
```sql
SELECT COUNT(*) AS NumeroTotaleStudenti 
FROM studenti;
```
