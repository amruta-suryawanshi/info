git tips [![GitHub Stars][stars-img]][stars-url] [![GitHub Forks][forks-img]][forks-url] [![GitHub Watchers][watchers-img]][watchers-url] [![Tweet][tweet-img]][tweet-url]
=
[github-url]: https://github.com/rsp/info
[readme-url]: https://github.com/rsp/info#readme
[issues-url]: https://github.com/rsp/info/issues
[stars-url]: https://github.com/rsp/info/stargazers
[watchers-url]: https://github.com/rsp/info/watchers
[forks-url]: https://github.com/rsp/info/network/members
[tweet-img]: https://img.shields.io/twitter/url/https/github.com/rsp/info/blob/master/git-tips.md.svg?style=social
[tweet-url]: https://twitter.com/intent/tweet?text=%23Git+Tips+by+@pocztarski:&url=https%3A%2F%2Fgithub.com%2Frsp%2Finfo%2Fblob%2Fmaster%2Fgit-tips.md
[license-url]: https://github.com/rsp/info/blob/master/LICENSE.md
[license-img]: https://img.shields.io/github/license/rsp/info.svg
[stars-img]: https://img.shields.io/github/stars/rsp/info.svg?style=social&amp;label=Stars
[forks-img]: https://img.shields.io/github/forks/rsp/info.svg?style=social&amp;label=Forks
[watchers-img]: https://img.shields.io/github/watchers/rsp/info.svg?style=social&amp;label=Watchers
[travis-url]: https://travis-ci.org/rsp/info
[travis-img]: https://travis-ci.org/rsp/info.svg?branch=master
[snyk-url]: https://snyk.io/test/github/rsp/info
[snyk-img]: https://snyk.io/test/github/rsp/info/badge.svg
[github-follow-url]: https://github.com/rsp
[github-follow-img]: https://img.shields.io/github/followers/rsp.svg?style=social&label=Follow
[twitter-follow-url]: https://twitter.com/intent/follow?screen_name=pocztarski
[twitter-follow-img]: https://img.shields.io/twitter/follow/pocztarski.svg?style=social&label=Follow
[stackoverflow-url]: https://stackoverflow.com/users/613198/rsp
[stackexchange-url]: https://stackexchange.com/users/303952/rsp
[stackexchange-img]: https://stackexchange.com/users/flair/303952.png

by [**Rafał Pocztarski**](https://pocztarski.com/)
[![Follow on GitHub][github-follow-img]][github-follow-url]
[![Follow on Twitter][twitter-follow-img]][twitter-follow-url]

Some of that ifo was originally written for my answers on Stack Overflow, see:

[![Follow on Stack Exchange][stackexchange-img]][stackoverflow-url]

How to push to two repos in one command
-
If you want to start from scratch then
create a repo in GitHub and clone it with:
```sh
git clone git@github.com:USER/REPO.git
cd REPO
```
where USER is your GitHub username and REPO is the name of your repository.

If you already have a local repo and want to add it to GitHub then create a new repo in GitHub but - instead of cloning it - add it to your existing local repo with:
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

Of course you can switch GitHub with GitLab and have it work the other way - pull from GitLab and push to both GitHub and GitLab.

It's also useful to add more specific remotes:
```sh
git remote add github git@github.com:USER/REPO.git
git remote add gitlab git@gitlab.com:USER/REPO.git
```
so that you can push to both remotes explicitly with:
```sh
git push github master
git push gitlab master
```

Instead of adding a second push URL to "origin" remote you can alternatively add a new remote called "all" with:
```sh
git remote add all git@github.com:USER/REPO.git
git remote set-url --add --push all git@github.com:USER/REPO.git
git remote set-url --add --push all git@gitlab.com:USER/REPO.git
```
and use "all" remote to push to both repos:
```sh
git push all master
```
but using "origin" may be more convenient if writing `git push origin master` (or (or [`gpom`](https://github.com/rsp/scripts/blob/master/gpom.md)) is in your muscle memory.

Author
------
[**Rafał Pocztarski**](https://pocztarski.com/)
<br/>
[![Follow on GitHub][github-follow-img]][github-follow-url]
[![Follow on Twitter][twitter-follow-img]][twitter-follow-url]
<br/>
[![Follow on Stack Exchange][stackexchange-img]][stackoverflow-url]

Share
-----
[Tweet the link to this article][tweet-url]
