#
1. branch 只是一个路标, a label of commit
2. HEAD 和 branch 的区别是, branch一直指向本branch的最新commit，而HEAD会随着branch的checkout而跳转到另一个branch的最新commit
3. checkout 可以到branch，也可以到commit SSH
4. Detached HEAD (vs attached)。 Normal HEAD 都是在branch 的latest commit。Detached HEAD允许你跳转到任何一个commit。
5.
6. 1
 git fetch upstream master (at any HEAD)
 git merge upstream/master (at HEAD main)
 git checkout -b master-copy origin/master (at any HEAD)
 git push origin main:master (at any HEAD)
 git rebase --onto master feature_a feature_b
 
git push -d <remote_name> <branchname>

git rebase -i 'commit_id'
git commit -ammend

git checkout -b mr36 upstream/merge-requests/36





 
