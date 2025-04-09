Modellizzare la struttura di un database per memorizzare tutti i dati riguardanti una università:
- sono presenti diversi Dipartimenti (es.: Lettere e Filosofia, Matematica, Ingegneria ecc.);
- ogni Dipartimento offre più Corsi di Laurea (es.: Civiltà e Letterature Classiche, Informatica, Ingegneria Elettronica ecc..)
- ogni Corso di Laurea prevede diversi Corsi (es.: Letteratura Latina, Sistemi Operativi 1, Analisi Matematica 2 ecc.);
- ogni Corso può essere tenuto da diversi Insegnanti;
- ogni Corso prevede più appelli d'Esame;
- ogni Studente è iscritto ad un solo Corso di Laurea;
- ogni Studente può iscriversi a più appelli di Esame;
- per ogni appello d'Esame a cui lo Studente ha partecipato, è necessario memorizzare il voto ottenuto, anche se non sufficiente. 

Pensiamo a quali entità (tabelle) creare per il nostro database e cerchiamo poi di stabilirne le relazioni.
 Infine, andiamo a definire le colonne e i tipi di dato di ogni tabella.


# Dipartimenti

- DipartimentoID INT PRIMARY KEY AUTO_INCREMENT,
- Nome VARCHAR(100) NOT NULL


# Corsi di Laurea
- CorsoLaureaID INT PRIMARY KEY AUTO_INCREMENT,
- Nome VARCHAR(100) NOT NULL,
- DipartimentoID INT,
- FOREIGN KEY (DipartimentoID) REFERENCES Dipartimenti(DipartimentoID)

# Corsi
- CorsoID INT PRIMARY KEY AUTO_INCREMENT,
- Nome VARCHAR(100) NOT NULL,
- CorsoLaureaID INT,
- FOREIGN KEY (CorsoLaureaID) REFERENCES CorsiLaurea(CorsoLaureaID)

# Insegnanti
- InsegnanteID INT PRIMARY KEY AUTO_INCREMENT,
- Nome VARCHAR(100),
- Cognome VARCHAR(100),
- Email VARCHAR(150)

# Studenti
- CorsoID INT,
- InsegnanteID INT,
- PRIMARY KEY (CorsoID, InsegnanteID),
- FOREIGN KEY (CorsoID) REFERENCES Corsi(CorsoID),
- FOREIGN KEY (InsegnanteID) REFERENCES Insegnanti(InsegnanteID)

# Appelli d'Esame
- AppelloID INT PRIMARY KEY AUTO_INCREMENT,
- CorsoID INT,
- Data DATE,
- FOREIGN KEY (CorsoID) REFERENCES Corsi(CorsoID)


# Iscrizioni agli Appelli (con voto)
- AppelloID INT,
- StudenteID INT,
- Voto INT, -- anche se non sufficiente
- PRIMARY KEY (AppelloID, StudenteID),
- FOREIGN KEY (AppelloID) REFERENCES Appelli(AppelloID),
- FOREIGN KEY (StudenteID) REFERENCES Studenti(StudenteID)


allora: 
Un Dipartimento => offre molti Corsi di Laurea

Un Corso di Laurea => contiene molti Corsi

Un Corso => può essere tenuto da più Insegnanti (relazione N:M)

Un Corso => ha molti Appelli

Uno Studente => è iscritto a un solo Corso di Laurea

Uno Studente => può iscriversi a molti Appelli

Ogni Iscrizione a un Appello => ha un Voto