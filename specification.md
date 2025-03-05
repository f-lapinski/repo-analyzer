# Analiza danych z platform Gitowych, takich jak **GitHub** i **Azure DevOps**…

**Zbieranie i prezentacja statystyk** dotyczących m.in.:
- **Pull requestów**
- **Komentarzy**
- **Commitów**
- **Code review**
- **Użytkowników i ich grup**

*GitHub's REST API considers every pull request an issue, but not every issue is a pull request. For this reason, "Issues" endpoints may return both issues and pull requests in the response. You can identify pull requests by the `pull_request` key. Be aware that the `id` of a pull request returned from "Issues" endpoints will be an issue id. To find out the pull request id, use the "[List pull requests](https://docs.github.com/rest/pulls/pulls#list-pull-requests)" endpoint.*

## GitHub

API: [https://docs.github.com/en/rest?apiVersion=2022-11-28](https://docs.github.com/en/rest?apiVersion=2022-11-28)

### Skanowanie w poszukiwaniu zmian

Do skanowania zmian w repozytorium GitHub możesz użyć:

1️⃣ **REST API**

- `GET /repos/{owner}/{repo}/commits` → Pobiera listę commitów
- `GET /repos/{owner}/{repo}/pulls` → Sprawdza nowe pull requesty
- `GET /repos/{owner}/{repo}/compare/{base}...{head}` → Porównuje dwa commity i pokazuje zmienione pliki

2️⃣ **GitHub Webhooks**

- Powiadomienia o zmianach w repo (np. `push`, `pull_request`, `issues`) wysyłane na Twój serwer

📌 **REST API** nadaje się do okresowego skanowania, a **Webhooki** do reakcji w czasie rzeczywistym. 🚀

### Typy zwracanych danych z API

Media types określają format danych zwracanych przez API GitHuba.

Dodaje się je w **nagłówku `Accept`** podczas wysyłania zapytań.

Najczęściej używane:

✅ `application/vnd.github+json`

✅ `application/json`

Niektóre endpointy obsługują specjalne formaty, np.:

🔹 `diff`, `patch`, `sha` – dla commitów i pull requestów

🔹 `full`, `raw`, `text`, `html` – dla innych zasobów

Format niestandardowych media types wygląda tak:

`application/vnd.github.PARAM+json` (np. `application/vnd.github.raw+json`).

### Podstawowe Endpointy

#### **Pull Requesty**
- **Lista PR**:`GET /repos/{owner}/{repo}/pulls`
- **Szczegóły PR**:`GET /repos/{owner}/{repo}/pulls/{pull_number}`

#### **Komentarze**
- **Komentarze PR**:`GET /repos/{owner}/{repo}/pulls/comments`
- **Komentarze do commitów**:`GET /repos/{owner}/{repo}/commits/{commit_sha}/comments`

#### **Commity**
- **Lista commitów**:`GET /repos/{owner}/{repo}/commits`
- **Szczegóły commita**:`GET /repos/{owner}/{repo}/commits/{commit_sha}`

#### **Code Review**
- **Lista recenzji PR**:`GET /repos/{owner}/{repo}/pulls/{pull_number}/reviews`
- **Komentarze do recenzji PR**:`GET /repos/{owner}/{repo}/pulls/{pull_number}/reviews/{review_id}/comments`

#### **Użytkownicy i Grupy**
- **Informacje o użytkowniku**:`GET /users/{username}`
- **Lista organizacji użytkownika**:`GET /users/{username}/orgs`
- **Członkowie organizacji**:`GET /orgs/{org}/members`
- **Lista zespołów w organizacji**:`GET /orgs/{org}/teams`

### Sposoby Authentication

#### **1️⃣ Personal Access Token (PAT)**
- Najprostsza metoda. Tworzysz token w ustawieniach GitHub i używasz go w nagłówku.

#### **2️⃣ OAuth**
- Używane, gdy użytkownicy logują się, aby autoryzować aplikację do dostępu do ich repozytoriów.

#### **3️⃣ GitHub App (JWT + Installation Token)**
- Bezpieczne dla aplikacji działających na wielu repozytoriach, z uprawnieniami nadanymi przez właściciela organizacji.

#### **4️⃣ Webhooks**
- GitHub wysyła powiadomienia o zmianach do Twojego serwera (np. o nowych commitach, PR-ach).
