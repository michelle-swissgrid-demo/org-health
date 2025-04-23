# org-health

## Steps taken

This is done by adding a secret to the repository so that it has the permissions to make admin-level changes in the organization, otherwise it would not be able to archive other repositories in the organization. Only users (who are admins) can perform these actions, thus we use a personal access token (of the admin) in the repository to give the scripts used the ability to modify other repositories of the organization. 

On the admin account:
1. GitHub Account > Settings > Developer settings > Personal access tokens
2. Generate a classic token
3. Give it repo and admin:org scopes

For the enforcer repository:
1. Settings > Secrets and variables > Actions
2. Create New repository secret
3. Name it `GH_TOKEN` and add the personal access token as the secret