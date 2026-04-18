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

## Cloud Tasks → Notification Discord

À chaque création de carte, le backend enqueue une **GCP Cloud Task** qui déclenche une **Cloud Function**. Celle-ci envoie un message embed dans un channel Discord via webhook.

**Flux :** `POST /cards` → `CardService` → `CloudTaskPort` → Cloud Tasks queue → Cloud Function → Discord webhook

### Variables d'environnement supplémentaires (prod)

| Variable | Description |
|----------|-------------|
| `CLOUD_TASKS_PROJECT_ID` | ID du projet GCP |
| `CLOUD_TASKS_LOCATION` | Région GCP (ex: `europe-west1`) |
| `CLOUD_TASKS_QUEUE` | Nom de la queue (ex: `card-notifications`) |
| `CLOUD_FUNCTION_URL` | URL HTTPS de la Cloud Function déployée |

### Déploiement de la Cloud Function

```bash
cd cloud-functions/discord-notifier
gcloud functions deploy discordNotifier \
  --gen2 --runtime=nodejs20 --trigger-http --allow-unauthenticated \
  --region=europe-west1 \
  --set-env-vars DISCORD_WEBHOOK_URL=<url-du-webhook-discord>
```