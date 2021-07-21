# How to pull a branch after a force push

According to a [post on SO] this can be a handy workflow:

```shell
# receive the new commits
$ git fetch

# reset the commit in the local branch to the latest version on remote dropping everything you have locally
$ git reset origin/<BRANCH_NAME> -—hard
```

[post on SO]: https://stackoverflow.com/questions/9813816/git-pull-after-forced-update
