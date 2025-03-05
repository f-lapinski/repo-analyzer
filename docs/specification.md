# Data Analysis from Git Platforms

**Collecting and presenting statistics** on:
- **Pull requests**
- **Comments**
- **Commits**
- **Code reviews**
- **Users and their groups**

*GitHub's REST API considers every pull request an issue, but not every issue is a pull request. For this reason, "Issues" endpoints may return both issues and pull requests in the response. You can identify pull requests by the `pull_request` key. Be aware that the `id` of a pull request returned from "Issues" endpoints will be an issue id. To find out the pull request id, use the "[List pull requests](https://docs.github.com/rest/pulls/pulls#list-pull-requests)" endpoint.*

## GitHub

API: [https://docs.github.com/en/rest?apiVersion=2022-11-28](https://docs.github.com/en/rest?apiVersion=2022-11-28)

### Scanning for Changes

- We can scan it manually by requesting endpoints, or we can use webhooks for realtime information.

### Response Media Types from API

Mostly used are:

- `application/vnd.github+json`

- `application/json`

Some endpoints support special formats, such as:

- `diff`, `patch`, `sha` – for commits and pull requests

- `full`, `raw`, `text`, `html` – for other resources

### Basic Endpoints

- **List PRs**: 
`GET /repos/{owner}/{repo}/pulls`
- **Pull Request details**: `GET /repos/{owner}/{repo}/pulls/{pull_number}`
- **PR comments**: `GET /repos/{owner}/{repo}/pulls/comments`
- **Commit comments**: `GET /repos/{owner}/{repo}/commits/{commit_sha}/comments`
- **List of commits**: `GET /repos/{owner}/{repo}/commits`
- **Commit details**: `GET /repos/{owner}/{repo}/commits/{commit_sha}`
- **List of PR reviews**: `GET /repos/{owner}/{repo}/pulls/{pull_number}/reviews`
- **Review comments for PR**: `GET /repos/{owner}/{repo}/pulls/{pull_number}/reviews/{review_id}/comments`
- **User information**: `GET /users/{username}`
- **List of user's organizations**: `GET /users/{username}/orgs`
- **Members of an organization**: `GET /orgs/{org}/members`
- **List of teams in an organization**: `GET /orgs/{org}/teams`

### Authentication Methods

- For authentication, we can use a couple of methods:
  - Personal Access Token (PAT)
  - OAuth
  - GitHup App
  - Webhooks