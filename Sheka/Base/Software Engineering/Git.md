18.04.2022  11:37
Tags:  |
____

# Git
### general
untracked files - созданные файлы, которые не были добавлены в индексацию (stage)
Чтобы посмотреть список опций к командам, надо использовать -h
`git config -h`
Чтобы подробно узнать о команде используй help
`git help config`

### git config
Все результаты работы в командной строке с командой git config буду лежать в .git/config, т.е. можно просто редактировать тот файл.
```git
$ git config user.name "egorsheka"
$ git config user.mail "egorsheka@gmail.com"
```
Сохранить логин и пароль на компе автоматически
```git
// local
$ git config credential.helper store
// global
$ git config --global credential.helper store
$ git push http://example.com/repo.git
Username: <type your username>
Password: <type your password>

[several days later]
$ git push http://example.com/repo.git
[your credentials are used automatically]
```
https://git-scm.com/book/ru/v2/%D0%98%D0%BD%D1%81%D1%82%D1%80%D1%83%D0%BC%D0%B5%D0%BD%D1%82%D1%8B-Git-%D0%A5%D1%80%D0%B0%D0%BD%D0%B8%D0%BB%D0%B8%D1%89%D0%B5-%D1%83%D1%87%D1%91%D1%82%D0%BD%D1%8B%D1%85-%D0%B4%D0%B0%D0%BD%D0%BD%D1%8B%D1%85
### git diff, git show, git status, git add -p, git commit -a
`git diff` - показывает изменения в untracked files
`git diff --staged` - показывает изменения в индексе
`git show` - позволяет просто посмотреть что произошло в коммите, выводит последний коммит
`git show --pretty=fuller` -более подробно при опции 
`git status` позволяет увидеть непроиндексированные файлы и untracted файлы.

`git add -p MyJavaClass.java` консоль будет спршивать добавлять ли каждый фрагмент изменения в индекс или нет. (y or n) 

`git commit -a` позволяет закомитеть изменённые файлы без `git add`, но untracked files не будут закоммичены.
`git commit -m "Only this file" <path>(например .gitignor)` позволяет без `git add` закоммитеть конкретный файл, но untracked file не сможет быть закоммичен.

`git add .` добавить всё в текущей директории.
`git add -A` добавить всё в проекте.

### git branch
ветка - это указатель на коммит
`git branch` - список локальный веток
`git branch -r`
`git branch - a` - список всех веток(локальных + удалённых)

`git branch new_branch` - создание ветки без переключения на неё 
**теперь на один и тот же коммит будет указывать две ветки**
`git branch -f master 54a3` - передвинуть ветку на конкретный коммит
таким образом можно просто работать в мастере, делать там коммиты, в конце работы создать новую ветку, а указатель мастера передвинуть на нужный коммит(`git checkout new_branch`, `git branch -f master 54a3`). 

`git branch -d` - удаление ветки (`-D` принудительно удаление)
`git branch -m old_branch new_branch` переминовать ветку
иногда возможно восоздать удалённую ветку, для этого нужно найти необходимый последний коммит с помощью `git reflog --date=iso`, а затем воссоздать ветку `git branch old_branch HEAD@{6}` иногда в windows 'HEAD@{6}' надо брать в кавычки

`git push origin --delete crazy-experiment` - удалить ветку на удалённом репозитории
### git checkout 
`git checkout my_branch` - переключиться на ветку 
**при переключении с ветку на ветку индексация сохраняется, если в коммитах веток сделаны изменения в разных файлах, т.е. на второй ветке можно случайно закоммитеть ненужные изменения**
т.е. можно вести разработку в master, добавить все изменения в индексацию, а потом просто переключиться на новую ветку и закоммитеть всё.

`git checkout -b new-branch` - создание ветки и переключение на неё
`git checkout -f my_branch` - переключиться на ветку и удалить всё из индексации

`git checkout 32d5 README.md` - возвращает в индексацию состояние файла из коммита 32в5
### git merge
если в мастере не было коммитов после создание новой векти из него, то при мердже указатель мастера просто перемиститься на последний коммит новой ветки
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
### удаление, переменование 
просто удаляешь или переменовываешь файл, затем git add и git commit. 
если же надо удалить чисто из индиксации(сам файл останется), то команда 
`git rm --cashed <path>` 
`git rm -r --cashed <directory>` для директорий
`git checkout -f HEAD` - удалить всю индексацию
`git clean -dxf` - удалить все untracked файлы и директории (`d` файлы и директории, `x` ignore файлы `f` подтверждение)
### git reset
`git reset --hard` = `git checkout -f`
`git reset` - сделает все индексированные файлы неиндексированными 

`git reset --hard 23a3` - перенесёт HEAD и master на коммит 23a3 (+ удаляется вся индексация, untracked files удаляются только с помощью `git clean`)
`git reset --soft 23a3` -  перенесёт HEAD и master на коммит 23a3 (индексация останется, также в индексацию перенесутся все прошлые коммиты)
`git reset 23a3(по умолчанию --mixed)` -  перенесёт HEAD и master на коммит 23a3, файлы, которые были в индексации, теперь будут непроиндексированными 

при применении `git reset`, коммит с которого переместились можно найти по указателю `ORIG_HEAD`, т.е. чтобы вернуться обратно достаточно `git reset --soft ORIG_HEAD`

`git commit --amend` - внести новые изменения в прошлый коммит (т.е. вносим изменения, `git add`, `git commit --amend`) = `git reset --soft @~`, `git add`, `git commit -c ORIG_HEAD`(возьмёт коммент из прошлого коммита; чтобы выйти из консоли `esc` `:q` `enter`)
###  восстановление предыдущих версий файлов
`git checkout 54a3 index.html` - сделает файл или директорию такой, какая в указаном коммите
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

проделать кейс. 
удалить 3 последних коммита с удалённого репо и закинуть новые 
git grep
____ 
### Links
- https://www.gitkraken.com/learn/git
- https://www.atlassian.com/ru/git/tutorials/saving-changes/git-stash