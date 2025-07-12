# 📊 Script d'Extraction et d'Insertion des Données de Relevé

Ce script lit un fichier texte contenant des statistiques de relevés (format `.txt`), extrait automatiquement les données clés, et les insère à la fois dans un fichier Excel (`Suivi Btj 2025.xlsx`) et dans une base de données MySQL.

---

## ⚙️ Fonctionnalités

- 📅 Extraction automatique de la **date de traitement** et de l'**heure d'exécution**
- 🔍 Recherche via expressions régulières des données statistiques importantes (compteurs, abonnés, factures…)
- 📥 Ajout ou création automatique d’un fichier **Excel**
- 🛢️ Insertion des données dans une **base de données MySQL** (`scheduler_test`)
- ✅ Création de la table `Suivi_Btj` si elle n’existe pas

---

## 📦 Prérequis

- Python 3.x
- Bibliothèques :
  - `openpyxl`
  - `pymysql`
- Une base de données MySQL locale accessible avec :
  - **host**: `localhost`
  - **user**: `root`
  - **password**: `azerty`
  - **database**: `scheduler_test`

---

## 📁 Structure attendue du fichier texte

Le fichier `.txt` doit contenir des lignes semblables à :

Production on Monday March 24 12:45:30 2025


Cptrs a Releves - - - - - - - 1834

...

to_date('24/03/2025')

...

Les lignes contenant les informations suivantes seront analysées :

- Cptrs a Releves
- Cptrs Non Releves
- Cptrs NI egale AI
- Abonnes Factures
- Abon. Non Factures
- Nbre Factures Fichier Ordinaire
- Nbre Factures Fichier Simple
- Factures ADM de la mensuel de prelevement
- Somme Restitutions et Adm

---

## 🚀 Exécution

Dans un terminal :

```bash
python script.py chemin/vers/fichier_releve.txt
```

⚠️ Le fichier texte doit être fourni en argument.

## 🗃️ Données insérées

Chaque ligne correspond à une exécution, avec les colonnes suivantes :

- Date
- Heure
- Cptrs Releves
- Cptrs Non Releves
- Cptrs NI = AI
- Abonnes Factures
- Abonnes Non Factures
- Factures Ordinaire
- Factures Simple
- Factures ADM
- Somme Restitutions + ADM

## 🛠️ À adapter

Modifier les identifiants de connexion `MySQL` dans `DB_CONFIG` si nécessaire.

Vérifier que le fichier `.txt` respecte bien la structure attendue (sinon certaines valeurs pourraient être manquantes).

## 📤 Sorties
Un fichier Excel : `Suivi Btj 2025.xlsx` (créé ou mis à jour)

Une ligne insérée dans la base de données `scheduler_test` dans la table `Suivi_Btj`