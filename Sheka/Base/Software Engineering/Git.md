18.04.2022  11:37
Tags:  |
____

# Git
### git merge
ветка - это указатель на коммит
`git branch` - список локальный веток
`git branch - a` - список всех веток(локальных + удалённых)
`git branch new_branch` - создание ветки без переключения на неё 
`git checkout -b new-branch` - создание ветки и переключение на неё
`git branch -d` - удаление ветки (`-D` принудительно удаление)
`git branch -m old_branch new_branch` переминовать ветку

`git push origin --delete crazy-experiment` - удалить ветку на удалённом репозитории

`git checkout my_branch` - переключиться на ветку 

**Чтобы проделать операцию слияние необходимо:**

`git checkout -b some-feature  `
# Edit and commit some files  
`git checkout main `
`git pull`
**`git merge some-feature `**
`git branch -d new-feature`
![[Pasted image 20220419170745.png]]

при появление конфликта необходимо:
1) изменить файлы
2) git add, git commit


### git pull
git pull = git fetch + git merge 

### git stash
- `git stash save "add style to our site"` - поместить в хранилище 
- `git stash pop` - удалить с хранилища и вставить в текущую ветку
- `git stash apply` - вставить в текущую ветку не удаляя

При этом следующие файлы отложены **не** будут:
1) новые файлы в рабочей копии, которые еще не были проиндексированы;
2) игнорируемые файлы(.gitignore).
Чтобы добавить всё используй:
- `git stash -u` (`--include-untracked`)
- `git stash -a` ( `--all`)
![[01.svg]]
- `git stash list` - посмотреть все наборы отложенных изменений 
```git
$ git stash list  
stash@{0}: On main: add style to our site  
stash@{1}: WIP on main: 5002d47 our new homepage  
stash@{2}: WIP on main: 5002d47 our new homepage
```

- `git stash pop stash@{2}` - достать конкретный 
- other command -   [https://www.atlassian.com/ru/git/tutorials/saving-changes/git-stash](https://www.atlassian.com/ru/git/tutorials/saving-changes/git-stash)

## не усвоил
https://www.atlassian.com/ru/git/tutorials/using-branches/merge-conflicts
____ 
### Links
- https://www.gitkraken.com/learn/git
- https://www.atlassian.com/ru/git/tutorials/saving-changes/git-stash