# 2. Contribute with Git

Before creating your first pull request, set up your fork to contribute to PyRIT by following these steps:

1. [Fork](https://github.com/Azure/PyRIT/fork) the repo from the main branch. By default, forks are named the same as their upstream repository. This will create a new repo called `GITHUB_USERNAME/PyRIT` (where `GITHUB_USERNAME` is a variable for your GitHub username).
1. Add this new repo locally wherever you cloned PyRIT
```
# to see existing remotes
git remote -v

# add your fork as a remote named `REMOTE_NAME`
git remote add REMOTE_NAME https://github.com/GITHUB_USERNAME/PyRIT.git
```

To add your contribution to the repo, the flow typically looks as follows:
```
git checkout main
git pull # pull from origin
git checkout -b mybranch

... # make changes

git add .
git commit -m "changes were made"
git push REMOTE_NAME
```

After pushing changes, you'll see a link to create a PR:
```
remote: Create a pull request for 'mybranch' on GitHub by visiting:
remote:      https://github.com/GITHUB_USERNAME/PyRIT/pull/new/mybranch
```

See more on [creating a pull request from a fork](https://docs.github.com/en/pull-requests/collaborating-with-pull-requests/proposing-changes-to-your-work-with-pull-requests/creating-a-pull-request-from-a-fork).
