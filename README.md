
# GitLab to GitHub migration

### The `.env` file in th repo has been configured for Prop Data's needs already

Migrate repositories, wikis, issues and milestones from GitLab to GitHub.

## Install

1. Set environment variables in `.env`
  * `GITLAB_URL` - The URL of your local GitLab instance e.g. `http://GitLab.local`
  * `GITLAB_GIT_URL` - The Git URL of your local GitLab instance e.g. `git@GitLab.local`
  * `GITLAB_TOKEN` - Your [GitLab API token](https://docs.gitlab.com/ce/user/profile/personal_access_tokens.html)
  * `GITHUB_ORG` - Your GitHub organization name e.g. `StratoTechnology`
  * `GITHUB_TEAM_ID` - The id of the GitHub team that will be granted access to this repository
  * `GITHUB_USERNAME` - Your GitHub username e.g. `WesleyCharlesBlake`
  * `GITHUB_TOKEN` - Your [GitHub API token](https://github.com/settings/tokens)

3. Install dependencies with `npm install` and `npm install -g coffee-script`

4. List available tasks with `cake`
```
Cakefile defines the following tasks:

cake migrate:repo         # migrate repository
cake migrate:wiki         # migrate wiki
cake migrate:issues       # migrate issues
cake migrate:milestones   # migrate milestones

  -i, --gitlab_id    GitLab project id
  -l, --gitlab_name  GitLab repo name
  -h, --github_name  GitHub repo name
```
## Examples
```
cake -l <gitlab-namespace>/<repo-name> -h <github-repo-name> migrate:repo
cake -l <gitlab-namespace>/<repo-name> -h <github-repo-name> migrate:wiki
cake -l <gitlab-namespace>/<repo-name> -h <github-repo-name> migrate:issues
cake -l <gitlab-namespace>/<repo-name> -h <github-repo-name> migrate:milestones

# real example:
cake -l propdata-custom/ReedStoneEstate -h reedstone.co.za migrate:repo

```

## Notes

* `gitlab_id` can be found by inspecting the `body` tag of the GitLab project page (e.g. `data-project-id="84"`), or via the GitLab API.

* `GITHUB_TEAM_ID` can be found via `api.github.com/teams` (requires org owner rights).

* `migrate:wiki` requires that the GitHub wiki must be created first (it's enough to create a single blank page).

* This app will create the repo on Github, so please ensure you adhere to our repo naming conventions (which is to use the projects primary url: eg mydomain.co.za)
