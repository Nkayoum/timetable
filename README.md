//QUESTION 3
CREATE VIEW vue AS 
SELECT DISTINCT C.codeCours, T.jourCoursDate  FROM Cours C
JOIN Typehoraire T
ON C.codeCours= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON  T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cl
ON cl.specialiteNomSpec=cls.classSpecialiteNomspec
WHERE T.jourCoursDate 
IN ('lundi','mardi','mercredi','jeudi','vendredi','samedi');

//QUESTION4
alter table etudiant 
add password varchar(10);
update etudiant set password = ora_hash(matricule) 
where matricule = valeur;

alter table enseignants 
add password varchar(10);
update enseignants set password = ora_hash(matricule)
where matricule = valeur;

//QUESTION 5
SET MARKUP HTML ON SPOOL ON PREFORMAT OFF ENTMAP ON -
HEAD "<TITLE>Department Report</TITLE> -
<STYLE type='text/css'> -
<!-- BODY {background: #DCDFFF} --> -
</STYLE>" –
 BODY "TEXT='#000000'" –
 TABLE "WIDTH='50%' BORDER='10'"
SPOOL EmploieDeTempsHTML.html
SELECT DISTINCT  T.jourCoursDate, C.VOLUMEH, C.syllabus 
FROM Cours C
JOIN Typehoraire T
ON C.syllabus= T.crsCodeCours
JOIN Jourcours J
ON J.dateJourCours=T.jourCoursDate
JOIN Coursdeclasse cls
ON T.crsCodeCours=cls.crsCodeCours
JOIN Classe Cla
ON cla.specialiteNomSpec=cls.classSpecialiteNomspec
JOIN Etudiantdeclasse et 
on cls.crsCodeCours=et.COURCODECOURS
JOIN ETUDIANT pp 
ON pp.MATRICULE=et.ETUDIANTMATRICULE
WHERE  et.ETUDIANTMATRICULE=&Matricule AND PASSWORD=ora_hash(&Password);
SPOOL OFF
