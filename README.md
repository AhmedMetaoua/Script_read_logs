# Script de Suivi BTJ

## Description

Ce script Python automatise l'extraction et le suivi des données de traitement BTJ (Batch de Traitement des Journaux). Il analyse les fichiers de relevé texte, extrait les informations importantes et les sauvegarde dans un fichier Excel ainsi que dans une base de données MySQL.

## Fonctionnalités

- **Extraction automatique** des données depuis les fichiers de relevé texte
- **Sauvegarde Excel** dans un fichier de suivi annuel
- **Stockage en base de données** MySQL avec création automatique des tables
- **Validation des données** avec gestion d'erreurs
- **Interface en ligne de commande** simple d'utilisation

## Données extraites

Le script extrait les informations suivantes :
- Date de traitement
- Heure d'exécution
- Compteurs relevés
- Compteurs non relevés
- Compteurs NI = AI
- Abonnés facturés
- Abonnés non facturés
- Factures ordinaires
- Factures simples
- Factures ADM
- Somme des restitutions + ADM

## Prérequis

### Dépendances Python
```bash
pip install openpyxl pymysql
```

### Base de données MySQL
- Serveur MySQL accessible
- Base de données nommée `scheduler_test`
- Utilisateur avec droits de création/insertion

## Configuration

### Configuration de la base de données
Modifiez les paramètres dans le script selon votre environnement :

```python
DB_CONFIG = {
    "host": "localhost",
    "user": "root",
    "password": "azerty",
    "database": "scheduler_test"
}
```

### Fichier Excel
Le script utilise par défaut le fichier `Suivi Btj 2025.xlsx`. Il sera créé automatiquement s'il n'existe pas.

## Utilisation

### Syntaxe
```bash
python script.py <chemin/vers/fichier_releve.txt>
```

### Exemple
```bash
python script.py releve_20250712.txt
```

### Format du fichier d'entrée
Le fichier texte doit contenir :
- Une ligne avec la date au format `to_date('DD/MM/YYYY')`
- Une ligne avec l'heure au format `Production on ... HH:MM:SS`
- Les données de compteurs et factures avec leurs libellés respectifs

## Structure de la base de données

### Table `Suivi_Btj`
| Colonne | Type | Description |
|---------|------|-------------|
| `id` | INT (AUTO_INCREMENT) | Clé primaire |
| `date_traitement` | DATE | Date de traitement |
| `heure_execution` | TIME | Heure d'exécution |
| `cptrs_releves` | INT | Compteurs relevés |
| `cptrs_non_releves` | INT | Compteurs non relevés |
| `cptrs_ni_ai` | INT | Compteurs NI = AI |
| `abonnes_factures` | INT | Abonnés facturés |
| `abonnes_non_factures` | INT | Abonnés non facturés |
| `factures_ordinaire` | INT | Factures ordinaires |
| `factures_simple` | INT | Factures simples |
| `factures_adm` | INT | Factures ADM |
| `somme_restitutions_adm` | INT | Somme restitutions + ADM |

## Gestion des erreurs

Le script gère les erreurs suivantes :
- Fichier de relevé introuvable
- Erreurs de connexion à la base de données
- Données manquantes ou mal formatées

## Messages de sortie

- ✅ **Succès** : Données extraites et sauvegardées
- ❌ **Erreur** : Fichier introuvable ou erreur de base de données

## Exemples d'utilisation

### Traitement d'un fichier quotidien
```bash
python script.py releve_quotidien_20250712.txt
```

### Traitement en lot (script bash)
```bash
#!/bin/bash
for fichier in releve_*.txt; do
    python script.py "$fichier"
done
```

## Maintenance

### Sauvegarde des données
- Les données Excel sont sauvegardées dans le fichier `Suivi Btj 2025.xlsx`
- Les données MySQL sont stockées dans la table `Suivi_Btj`

### Archivage annuel
Il est recommandé de :
- Créer un nouveau fichier Excel chaque année
- Archiver les anciennes données
- Effectuer des sauvegardes régulières de la base de données

## Dépannage

### Problèmes courants

**Erreur de connexion MySQL**
- Vérifiez que le serveur MySQL est démarré
- Contrôlez les paramètres de connexion
- Vérifiez les droits d'accès de l'utilisateur

**Fichier Excel verrouillé**
- Fermez le fichier Excel s'il est ouvert
- Vérifiez les permissions d'écriture

**Données manquantes**
- Vérifiez le format du fichier de relevé
- Contrôlez que tous les libellés attendus sont présents

## Licence

Ce script est fourni tel quel pour usage interne. Adaptez les paramètres selon vos besoins spécifiques.

## Support

Pour toute question ou problème, contactez l'équipe de développement avec :
- Le message d'erreur complet
- Un exemple de fichier de relevé
- La configuration de votre environnement