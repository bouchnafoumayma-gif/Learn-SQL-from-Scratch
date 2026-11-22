# 🗄️ Cours SQL – Séance 1 : Découvrir SQL

**Club informatique 01** · Niveau : débutant complet · Durée : environ 2 h 30



---

## 🎯 Objectifs de la séance

À la fin de cette séance, tu sauras :

- expliquer ce qu'est une base de données et à quoi sert SQL ;
- reconnaître une **table**, une **ligne**, une **colonne** et une **clé primaire** ;
- lire des données avec `SELECT`, les filtrer avec `WHERE`, les trier avec `ORDER BY` ;
- ajouter, modifier et supprimer des données avec `INSERT`, `UPDATE` et `DELETE` ;
- calculer avec `COUNT`, `AVG`, `MIN`, `MAX`, regrouper avec `GROUP BY` et filtrer les groupes avec `HAVING` ;
- comprendre **dans quel ordre** SQL exécute une requête.

## 🗺️ Programme

| Partie | Contenu | Durée |
|---|---|---|
| 1 | Introduction | 10 min |
| 2 | Vocabulaire de base | 15 min |
| 3 | Présentation de la base du club | 10 min |
| 4 | Première requête : `SELECT` | 20 min |
| 5 | Exercices 1 (sur papier) | 15 min |
| 6 | Modifier les données | 15 min |
| 7 | Exercices 2 (sur papier) | 10 min |
| 8 | Calculs, regroupements et `HAVING` | 30 min |
| 9 | Exercice final : l'ordre d'exécution | 20 min |
| 10 | Conclusion et mini-défi | 10 min |

---

## 1. Introduction (10 min)

### C'est quoi une base de données ?

Une **base de données** est un endroit organisé où l'on range des informations, pour les retrouver facilement.

Exemples du quotidien :

- le **carnet de contacts** de ton téléphone (nom, numéro, email) ;
- un **tableau Excel** avec une liste d'étudiants ;
- les **produits** d'un site de vente en ligne ;
- les **comptes** et les **publications** d'un réseau social.

### C'est quoi SQL ?

**SQL** (prononcé « es-que-èl ») veut dire *Structured Query Language*, c'est-à-dire « langage de requêtes structuré ».

C'est le langage qu'on utilise pour **parler à une base de données**. Avec SQL, on peut lui dire :

- « Montre-moi tous les membres du club » ;
- « Ajoute un nouveau membre » ;
- « Change la ville de cette personne ».

> 💡 **Une requête** est simplement une phrase écrite en SQL pour poser une question ou donner un ordre à la base de données.

### À quoi ça sert dans la vraie vie ?

Presque toutes les applications utilisent une base de données : sites de e-commerce, applications de banque, réseaux sociaux, jeux vidéo, applications de l'école... Savoir SQL est donc très utile en informatique.

---

## 2. Le vocabulaire de base (15 min)

Une base de données contient des **tables**. Une table ressemble à un tableau Excel.

Voici un extrait de la table `membres` du club :

| id | prenom | nom | age | filiere | ville |
|---|---|---|---|---|---|
| 1 | Salma | Alaoui | 19 | Informatique | Rabat |
| 2 | Yassine | Bennani | 21 | Réseaux | Salé |
| 3 | Imane | Tazi | 18 | Informatique | Rabat |

### Les mots à retenir

| Mot | Définition | Exemple |
|---|---|---|
| **Table** | Un tableau qui range un type d'informations | `membres` |
| **Colonne** (ou champ) | Une catégorie d'information, verticale | `prenom`, `age` |
| **Ligne** (ou enregistrement) | Une fiche complète, horizontale | Toute la ligne de Salma |
| **Clé primaire** | Un identifiant **unique** pour chaque ligne | `id` |

### Pourquoi une clé primaire ?

Imagine deux membres qui s'appellent tous les deux « Sara Alaoui ». Comment les différencier ? Avec leur `id` : chaque ligne a un numéro unique, qui n'est jamais répété.

### Les types de données de base

Chaque colonne accepte un certain type de données :

| Type | Sert à stocker | Exemple |
|---|---|---|
| `INTEGER` | Un nombre entier | `19` |
| `TEXT` | Du texte | `'Rabat'` |
| `DATE` | Une date (souvent écrite en texte) | `'2026-09-15'` |

> ⚠️ **Règle importante :** en SQL, le texte s'écrit toujours entre **apostrophes simples** `'...'`. Les nombres s'écrivent sans apostrophes.

### ✅ Mini-quiz (à l'oral, avec l'extrait ci-dessus)

1. Combien de colonnes y a-t-il dans la table ci-dessus ? *(6)*
2. Combien de lignes ? *(3)*
3. Quelle colonne est la clé primaire ? *(`id`)*
4. Quel type de données pour la colonne `age` ? *(`INTEGER`)*

---

## 3. Présentation de la base du club (10 min)



### La table `membres` (à afficher)

| id | prenom | nom | age | filiere | ville | date_inscription |
|---|---|---|---|---|---|---|
| 1 | Salma | Alaoui | 19 | Informatique | Rabat | 2026-09-15 |
| 2 | Yassine | Bennani | 21 | Réseaux | Salé | 2026-09-16 |
| 3 | Imane | Tazi | 18 | Informatique | Rabat | 2026-09-20 |
| 4 | Omar | Idrissi | 22 | Data | Temara | 2026-09-22 |
| 5 | Khadija | Fassi | 20 | Robotique | Rabat | 2026-10-01 |
| 6 | Hamza | Berrada | 18 | Informatique | Salé | 2026-10-03 |
| 7 | Sara | Chraibi | 19 | Data | Rabat | 2026-10-05 |
| 8 | Mehdi | Lahlou | 23 | Réseaux | Kénitra | 2026-10-10 |
| 9 | Nada | Amrani | 18 | Robotique | Temara | 2026-10-12 |
| 10 | Ayoub | Zniber | 20 | Informatique | Rabat | 2026-10-15 |

### Les requêtes de création (à afficher et à expliquer)

```sql
CREATE TABLE membres (
    id INTEGER PRIMARY KEY,
    prenom TEXT,
    nom TEXT,
    age INTEGER,
    filiere TEXT,
    ville TEXT,
    date_inscription TEXT
);

INSERT INTO membres VALUES (1, 'Salma',   'Alaoui',  19, 'Informatique', 'Rabat',  '2026-09-15');
INSERT INTO membres VALUES (2, 'Yassine', 'Bennani', 21, 'Réseaux',      'Salé',   '2026-09-16');
INSERT INTO membres VALUES (3, 'Imane',   'Tazi',    18, 'Informatique', 'Rabat',  '2026-09-20');
INSERT INTO membres VALUES (4, 'Omar',    'Idrissi', 22, 'Data',         'Temara', '2026-09-22');
INSERT INTO membres VALUES (5, 'Khadija', 'Fassi',   20, 'Robotique',    'Rabat',  '2026-10-01');
INSERT INTO membres VALUES (6, 'Hamza',   'Berrada', 18, 'Informatique', 'Salé',   '2026-10-03');
INSERT INTO membres VALUES (7, 'Sara',    'Chraibi', 19, 'Data',         'Rabat',  '2026-10-05');
INSERT INTO membres VALUES (8, 'Mehdi',   'Lahlou',  23, 'Réseaux',      'Kénitra','2026-10-10');
INSERT INTO membres VALUES (9, 'Nada',    'Amrani',  18, 'Robotique',    'Temara', '2026-10-12');
INSERT INTO membres VALUES (10,'Ayoub',   'Zniber',  20, 'Informatique', 'Rabat',  '2026-10-15');
```

### Comment lire ce script

- `CREATE TABLE` : **crée** la table avec ses colonnes et leurs types.
- `id INTEGER PRIMARY KEY` : la colonne `id` contient des nombres entiers et sert de **clé primaire**.
- `INSERT INTO ... VALUES` : **ajoute** une ligne dans la table ; les valeurs sont données dans l'ordre des colonnes.
- Chaque requête se termine par un point-virgule `;`.

> 🔗 Fais le lien visuel : montre qu'**un `INSERT` = une ligne** du tableau affiché.

---

## 4. Première requête : `SELECT` (20 min)

`SELECT` veut dire « sélectionner » : c'est la commande pour **lire** des données.

> 📌 Les tableaux « Résultat » ci-dessous sont à afficher après avoir expliqué chaque requête.

### 4.1 Tout afficher

```sql
SELECT * FROM membres;
```

- `SELECT` : « montre-moi »
- `*` : « toutes les colonnes »
- `FROM membres` : « dans la table membres »

👉 **Résultat :** la table complète de la partie 3 (10 lignes, 7 colonnes).

### 4.2 Choisir des colonnes précises

```sql
SELECT prenom, nom FROM membres;
```

Les colonnes sont séparées par une virgule.

👉 **Résultat :** (10 lignes)

| prenom | nom |
|---|---|
| Salma | Alaoui |
| Yassine | Bennani |
| Imane | Tazi |
| Omar | Idrissi |
| Khadija | Fassi |
| Hamza | Berrada |
| Sara | Chraibi |
| Mehdi | Lahlou |
| Nada | Amrani |
| Ayoub | Zniber |

### 4.3 Filtrer avec `WHERE`

`WHERE` veut dire « où » : il garde seulement les lignes qui respectent une condition.

```sql
SELECT prenom, ville FROM membres WHERE ville = 'Rabat';
```

👉 **Résultat :**

| prenom | ville |
|---|---|
| Salma | Rabat |
| Imane | Rabat |
| Khadija | Rabat |
| Sara | Rabat |
| Ayoub | Rabat |

Les opérateurs de comparaison :

| Symbole | Signification | Exemple |
|---|---|---|
| `=` | égal à | `age = 18` |
| `<>` | différent de | `ville <> 'Rabat'` |
| `>` | plus grand que | `age > 19` |
| `<` | plus petit que | `age < 20` |
| `>=` | plus grand ou égal | `age >= 20` |
| `<=` | plus petit ou égal | `age <= 20` |

### 4.4 Combiner des conditions : `AND` et `OR`

- `AND` (et) : les **deux** conditions doivent être vraies.
- `OR` (ou) : **au moins une** des conditions doit être vraie.

```sql
SELECT prenom, age FROM membres WHERE ville = 'Rabat' AND age >= 20;
```

👉 **Résultat :**

| prenom | age |
|---|---|
| Khadija | 20 |
| Ayoub | 20 |

```sql
SELECT prenom, filiere FROM membres WHERE filiere = 'Data' OR filiere = 'Robotique';
```

👉 **Résultat :**

| prenom | filiere |
|---|---|
| Omar | Data |
| Khadija | Robotique |
| Sara | Data |
| Nada | Robotique |

### 4.5 Trier avec `ORDER BY`

```sql
SELECT prenom, age FROM membres ORDER BY age;
```

Par défaut, le tri est **croissant** (du plus petit au plus grand). Ajoute `DESC` pour un tri **décroissant** :

```sql
SELECT prenom, age FROM membres ORDER BY age DESC;
```

👉 **Résultat du tri décroissant :**

| prenom | age |
|---|---|
| Mehdi | 23 |
| Omar | 22 |
| Yassine | 21 |
| Khadija | 20 |
| Ayoub | 20 |
| Salma | 19 |
| Sara | 19 |
| Imane | 18 |
| Hamza | 18 |
| Nada | 18 |

> 💡 Quand deux personnes ont le même âge, leur ordre entre elles n'est pas garanti.

### 4.6 Limiter le nombre de résultats avec `LIMIT`

```sql
SELECT prenom, age FROM membres ORDER BY age DESC LIMIT 3;
```

👉 **Résultat :** les 3 membres les plus âgés.

| prenom | age |
|---|---|
| Mehdi | 23 |
| Omar | 22 |
| Yassine | 21 |

### 📌 L'ordre d'écriture d'une requête

```sql
SELECT colonnes
FROM table
WHERE condition
ORDER BY colonne
LIMIT nombre;
```

*« Sélectionne ces colonnes, depuis cette table, où cette condition est vraie, trie, et limite. »*

> 🔔 **Spoiler :** l'ordre dans lequel on **écrit** une requête n'est **pas** l'ordre dans lequel SQL l'**exécute**. On le découvre dans la partie 9.

---

## 5. Exercices 1 : `SELECT` (15 min, sur papier)

Chaque participant écrit sa requête **sur papier**. Ensuite, la présentatrice affiche le corrigé et le résultat.

1. Affiche **toute** la table `membres`.
2. Affiche uniquement le `prenom` et la `filiere` de tous les membres.
3. Affiche les membres qui habitent à **Rabat**.
4. Affiche les membres qui ont **plus de 19 ans**.
5. Affiche les membres de la filière **Informatique**, triés par âge du plus âgé au plus jeune.
6. Affiche les **3 membres les plus âgés** (prénom et âge seulement).
7. **Bonus :** affiche les membres qui habitent à Rabat **et** qui sont en filière Informatique.

### ✅ Corrigé des exercices 1 (avec les résultats à afficher)

**1.**

```sql
SELECT * FROM membres;
```

👉 La table complète de la partie 3.

**2.**

```sql
SELECT prenom, filiere FROM membres;
```

👉 10 lignes : les colonnes `prenom` et `filiere` seulement.

**3.**

```sql
SELECT * FROM membres WHERE ville = 'Rabat';
```

| id | prenom | nom | age | filiere | ville |
|---|---|---|---|---|---|
| 1 | Salma | Alaoui | 19 | Informatique | Rabat |
| 3 | Imane | Tazi | 18 | Informatique | Rabat |
| 5 | Khadija | Fassi | 20 | Robotique | Rabat |
| 7 | Sara | Chraibi | 19 | Data | Rabat |
| 10 | Ayoub | Zniber | 20 | Informatique | Rabat |

*(la colonne `date_inscription` n'est pas affichée pour gagner de la place)*

**4.**

```sql
SELECT * FROM membres WHERE age > 19;
```

| id | prenom | nom | age | filiere | ville |
|---|---|---|---|---|---|
| 2 | Yassine | Bennani | 21 | Réseaux | Salé |
| 4 | Omar | Idrissi | 22 | Data | Temara |
| 5 | Khadija | Fassi | 20 | Robotique | Rabat |
| 8 | Mehdi | Lahlou | 23 | Réseaux | Kénitra |
| 10 | Ayoub | Zniber | 20 | Informatique | Rabat |

**5.**

```sql
SELECT * FROM membres WHERE filiere = 'Informatique' ORDER BY age DESC;
```

| id | prenom | nom | age | filiere | ville |
|---|---|---|---|---|---|
| 10 | Ayoub | Zniber | 20 | Informatique | Rabat |
| 1 | Salma | Alaoui | 19 | Informatique | Rabat |
| 3 | Imane | Tazi | 18 | Informatique | Rabat |
| 6 | Hamza | Berrada | 18 | Informatique | Salé |

**6.**

```sql
SELECT prenom, age FROM membres ORDER BY age DESC LIMIT 3;
```

| prenom | age |
|---|---|
| Mehdi | 23 |
| Omar | 22 |
| Yassine | 21 |

**7. (bonus)**

```sql
SELECT * FROM membres WHERE ville = 'Rabat' AND filiere = 'Informatique';
```

| id | prenom | nom | age | filiere | ville |
|---|---|---|---|---|---|
| 1 | Salma | Alaoui | 19 | Informatique | Rabat |
| 3 | Imane | Tazi | 18 | Informatique | Rabat |
| 10 | Ayoub | Zniber | 20 | Informatique | Rabat |

### ⚠️ Erreurs fréquentes des débutants

| Erreur | Pourquoi c'est faux | Correction |
|---|---|---|
| `WHERE ville = Rabat` | Le texte doit être entre apostrophes | `WHERE ville = 'Rabat'` |
| Oublier le `;` à la fin | Certains outils le demandent | Toujours terminer par `;` |
| `WHERE age = > 19` | Mauvais symbole | `WHERE age > 19` |
| `'rabat'` en minuscule | Le texte doit correspondre exactement | Écrire `'Rabat'` |

---

## 6. Modifier les données (15 min)

Jusqu'ici, on a seulement **lu** les données. Maintenant, on apprend à les **changer**.

### 6.1 Ajouter une ligne : `INSERT INTO`

```sql
INSERT INTO membres (id, prenom, nom, age, filiere, ville, date_inscription)
VALUES (11, 'Rania', 'Kettani', 19, 'Informatique', 'Rabat', '2026-11-20');
```

- On indique d'abord la **liste des colonnes**, puis les **valeurs** dans le même ordre.
- Le nouvel `id` doit être **unique** : ici, `11`.

👉 **Effet :** une 11ᵉ ligne apparaît à la fin du tableau.

Pour vérifier :

```sql
SELECT * FROM membres WHERE id = 11;
```

### 6.2 Modifier une ligne : `UPDATE`

```sql
UPDATE membres SET ville = 'Salé' WHERE id = 3;
```

- `UPDATE membres` : « change la table membres »
- `SET ville = 'Salé'` : « mets la ville à Salé »
- `WHERE id = 3` : « seulement pour la ligne dont l'id est 3 »

👉 **Effet :** Imane (id 3) habite maintenant à Salé, et personne d'autre n'est touché.

On peut aussi modifier plusieurs colonnes à la fois :

```sql
UPDATE membres SET age = 21, filiere = 'Data' WHERE id = 6;
```

### 6.3 Supprimer une ligne : `DELETE`

```sql
DELETE FROM membres WHERE id = 11;
```

👉 **Effet :** la ligne de Rania disparaît.

### 🚨 ATTENTION : toujours mettre un `WHERE` !

```sql
UPDATE membres SET ville = 'Rabat';
DELETE FROM membres;
```

Sans `WHERE`, la première change la ville de **tous** les membres, et la seconde **supprime tout** le contenu de la table.

> 🔒 **Règle d'or :** avant un `UPDATE` ou un `DELETE`, écris d'abord un `SELECT` avec le même `WHERE` pour voir quelles lignes seront touchées.

```sql
-- 1) Je vérifie d'abord
SELECT * FROM membres WHERE id = 11;
-- 2) Puis seulement après, je supprime
DELETE FROM membres WHERE id = 11;
```

### Résumé des 4 commandes

| Action | Commande | Question à se poser |
|---|---|---|
| Lire | `SELECT` | Quelles données je veux voir ? |
| Ajouter | `INSERT INTO` | Quelle nouvelle ligne j'ajoute ? |
| Modifier | `UPDATE` | Quelle ligne je change, et quoi ? |
| Supprimer | `DELETE` | Quelle ligne je supprime ? |

---

## 7. Exercices 2 : modifier les données (10 min, sur papier)

Chaque participant écrit les requêtes sur papier. La présentatrice affiche le corrigé et décrit l'**effet** sur le tableau.

1. **Ajoute** un nouveau membre : un volontaire de la salle (`id` = 11).
2. Écris le `SELECT` qui permet de **vérifier** que sa ligne est bien là.
3. **Modifie** l'âge (ou la ville) de ce volontaire avec `UPDATE`.
4. **Modifie** la ville de **Nada** (id 9) pour la mettre à `'Rabat'`.
5. **Supprime** la ligne du volontaire avec `DELETE`.
6. Écris le `SELECT` qui affiche **toute la table** pour vérifier le résultat final.
7. **Bonus :** change la filière de **tous** les membres de Salé pour `'Réseaux'`. *(N'oublie pas le `WHERE` !)*

### ✅ Corrigé des exercices 2

```sql
-- 1  (effet : une 11e ligne apparaît)
INSERT INTO membres (id, prenom, nom, age, filiere, ville, date_inscription)
VALUES (11, 'Prénom', 'Nom', 20, 'Informatique', 'Rabat', '2026-11-20');

-- 2
SELECT * FROM membres WHERE id = 11;

-- 3  (effet : seul le volontaire change)
UPDATE membres SET age = 21 WHERE id = 11;

-- 4  (effet : Nada passe de Temara à Rabat)
UPDATE membres SET ville = 'Rabat' WHERE id = 9;

-- 5  (effet : la ligne 11 disparaît)
DELETE FROM membres WHERE id = 11;

-- 6  (on retrouve 10 membres, avec Nada à Rabat)
SELECT * FROM membres;

-- 7 (bonus) (effet : Yassine et Hamza passent en Réseaux)
UPDATE membres SET filiere = 'Réseaux' WHERE ville = 'Salé';
```

> 🔄 **Important pour la suite :** pour la partie 8 et 9, on **repart de la table d'origine** (celle de la partie 3, avant les modifications des exercices 2). Dis-le clairement aux participants.

---

## 8. Calculs, regroupements et `HAVING` (30 min)

Jusqu'ici, chaque requête renvoyait des **lignes** de la table. Maintenant, on veut des **réponses calculées** : « Combien de membres ? Quel est l'âge moyen ? ».

### 8.1 Les fonctions de calcul (agrégation)

Une **fonction d'agrégation** prend plusieurs lignes et les **résume en une seule valeur**.

| Fonction | Rôle | Exemple |
|---|---|---|
| `COUNT(*)` | Compte les lignes | `COUNT(*)` |
| `SUM(col)` | Additionne | `SUM(age)` |
| `AVG(col)` | Fait la moyenne | `AVG(age)` |
| `MIN(col)` | Trouve la plus petite valeur | `MIN(age)` |
| `MAX(col)` | Trouve la plus grande valeur | `MAX(age)` |

```sql
SELECT COUNT(*) FROM membres;
```

👉 **Résultat :** `10` (10 membres au total).

```sql
SELECT AVG(age) FROM membres;
```

👉 **Résultat :** `19.8` (la somme des âges est 198, divisée par 10).

```sql
SELECT MIN(age), MAX(age) FROM membres;
```

👉 **Résultat :** `18` et `23`.

On peut les combiner avec `WHERE` :

```sql
SELECT AVG(age) FROM membres WHERE ville = 'Rabat';
```

👉 **Résultat :** `19.2` (les 5 membres de Rabat ont 19, 18, 20, 19 et 20 ans, soit 96 au total, divisé par 5).

### 8.2 Donner un nom au résultat : `AS`

Avec `AS`, on donne un **nom (alias)** à une colonne calculée :

```sql
SELECT COUNT(*) AS nb_membres, AVG(age) AS age_moyen FROM membres;
```

| nb_membres | age_moyen |
|---|---|
| 10 | 19.8 |

### 8.3 Regrouper avec `GROUP BY`

Problème : on ne veut pas **un seul** résultat pour toute la table, mais **un résultat par filière**.

`GROUP BY` veut dire « **regroupe** les lignes qui ont la même valeur dans cette colonne », puis la fonction de calcul est appliquée **dans chaque groupe**.

```sql
SELECT filiere, COUNT(*) AS nb_membres, AVG(age) AS age_moyen
FROM membres
GROUP BY filiere;
```

👉 **Résultat :**

| filiere | nb_membres | age_moyen |
|---|---|---|
| Informatique | 4 | 18.75 |
| Réseaux | 2 | 22 |
| Data | 2 | 20.5 |
| Robotique | 2 | 19 |

💡 **Image à donner :** imagine qu'on fait des **tas** avec les fiches des membres : un tas par filière. Ensuite, on compte chaque tas et on calcule sa moyenne.

> ⚠️ **Règle :** quand on utilise `GROUP BY`, les colonnes du `SELECT` doivent être soit **la colonne de regroupement** (ici `filiere`), soit **une fonction de calcul**. Si on écrit `SELECT prenom, COUNT(*) ... GROUP BY filiere`, SQL ne sait pas quel prénom afficher pour un tas de 4 personnes. Beaucoup d'outils donnent alors une erreur.

### 8.4 Filtrer les groupes avec `HAVING`

`WHERE` filtre les **lignes** (les personnes). Mais comment filtrer les **groupes** (les tas) ? Avec `HAVING`.

```sql
SELECT filiere, COUNT(*) AS nb_membres
FROM membres
GROUP BY filiere
HAVING COUNT(*) >= 3;
```

👉 **Résultat :** il ne reste que la filière qui a au moins 3 membres.

| filiere | nb_membres |
|---|---|
| Informatique | 4 |

### 8.5 `WHERE` ou `HAVING` ?

| | `WHERE` | `HAVING` |
|---|---|---|
| Filtre | les **lignes** (les personnes) | les **groupes** (les tas) |
| Moment | **avant** le `GROUP BY` | **après** le `GROUP BY` |
| Peut utiliser `COUNT`, `AVG`... | ❌ Non | ✅ Oui |
| Exemple | `WHERE age > 18` | `HAVING COUNT(*) >= 2` |

> ❌ **Erreur classique :** `WHERE COUNT(*) >= 2`. Au moment du `WHERE`, les groupes n'existent pas encore, donc on ne peut pas les compter. Il faut utiliser `HAVING`.

---

## 9. Exercice final : dans quel ordre SQL exécute une requête ? (20 min)

C'est l'exercice qui rassemble **tout** : `WHERE`, `GROUP BY`, `HAVING`, fonctions de calcul, `ORDER BY`.

### La question

> « Parmi les membres de **plus de 18 ans**, pour chaque filière, affiche le **nombre de membres** et l'**âge moyen**, mais **seulement** les filières qui ont **au moins 2 membres**, du plus grand âge moyen au plus petit. »

### La requête

```sql
SELECT filiere, COUNT(*) AS nb_membres, AVG(age) AS age_moyen
FROM membres
WHERE age > 18
GROUP BY filiere
HAVING COUNT(*) >= 2
ORDER BY age_moyen DESC;
```

### 🔑 L'idée centrale : écrire n'est pas exécuter

On **écrit** `SELECT` en premier. Mais SQL ne **commence pas** par le `SELECT` !

| Ordre d'écriture | Ordre d'exécution | Ce que fait SQL |
|---|---|---|
| `SELECT` | **5ᵉ** | Calcule les colonnes et les fonctions |
| `FROM` | **1ᵉʳ** | Va chercher la table |
| `WHERE` | **2ᵉ** | Enlève les lignes qui ne respectent pas la condition |
| `GROUP BY` | **3ᵉ** | Fait les tas |
| `HAVING` | **4ᵉ** | Enlève les tas qui ne respectent pas la condition |
| `ORDER BY` | **6ᵉ** | Trie le résultat |
| `LIMIT` | **7ᵉ** (dernier) | Garde seulement les premières lignes |

🧠 **À retenir :** **FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT**

*Astuce mémo : « **F**ort **W**eekend, **G**rande **H**istoire, **S**ortie **O**rganisée, **L**ibre. »*

### Étape par étape avec la table d'origine

**Étape 1 : `FROM membres`** (premier)
SQL prend toute la table : 10 lignes.

**Étape 2 : `WHERE age > 18`** (deuxième)
SQL enlève les membres qui ont 18 ans (Imane, Hamza, Nada). Il reste **7 lignes** :

| id | prenom | age | filiere |
|---|---|---|---|
| 1 | Salma | 19 | Informatique |
| 2 | Yassine | 21 | Réseaux |
| 4 | Omar | 22 | Data |
| 5 | Khadija | 20 | Robotique |
| 7 | Sara | 19 | Data |
| 8 | Mehdi | 23 | Réseaux |
| 10 | Ayoub | 20 | Informatique |

**Étape 3 : `GROUP BY filiere`** (troisième)
SQL fait **4 tas**, un par filière :

| Tas | Membres dans le tas |
|---|---|
| Informatique | Salma (19), Ayoub (20) |
| Réseaux | Yassine (21), Mehdi (23) |
| Data | Omar (22), Sara (19) |
| Robotique | Khadija (20) |

**Étape 4 : `HAVING COUNT(*) >= 2`** (quatrième)
SQL compte chaque tas et enlève ceux qui ont moins de 2 membres. Le tas **Robotique** n'a qu'une personne : il est supprimé. Il reste **3 tas**.

**Étape 5 : `SELECT filiere, COUNT(*), AVG(age)`** (cinquième)
Seulement maintenant, SQL calcule les colonnes à afficher, tas par tas :

| filiere | nb_membres | age_moyen |
|---|---|---|
| Informatique | 2 | 19.5 |
| Réseaux | 2 | 22 |
| Data | 2 | 20.5 |

**Étape 6 : `ORDER BY age_moyen DESC`** (sixième)
SQL trie du plus grand âge moyen au plus petit :

| filiere | nb_membres | age_moyen |
|---|---|---|
| Réseaux | 2 | 22 |
| Data | 2 | 20.5 |
| Informatique | 2 | 19.5 |

**Étape 7 : `LIMIT`** (dernier)
Il n'y a pas de `LIMIT` dans cette requête, donc rien ne change. S'il y avait eu `LIMIT 2`, on aurait gardé seulement Réseaux et Data.

### ❓ Questions de réflexion (à poser à la salle)

**1. Pourquoi peut-on écrire `ORDER BY age_moyen` mais pas `WHERE age_moyen > 20` ?**

> Parce que l'alias `age_moyen` est créé à l'étape 5 (`SELECT`). Le `ORDER BY` (étape 6) vient **après**, donc il le connaît. Le `WHERE` (étape 2) vient **avant**, donc le nom `age_moyen` n'existe pas encore.

**2. Pourquoi `HAVING` peut-il utiliser `COUNT(*)` alors que `WHERE` ne le peut pas ?**

> Parce que `HAVING` s'exécute **après** le `GROUP BY` : les tas existent, on peut donc les compter. Le `WHERE` s'exécute **avant**, quand il n'y a encore que des lignes individuelles.

**3. Que se passe-t-il si on met la condition `age > 18` dans `HAVING` au lieu de `WHERE` ?**

> Ce serait faux : après le regroupement, on ne regarde plus les âges individuels. Pour filtrer des **personnes**, on utilise `WHERE`. Pour filtrer des **groupes**, on utilise `HAVING`.

### ✍️ Exercices d'entraînement (sur papier)

**A.** Affiche le **nombre de membres par ville**, de la ville la plus peuplée à la moins peuplée (en cas d'égalité, par ordre alphabétique de ville).

**B.** Pour chaque ville qui a **au moins 2 membres**, affiche l'âge **minimum** et l'âge **maximum**, triés par ville.

**C. Remets dans l'ordre d'exécution** ces clauses : `ORDER BY`, `HAVING`, `FROM`, `SELECT`, `GROUP BY`, `WHERE`.

### ✅ Corrigé des exercices d'entraînement

**A.**

```sql
SELECT ville, COUNT(*) AS nb_membres
FROM membres
GROUP BY ville
ORDER BY nb_membres DESC, ville;
```

| ville | nb_membres |
|---|---|
| Rabat | 5 |
| Salé | 2 |
| Temara | 2 |
| Kénitra | 1 |

**B.**

```sql
SELECT ville, MIN(age) AS age_min, MAX(age) AS age_max
FROM membres
GROUP BY ville
HAVING COUNT(*) >= 2
ORDER BY ville;
```

| ville | age_min | age_max |
|---|---|---|
| Rabat | 18 | 20 |
| Salé | 18 | 21 |
| Temara | 18 | 22 |

*(Kénitra a un seul membre, donc `HAVING` l'enlève.)*

**C.** `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY`

---

## 10. Conclusion (10 min)

### 🧠 Les points à retenir

1. Une **base de données** range des informations dans des **tables** (lignes et colonnes).
2. **SQL** est le langage pour parler à une base de données.
3. `SELECT ... FROM ... WHERE ... ORDER BY ... LIMIT` sert à **lire**, **filtrer** et **trier**.
4. `INSERT`, `UPDATE` et `DELETE` servent à **ajouter**, **modifier** et **supprimer**. Avec `UPDATE` et `DELETE`, **toujours un `WHERE`**.
5. `COUNT`, `SUM`, `AVG`, `MIN`, `MAX` **résument** plusieurs lignes en une valeur ; `GROUP BY` les calcule **par groupe**.
6. `WHERE` filtre les **lignes**, `HAVING` filtre les **groupes**.
7. SQL exécute dans cet ordre : **FROM → WHERE → GROUP BY → HAVING → SELECT → ORDER BY → LIMIT**.

### 🏠 Mini-défi à faire à la maison

Crée une **nouvelle table** `livres` avec ces colonnes : `id`, `titre`, `auteur`, `annee`. Puis :

1. Ajoute 5 livres avec `INSERT`.
2. Affiche les livres publiés après l'an 2000.
3. Trie les livres par année, du plus récent au plus ancien.
4. Modifie le titre d'un livre.
5. Supprime un livre.
6. **Défi bonus :** affiche, pour chaque auteur, le nombre de livres écrits.

*Indice pour créer la table :*

```sql
CREATE TABLE livres (
    id INTEGER PRIMARY KEY,
    titre TEXT,
    auteur TEXT,
    annee INTEGER
);
```

### 🔜 Prochaine séance

- Recherche de texte avec `LIKE`
- Créer plusieurs tables et les relier (clé étrangère)
- Les **jointures** (`JOIN`) entre plusieurs tables
- Un petit projet complet

---

## 📝 Aide-mémoire (à garder)

```sql
-- Lire
SELECT colonne1, colonne2 FROM table WHERE condition ORDER BY colonne DESC LIMIT 5;

-- Ajouter
INSERT INTO table (col1, col2) VALUES ('texte', 10);

-- Modifier
UPDATE table SET col1 = 'nouvelle valeur' WHERE id = 1;

-- Supprimer
DELETE FROM table WHERE id = 1;

-- Calculer par groupe
SELECT col, COUNT(*) AS nb, AVG(age) AS moyenne
FROM table
WHERE condition_sur_les_lignes
GROUP BY col
HAVING condition_sur_les_groupes
ORDER BY moyenne DESC;
```

**Ordre d'exécution :** `FROM` → `WHERE` → `GROUP BY` → `HAVING` → `SELECT` → `ORDER BY` → `LIMIT`

---

## 🎤 01_Club Oumayma Bouchnaf

