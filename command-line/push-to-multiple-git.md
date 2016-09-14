### Push/pull to multiple Git locations

Working with multiple git remotes can be awkward. In my use case I wanted to push the same repository (my notes) between a Github instance behind a firewall and a private repository on Github.com. Git has support natively for multiple

```
git remote set-url origin --push --add user1@repo1
git remote set-url origin --push --add user2@repo2
git remote -v
```

- Source(s)
  - [stackoverflow.com](http://stackoverflow.com/questions/849308/pull-push-from-multiple-remote-locations/12795747#12795747)
