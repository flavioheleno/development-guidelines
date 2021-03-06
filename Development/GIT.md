# GIT
Every project has a main GIT repository, either on [Bitbucket](http://bitbucket.org) or on [GitHub](http://github.com), that is called `upstream` and **every** deploy is made from upstream's _master_ branch.

With that in mind is important that the master branch from upstream repositories are kept clean and stable, to achieve that, **all** work done in a project should be done on a **fork** from the upstream repository and __NEVER__ straight into the upstream repository.

# Example

Add a new article (`NewArticle.md`) to the [Development Guideline](https://bitbucket.org/veridu/development-guidelines).

1. Go to [Development Guideline's page on BitBucket](https://bitbucket.org/veridu/development-guidelines)
2. Fork it (https://bitbucket.org/veridu/development-guidelines/fork)
3. Clone your fork on your dev machine (`git clone git@bitbucket.org:devUser/development-guidelines.git`)
4. Add upstream repository remote (`git remote add upstream git@bitbucket.org:veridu/development-guidelines.git`)
5. Create a new branch for your new article (`git branch new-article -c`)
6. Add your content (`echo "woot!" > NewArticle.md`)
7. Add your changes (`git add NewArticle.md`)
8. Commit your changes (`git commit -m "Added my new Article!"`)
9. Push your commits to your fork (`git push origin new-article`)
10. Create a pull request (https://bitbucket.org/devUser/development-guidelines/pull-requests/new)
11. Enjoy!

# Side Notes

- You should **always** sync your repository (`git pull upstream master`) with upstream before pushing changes to be sure your changes are compatible with the latest work available.
- Project settings (except for the ones that should be consistent between dev/prod environments) must not be added to code repository and instead should be be distributed as `.dist` files, including documentation for each entry and possible different syntaxes whenever applicable.
- `.gitignore` files should ensure that log files, core dump files, backup files, editor/IDE files, build binaries and whatever else that shouldn't be part of the code repository is properly ignored from git tracking.

# Repository Setup

## BitBucket

### Access Management

Go to `Repository Settings` (e.g. https://bitbucket.org/veridu/scoringreports/admin/access), under **General**, click on *Access management* (e.g. https://bitbucket.org/veridu/scoringreports/admin/access).

#### Users

Ensure you remove yourself as an admin (change group access before removing yourself).

#### Groups

Ensure the following access policies according to your project audience:

- Backend
    - Administrators: `ADMIN`
    - Back-End: `READ`
    - Front-End: `READ`
    - Operations: `READ`
    - Scoring: `READ`
- Frontend
    - Administrators: `ADMIN`
    - Front-End: `READ`
    - Operations: `READ`
- Scoring
    - Administrators: `ADMIN`
    - Operations: `READ`
    - Scoring: `READ`

### Webhooks

Go to `Repository Settings` (e.g. https://bitbucket.org/veridu/development-guidelines/admin), under **Integrations**, click on *Webhooks* (e.g. https://bitbucket.org/veridu/development-guidelines/admin/addon/admin/bitbucket-webhooks/bb-webhooks-repo-admin).

#### Slack

- Title: `Slack`
- URL: `***REMOVED***`
- Status: `Active`
- Triggers: `Choose from a full list of triggers`
    - Pull Request: `Created` and `Merged`

## GitHub

### Webhooks

Go to `Repository Settings` (e.g. https://github.com/veridu/veridu-php/settings), on the left menu, click on *Webhooks & services* (e.g. https://github.com/veridu/veridu-php/settings/hooks).

#### Slack

- Payload URL: `***REMOVED***`
- Content type: `application/json`
- Secret: empty
- Which events would you like to trigger this webhook?: `Let me select individual events.`
    - `Pull request`
