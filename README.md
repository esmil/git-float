# git-float


## What is this?

git-float is a script to help manage "floating commits". That is commits that you
keep rebasing locally and are not meant upstreaming or just not ready yet.

Using `git pull -r` git will automatically rebase local commits after pulling the
latest changes. However when you want to push some commits you first need
to rebase your commits to move the floating commits last, and then find the
SHA of the last non-floating commit that is ready to be pushed before doing
```sh
git push origin <SHA>:master
```
This process is where git-float will help you.


## How to use git-float

Mark your floating commits with the prefix `float!` in the commit header.
Enter your local git reposity, and type
```sh
/path/to/git-float -i
```
This will install a filter that automatically moves floating commits to the
end of the list when doing `git rebase -i`. It will also install a pre-push
hook that prevents you from pushing floating commits, and if you do it will
find the last non-floating commit SHA and suggest you use
```sh
git push <remote> <SHA>:<upstream branch>
```
instead.

If you no longer want to use git-float, just do
```sh
/path/to/git-float -u
```
to uninstall the hooks again.


## Licence

git-float released under GPLv2 or later to be compatible with [git].

[git]: https://git-scm.com/
