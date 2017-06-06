### Move a git repo with history

Move a git repo with all the branches and history from one server to another.

```
git clone --mirror <URL to my OLD repo location>
cd <New directory where your OLD repo was cloned>
git remote set-url origin <URL to my NEW repo location>
git push -f origin
```

- Source(s)
  - [stackoverflow.com](http://stackoverflow.com/questions/1484648/how-to-migrate-git-repository-from-one-server-to-a-new-one)
