# org-health

## Health Files
**Explore what these health files are and create a list of recommended documentation files essential for every GitHub repository and specify what content each of this document should include.**
- Community health files are a set of files that provide guidance and templates for maintaining a healthy and collaborative open source project. They define and standardize aspects of project development and community interaction. 
- GitHub allows people to create default community health files by adding them to a public .github repo of the organization. Then for any repository owned by a user of that organization, it will look for the community health files in the following order: the `.github` folder, the root, and then the `docs` folder. If a health file can not be found, it will use the default from the special repository.
- For example, if a project does not have the `CONTRIBUTING.md` file, when users create an issue/PR, they will see a link to the default `CONTRIBUTING.md` of the `.github` repo. However, if the repo does have the `.github/ISSUE_TEMPLATE` folder, the defaults will not be used. This allows repo maintainers to override the defaults. 
- Moreover, storing files in `.github` allows changes to the defaults in one place. 
- Note: issue templates and their configuration file must be in a folder called .github/ISSUE_TEMPLATE. All other supported files may be in the root of the repository, the .github folder, or the docs folder.

**The most general community health files are below:**
- Issue and pull request templates and config.yml: Issue and pull request templates customize and standardize the information you'd like contributors to include when they open issues and pull requests in your repository. If an issue template sets a label, that label must be created in your .github repository and any repositories where the template will be used.
- `CODE_OF_CONDUCT.md`: A CODE_OF_CONDUCT file defines standards for how to engage in a community.
- `CONTRIBUTING.md`: A CONTRIBUTING file communicates how people should contribute to your project.
- `GOVERNANCE.md`: A GOVERNANCE file lets people know about how your proj`ect is governed. For example, it might discuss project roles and how decisions are made.
- `SECURITY.md`: A SECURITY file gives instructions on how to report a security vulnerability in your project and description that hyperlinks the file. 
- `SUPPORT.md`: A SUPPORT file lets people know about ways to get help with your project
- `FUNDING.md`: A FUNDING file displays a sponsor button in your repository to increase the visibility of funding options for your open source project.

**Demo: Create a demo respoitory with these files and present it to us.**
- The current .github repository contains all the health files presented above
- Since it is in the .github repository of an organization, all the repositories in the organization inherit it. 

**Enforcement of health files**
Enforcement: You need to enforce that every new repository in the whole organization (not just yours) contain these documents and if they do not, they should be disabled. Using GitHub Actions workflow, could you implement a GitHub Action that that does it across the whole GitHub organization?
- The workflow in `org-health` specifies a few health files that a repository must have, not just inherited but their own custom ones.
- If they are found to not have the health file, they are moved to public archive. 

**Communication Strategy**
Users in the company currently do not know about these requirements. How could you communicate the above to the users and what should that communication include?
- Explanation to what health files are and why they are important in every repository
- Default templates for each type of health file, so they can be added easily to each repository. 
- Example repositories that have added the health files correctly so that they can compare. 


## Enforcement of Health Files
A workflow is used to iterate over all repositories in the organisation and check whether they have added specific custom health files. The workflow needs admin-level permissions in order to archive other repositoresi within the organization. This is done by adding a secret to the repository so that it has the permissions to make admin-level changes in the organization, otherwise it would not be able to archive other repositories in the organization. Only users (who are admins) can perform these actions, thus we use a personal access token (of the admin) in the repository to give the scripts used the ability to modify other repositories of the organization. 

On the admin account:
1. GitHub Account > Settings > Developer settings > Personal access tokens
2. Generate a classic token
3. Give it repo and admin:org scopes

For the enforcer repository:
1. Settings > Secrets and variables > Actions
2. Create New repository secret
3. Name it `GH_TOKEN` and add the personal access token as the secret
4. Now when `GH_TOKEN` is mentioned in the workflow, it is referring to the secret added to this repository
