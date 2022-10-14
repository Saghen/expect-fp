# Using Git Sub Tree to Update

Since Jest is a monorepo, we use `git subtree` to keep up to date. Full guide can be found here: https://stackoverflow.com/questions/24577084/forking-a-sub-directory-of-a-repository-on-github-and-making-it-part-of-my-own-r

> When you're dealing with the upstream repository, you will have to use a mix of git and git subtree commands. To get new filtered commits, we need to do it in three stages.

> In the first stage, we'll update upstream-master to the current version of the XBMC repository.

```
git checkout upstream-master
git pull
```

> This should pull down new commits, if there are any.

> Next, we will update upstream-skin with the new filtered version of the commits. Since git subtree ensures that commit hashes will be the same, this should be a clean process. Note that you want to run these commands while still on the upstream-master branch.

```
git subtree split --prefix=addons/skin.confluence \
  --onto upstream-skin -b upstream-skin
```

> With upstream-skin now updated, you can update your master branch as you see fit (either by merging or rebasing).

```
git checkout master
git rebase upstream-skin
```
