# Introduction

## Types de langages
Le langage SQL est composé de plusieurs "types" de langages. Ci-dessous, les quatre principaux types de langages définis pour Microsoft SQL Server.

### Langage de définition de données (DDL)
Le langage de définition de données (DDL) grère la création des objets de base de données, tels que les tables, les contraites et les procédures stockées. Les commandes DDL incluent:
 - USE
 - CREATE
 - ALTER
 - DROP

### Langage de manipulation de données (DML)
Le langage de manipulation de données (DML) est l'élément de langage qui permet d'utiliser les instructions principales:
 - SELECT
 - INSERT
 - UPDATE
 - DELETE
 - MERGE

### Langage de contrôle de données (DCL)
Le langage de contrôle de données (DCL) gère l'intégrité, à savoir la vérification de contraintes d'intégrité, mais aussi la confidentialité, à savoir le contrôle des droits d'accès et les autorisations de sécurité. Les commandes DCL incluent:
 - GRANT
 - REVOKE
 - DENY

### Langage de contrôle des transactions (TCL)
Le langage de contrôle des transactions (TCL) gère les transactions, une transaction étant un mécanisme permettant de cumuler différentes instructions vues comme une tâche unique, dont l'enchaînement est structuré et pour laquelle chaque instruction est indissociable. Les commandes TCL incluent:
 - BEGIN TRANSACTION
 - COMMIT TRANSACTION
 - ROLLBACK TRANSACTION

### Notes sur le langage SQL
 - Les instructions SQL ne sont pas sensibles à la casse
 - Les instructions SQL peuvent être saisies sur une ou plusieurs lignes
 - Les mots-clés peuvent être ni abrégés ni fractionnés sur plusieurs lignes. Ils sont généralement écrits en majuscules.
 - Les clauses sont généralement placées sur des lignes distinctes
 - Des indentations sont utilisées pour améliorer la lisibilité
 - Les instructions SQL peuvent être terminées par un point-virgule (;), mais ce n'est (parfois) pas obligatoire.

## Types de données
