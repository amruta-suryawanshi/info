git tips
========

How to push to two repos in one command
-
Create a repo in GitHub and clone it with:
```sh
git clone git@github.com:USER/REPO.git
```
where USER is your GitHub username and REPO is the name of your repository.

If you already have a local repo and want to add it to GitHub then create a new repo n GitHub and instead of cloning add it to your existing local repo with:
```sh
git remote add origin git@github.com:USER/REPO.git
```
Now, create a new repo on GitLab with the same name.

And add **both** GitHub and GitLab repos as push urls for the "origin" remote:
```sh
git remote set-url --add --push origin git@github.com:USER/REPO.git
git remote set-url --add --push origin git@gitlab.com:USER/REPO.git
```
(Note that you need to repeat the GitHub link even though it was already set with `git clone` or `git remote add origin` before.)

Now every time you run:
```sh
git push origin master
```
(or [`gpom`](https://github.com/rsp/scripts/blob/master/gpom.md) if you're using [my scripts](https://github.com/rsp/scripts))

your code will be pushed to both GitHub and GitLab.
Pulling/fetching from "origin" will use only GitHub.

It can be useful if you want to have a backup repo or if you want to use GitLab CI while promarily working on GitHub.

Unlike Travis, GitLab CI has a modern GCC version installed by default but it only tests repos hosten on GitLab. Pushing your repo to both GitHub and GitLab can be used to test your code with modern GCC on GitLab CI.

