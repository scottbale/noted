# Git and Mercurial
## Side-by-side

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------
scenario                                                              hg                                                                             git
--------------------------------------------------------------------- ------------------------------------------------------------------------------ ----------------------------------------------------------------------------

clone a repo                                                          hg clone
ignore file                                                           .hgignore                                                                      .gitignore
global config file                                                    ~/.hgrc                                                                        ~/.gitconfig
cmd-specific help                                                     hg help foo                                                                    man git-foo

status                                                                hg status; hg st                                                               git status; gs
status (ignoring untracked)                                           hg st -armd
summary                                                               hg summary

remote repo aliases                                                   hg paths                                                                       git remote -v
add remote                                                            (hand-edit .hg/hgrc ?)                                                         git remote add name url
track remote branch                                                                                                                                  git branch [--track|--set-upstream] branch-name origin/branch-name

log changes for specific user and/or path                             hg log -u sbale -l 3 path                                                      git log -3 path
graphical log                                                         hg glog -l 8             [includes branches]

update working dir (or switch revisions) [discard uncommitted]        hg up [-C] [default|2112]; hg co; hg checkout; hg update
revert                                                                hg revert --no-backup -r 2113 [-a|path/to/foo.hs]
commit specific file w/ message                                       hg commit -m "yadda yadda" something.clj
get latest revisions from remote repo                                 hg pull                                                                        git fetch
...and update to new branch head                                      hg pull -u                                                                     git pull
...and rebase working directory to branch head                        hg pull --rebase
see any incoming changes                                              hg in; hg incoming
push specific revision to remote repo                                 hg push -r 2113
push revision with new head                                           hg push -f -r 2113
add to vc                                                             hg add foo
remove from vc                                                        hg remove foo; hg rm foo
see difference                                                        hg diff
...in specific revision                                               hg diff -c 2112
meld                                                                  hg meld [-c 2112] (see ~/.hgrc)
identity of current (or specific) revision                            hg id -nib [-r 2112]
remove untracked files from working copy                              hg purge

rebase                                                                hg rebase [--collapse] -s 2112 -d 2115                                         git rebase upstream branch
remove revision (and children)                                        hg strip 2112
stash/unstash                                                         hg shelve [foo.hs] / hg unshelve                                               git stash [foo.hs] / git stash pop
merge working dir w/ revision [using tool]                            hg merge -r 2115 [-t internal:local]  (see hg help merge-tools)
see/resolve merge conflicts                                           hg resolve [-l]
cherry-pick                                                           hg graft 2113

create a branch                                                       hg branch teh-awesome
update working dir to tag or branch                                   hg up teh-awesome     
push revision with new branch                                         hg push --new-branch -r 2113
close a branch                                                        hg commit --close-branch

---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

# TERMINOLOGY

## hg
path - symbolic name for remote repository
default, default-push - path names with special meaning for push/pull
head - changeset with no children 
tip - special reserved name, tag that identifies the most recent revision

## git
head - 
master - special built-in main branch name?
tree -
trunk -
pull - fetch + merge
