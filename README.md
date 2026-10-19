# gateway

**Point d'entrée unique** de l'application glop (Spring Cloud Gateway).
Le navigateur ne parle qu'à la gateway, qui redirige chaque requête vers le bon service selon l'URL.

| Chemin | Redirigé vers |
|---|---|
| `/api/users/**` | users |
| `/api/fidelity/**` | fidelity |
| `/api/statistiques/**` | statistiques |
| `/api/commande/**` | commande |
| `/api/catalogue/**` | catalogue |
| `/**` (tout le reste) | front |

Les routes sont définies dans `src/main/resources/application.yaml`.

## Lancer en local

```bash
./mvnw spring-boot:run      # → http://localhost:8080
```

Par défaut, la gateway redirige vers les services sur `localhost:8081` à `8085` et le front sur `localhost:3000`
(lancés depuis IntelliJ ou depuis glop-infra).

Exemple : http://localhost:8080/api/users/hello → http://localhost:8081/api/users/hello

## Dans Docker (glop-infra / serveur)

Les adresses sont remplacées par des variables d'environnement :

| Variable | Valeur dans Docker |
|---|---|
| `USERS_URL` | `http://users-api:8080` |
| `FIDELITY_URL` | `http://fidelity-api:8080` |
| `STATISTIQUES_URL` | `http://statistiques-api:8080` |
| `COMMANDE_URL` | `http://commande-api:8080` |
| `CATALOGUE_URL` | `http://catalogue-api:8080` |
| `FRONT_URL` | `http://front:3000` |
| `CORS_ALLOWED_ORIGINS` | origines autorisées pour `/api/**` (dev) |


