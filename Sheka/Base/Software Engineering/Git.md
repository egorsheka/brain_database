18.04.2022  11:37
Tags:  |
____

# Git
### general
![[Pasted image 20220503091611.png]]
untracked files - созданные файлы, которые не были добавлены в индексацию (stage)
Чтобы посмотреть список опций к командам, надо использовать -h `git config -h`
Чтобы подробно узнать о команде используй help `git help config`

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
### git log
`git log -p` - показать коммиты, показывающие внесённые изменения
`git log feature/PRG029-679 --first-parent` - показать коммиты только к данной ветки, без доп коммитов от слияния
### git diff, git show, git status
`git diff` - показывает изменения в working directory по сравнению с индексацией (untracked files не показывает)
`git diff --staged(или --cashed)` - показывает изменения в индексе
https://www.youtube.com/watch?v=1oExHLJXBIg&list=PLDyvV36pndZFHXjXuwA_NywNrVQO0aQqb&index=28

`git show` - позволяет просто посмотреть что произошло в коммите, выводит последний коммит
`git show --pretty=fuller` -более подробно при опции 

`git status` позволяет увидеть непроиндексированные файлы и untracted файлы.


### git add, git commit
`git add -p MyJavaClass.java` консоль будет спршивать добавлять ли каждый фрагмент изменения в индекс или нет. (y or n) 

`git commit -a` позволяет закомитеть изменённые файлы без `git add`, но untracked files не будут закоммичены.
`git commit -m "Only this file" <path>(например .gitignor)` позволяет без `git add` закоммитеть конкретный файл, но untracked file не сможет быть закоммичен.

`git add .` добавить всё в текущей директории.
`git add -A` добавить всё в проекте.
### git branch
ветка - это указатель на коммит
`git branch` - список локальный веток
`git branch -r` - список удалённых веток
`git branch - a` - список всех веток(локальных + удалённых)

`git branch new_branch` - создание ветки без переключения на неё, **теперь на один и тот же коммит будет указывать две ветки**
`git branch -f master 54a3` - передвинуть ветку на конкретный коммит
таким образом можно просто работать в мастере, делать там коммиты, в конце работы создать новую ветку, а указатель мастера передвинуть на нужный коммит(`git checkout new_branch`, `git branch -f master 54a3`). 

`git branch -d` - удаление ветки (`-D` принудительно удаление)
`git branch -m old_branch new_branch` переминовать ветку

иногда возможно восоздать удалённую ветку, для этого нужно найти необходимый последний коммит с помощью `git reflog --date=iso`, а затем воссоздать ветку `git branch old_branch HEAD@{6}` иногда в windows 'HEAD@{6}' надо брать в кавычки

### git checkout 
`git checkout my_branch` - переключиться на ветку 
**при переключении с ветку на ветку индексация сохраняется, если в коммитах веток сделаны изменения в разных файлах, т.е. на второй ветке можно случайно закоммитеть ненужные изменения**, т.е. можно вести разработку в master, добавить все изменения в индексацию, а потом просто переключиться на новую ветку и закоммитеть всё.

`git checkout -b new-branch` - создание ветки и переключение на неё
`git checkout -f my_branch` - переключиться на ветку и удалить всё из индексации

`git checkout 32d5 README.md` - возвращает в индексацию состояние файла из коммита 32в5
### git merge
если в мастере не было коммитов после создание новой векти из него, то при мердже указатель мастера просто перемиститься на последний коммит новой ветки
если же были, то создаётся коммит слияния, который просто является маркером, что ветки теперь слиты. В коммите могут быть видны изменения файла, если они были сделаны во время слияния (обычно при конфликте)

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
2) `git add`,  `git commit --no-edit` или `git merge --continue`

можно выбрать все изменения из текущий весрии `git checkout --ours filename`
можно выбрать все изменения из вливаемой ветки `git checkout --theirs filename`
`git checkout --conflict=diff3 --merge filename` - изменит файл таким образом, что будет отдельно видно, что было в ветках
`git checkout --merge` - вернёт версию с маркерами конфликта
отмена слияния `git reset --hard`, но если надо оставить непроиндексированные файлы, то тогда
`git reset --merge` = `git merge --abort`

`git merge my_branch --no-commit` - после слияния коммит не будет сделан, есть возможность что-то добавить в  слияние, а затем уже закоммитеть, обычно делается при семантических(логических) ошибок

`git merge --squash my_branch` - добавит в индексацию все сделаные изменения из `my_branch` 
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

при применении `git reset`, коммит с которого переместились можно найти по указателю `ORIG_HEAD`, т.е. чтобы вернуться обратно достаточно `git reset --soft ORIG_HEAD` или посмотреть нужный коммит в `git reflog` и также перейти на него `git reset --hard 38d5`

`git commit --amend` - внести новые изменения в прошлый коммит (т.е. вносим изменения, `git add`, `git commit --amend`) = `git reset --soft @~`, `git add`, `git commit -c ORIG_HEAD`(возьмёт коммент из прошлого коммита; чтобы выйти из консоли `esc` `:q` `enter`)
### git revert
команда используется, если разработка ведётся на одной ветке с несколькими разработчиками, в ситуции, когда кто-то уже запулил ненужный коммит. 
`git revert 23s5` - создает коммит противоположному коммиту 23s5
`git revert 64a2..23s5` - создает серию противоположных коммитов для диапозона 64a2 - 23s5
`git revert 3452 -m 1` - этот вариант отменяет все изменения, сделанные командой git merge, и восстанавливает состояние ветки (в которую происходило вливание) до мерджа

### cherry-pick
`git cherry-pick 23d2` - скопировать коммит в свою ветку
`git cherry-pick -n 23d2` - скопировать коммит себе в индех
`git cherry-pick master..feature` - скопировать все коммиты из feature
`git cherry-pick --abort` - отменить копирование в случае конфликта
`git cherry-pick --continue` - продолжить после конфликта
`git cherry-pick --quit` - оставить все коммиты до конфликта и выйти
### git rebase
по сравнению с merge лучше тем, что упрощает историю коммитов, нет никаких коммитов слияния.
хуже тем, что можно работать только в приватных ветках, возможы логические ошибки в коммитах
можно использовать, если внимательно отнисится к истории разработки, есть код-ревью, компилить проект после `rebase`, наличие тестов
 
`git rebase master`
![[Pasted image 20220501135751.png]]
`git rebase --abort` - отменит ребейз и вернёт всё как было 
`git rebase --skip` - пропустить конфликтный коммит 
`git rebase --continue` - продолжить после конфликта
`git reset --hard ORIG_HEAD` - откатить rebase или же смотреть `git reflog my_branch` 

`git rebase --onto master feature` - перебазировать текущую ветку на master начиная с коммита feature

Rebase по умолчанию пропускает коммиты слияния вместе с внесёнными в них изменениями


git rebase master     | git rebase --rebase-merges master       
--------- | -----------
![[Pasted image 20220501151802.png]] |  ![[Pasted image 20220501151701.png]]         

###  восстановление предыдущих версий файлов
`git checkout 54a3 index.html` - сделает файл или директорию такой, какая в указаном коммите
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

### git pull
git pull = git fetch + git merge 

### git push
`git push --force-with-lease origin <имя_ветки>`
Такой вариант лучше чем git push --force origin <имя_ветки>, тем что если кто-то успел запушить свои коммиты после того, как мы забирали изменения с сервера, то он не будет их перетирать, а выдаст нам ошибку, после чего мы сможем интегрировать чужие коммиты со своими изменениями и попытаться сделать push --force-with-lease ещё раз.
`git push origin --delete crazy-experiment` - удалить ветку на удалённом репозитории
`git push --set-upstream origin corrected-branch-name` - переменовать ветку на удалённом репозитории
https://urvanov.ru/2017/09/19/%D0%BE%D0%BF%D0%B0%D1%81%D0%BD%D0%BE%D1%81%D1%82%D1%8C-git-push-force-%D0%B8-%D0%BF%D0%BE%D0%BB%D0%B5%D0%B7%D0%BD%D0%BE%D1%81%D1%82%D1%8C-git-push-force-with-lease/
### интересно посмотреть

32 видео
46 видео
47 видео
49 виедо
50 видео

https://www.atlassian.com/ru/git/tutorials/using-branches/merge-conflicts

проделать кейс. 
удалить 3 последних коммита с удалённого репо и закинуть новые 
git grep
git bisect
git tree
pre-commit
git branch -merged
git rebase -i
Команда _git rebase_ (перебазирование) — применяет коммиты текущей ветки после коммитов ветки _(base tip)_, указанной в команде rebase. С помощью rebase можно выполнять целый ряд задач: слияние веток, перемотку _(fast forwarding)_, изменение коммитов текущей ветки (редактирование, именование, удаление, слияние, перетасовка коммитов), пересадку текущей ветки (с помощью опции _—onto_) и др.
git cherry-pick -m 1 63ad84c  https://www.toptal.com/git/interview-questions
____ 
### Links
- https://www.gitkraken.com/learn/git
- https://www.atlassian.com/ru/git/tutorials/saving-changes/git-stash