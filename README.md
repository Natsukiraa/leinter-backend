# Clean Code

## Membres de l'équipe
- GAZIO Maladie (Maël) 🦠
- PHE Lina 🐱
- TECHER Mathis 🤖

## Déploiement du projet 

### Prérequis
- Java 17 

### Variables d'environnement
| Nom de la variable | Description |
|--------------------|-------------|
| `DB_URL`           | URL de la base de données (ex: `jdbc:mysql://localhost:3306/clean_code_db`) |
| `DB_USERNAME`      | Nom d'utilisateur de la base de données |
| `DB_PASSWORD`      | Mot de passe de la base de données |

### Déploiement 

Les déploiments sont réalisés automatiquement via Cloud build et Cloud Run a chaque push sur main.
Grâce a un déclencheur, et au fichier `cloudbuild.yaml` présent à la racine du projet, le projet est automatiquement construit et déployé sur Cloud Run.