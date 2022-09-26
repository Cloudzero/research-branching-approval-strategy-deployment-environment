test

# approval-strategy-deployment-environment

This repository simulates a Deployment strategy using [GitHub Action](https://docs.github.com/en/actions/deployment/about-deployments/about-continuous-deployment) using [GitHub Environments](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment).

## Overview

We will maintain the CloudZero usage of the develop branch and the main branch.  Developers will create feature branches and us PR to move changes to develop. Moving changes to the main branch will happens like it does today following the [Development Process](https://cloudzero.atlassian.net/wiki/spaces/ENG/pages/40468620/Deployment+Process)

This is were the change happens, before deploying to "live", the deployment will need to be approved.

Here are the command to move from develop to main.

```text
git checkout develop
```

```text
git pull --rebase origin develop
```

```text
git checkout main
```

```text
git pull --rebase origin main
```

```text
git merge --ff-only develop
```

```text
git status
```

```text
git push origin main
```

The push to main will kick of the deployment to 'live', however, it will pause until it is approved.

## Knowing what is in each environment?

What ever is on the develop or main branch is what is deployed to alfa or main as long as the deployment workflow ran successfully.
If the workflow were to fail, then what is in the namespace (live/alfa) is the last know successful deployment. A deployment can be visualized in the "Actions" tab.
The last successful git hash can be used to checkout the code to work on code that is in a namespace.
![Actions tab view](assets/Actions_failures.png)

## Rollbacks

There are no rollbacks. Developer has to push a change to main.

## Using environments for deployment

GitHub has this note [here](https://docs.github.com/en/actions/deployment/targeting-different-environments/using-environments-for-deployment#creating-an-environment)

> Environments, environment secrets, and environment protection rules are available in public repositories for all products. For access to environments, environment secrets, and deployment branches in private or internal repositories, you must use GitHub Pro, GitHub Team, or GitHub Enterprise. For access to other environment protection rules in private or internal repositories, you must use GitHub Enterprise. For more information, see "GitHub's products."

See this link for [pricing](https://github.com/pricing)
