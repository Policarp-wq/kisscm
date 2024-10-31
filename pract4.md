# Практическое задание №4. Системы контроля версий

## Задача 1

На сайте https://onlywei.github.io/explain-git-with-d3 или http://git-school.github.io/visualizing-git/ (цвета могут отличаться, есть команды undo/redo) с помощью команд эмулятора git получить следующее состояние проекта (сливаем master с first, перебазируем second на master): см. картинку ниже. Прислать свою картинку.
## Решение
![](images/git.png)

```
git commit --amend "init"
git commit
git checkout 12dfcd3
git checkout -b first
git commit
git commit
git checkout master
git checkout 12dfcd3
git tag "in"
git checkout master
git commit
git merge first
git checkout "in"
git checkout -b second
git commit
git commit
git rebase master
git checkout master
git merge second
git checkout "in"
```

![image](https://github.com/user-attachments/assets/d155765d-2c93-4b1f-a5b9-0bf7dbb4da68)


## Задача 2

Создать локальный git-репозиторий. Задать свои имя и почту (далее – coder1). Разместить файл prog.py с какими-нибудь данными. Прислать в текстовом виде диалог с git.
## Решение

```bash
policarp@DESKTOP-MHHUTTM:~$ mkdir forgit
policarp@DESKTOP-MHHUTTM:~$ cd forgit/
policarp@DESKTOP-MHHUTTM:~/forgit$ git config --global user.name "Eugene Policarp"
policarp@DESKTOP-MHHUTTM:~/forgit$ git config --global user.email "tatarkin-evgeniy@mail.ru"
policarp@DESKTOP-MHHUTTM:~/forgit$ git init
hint: Using 'master' as the name for the initial branch. This default branch name
hint: is subject to change. To configure the initial branch name to use in all
hint: of your new repositories, which will suppress this warning, call:
hint:
hint:   git config --global init.defaultBranch <name>
hint:
hint: Names commonly chosen instead of 'master' are 'main', 'trunk' and
hint: 'development'. The just-created branch can be renamed via this command:
hint:
hint:   git branch -m <name>
Initialized empty Git repository in /home/policarp/forgit/.git/
policarp@DESKTOP-MHHUTTM:~/forgit$ touch prog.py
policarp@DESKTOP-MHHUTTM:~/forgit$ git add .
policarp@DESKTOP-MHHUTTM:~/forgit$ git commit -m "Init"
[master (root-commit) d4a60d2] Init
 1 file changed, 0 insertions(+), 0 deletions(-)
 create mode 100644 prog.py
```

![image](https://github.com/user-attachments/assets/034b551b-c6a0-435c-9463-14f49a5ff11f)


## Задача 3

Создать рядом с локальным репозиторием bare-репозиторий с именем server. Загрузить туда содержимое локального репозитория. Команда git remote -v должна выдать информацию о server! Синхронизировать coder1 с server.

Клонировать репозиторий server в отдельной папке. Задать для работы с ним произвольные данные пользователя и почты (далее – coder2). Добавить файл readme.md с описанием программы. Обновить сервер.

Coder1 получает актуальные данные с сервера. Добавляет в readme в раздел об авторах свою информацию и обновляет сервер.

Coder2 добавляет в readme в раздел об авторах свою информацию и решает вопрос с конфликтами.

Прислать список набранных команд и содержимое git log.

Пример лога коммитов:

```
*   commit a457d748f0dab75b4c642e964172887de3ef4e3e
|\  Merge: 48ce283 d731ba8
| | Author: Coder 2 <coder2@corp.com>
| | Date:   Sun Oct 11 11:27:09 2020 +0300
| | 
| |     readme fix
| | 
| * commit d731ba84014d603384cc3287a8ea9062dbb92303
| | Author: Coder 1 <coder1@corp.com>
| | Date:   Sun Oct 11 11:22:52 2020 +0300
| | 
| |     coder 1 info
| | 
* | commit 48ce28336e6b3b983cbd6323500af8ec598626f1
|/  Author: Coder 2 <coder2@corp.com>
|   Date:   Sun Oct 11 11:24:00 2020 +0300
|   
|       coder 2 info
| 
* commit ba9dfe9cb24316694808a347e8c36f8383d81bbe
| Author: Coder 2 <coder2@corp.com>
| Date:   Sun Oct 11 11:21:26 2020 +0300
| 
|     docs
| 
* commit 227d84c89e60e09eebbce6c0b94b41004a4541a4
  Author: Coder 1 <coder1@corp.com>
  Date:   Sun Oct 11 11:11:46 2020 +0300
  
      first commit
```

```bash
*   commit 2c36f55049093fb14a676c1ef88fa5860ab96650 (HEAD -> master, server/master)
|\  Merge: 04b0359 a11934c
| | Author: Eugene Policarp <tatarkin-evgeniy@mail.ru>
| | Date:   Thu Oct 31 14:00:19 2024 +0300
| |
| |     Fixed conflict
| |
| * commit a11934c9a7002ddf65c8cb2a4827d6641a163ebf (eugene-features)
| | Author: Eugene Policarp <tatarkin-evgeniy@mail.ru>
| | Date:   Thu Oct 31 13:53:51 2024 +0300
| |
| |     Added Eugene to authors
| |
* | commit 04b035985f40324ccc2ee4c5b368fc6e5aeada40
|/  Author: Vadim <vadim@mail.ru>
|   Date:   Thu Oct 31 13:55:01 2024 +0300
|
|       Added Vadim to authors
|
* commit ad8b1339f0fb37ad4694524e0492ed594c734f12
| Author: Vadim <vadim@mail.ru>
| Date:   Thu Oct 31 13:44:33 2024 +0300
|
|     added readme
|
* commit f8637e0fc7a0033d12c132420e3dac60f718f014
```

Команды:

```
cd forgit
git remote add server ../server/
git revote -v
git remote -v
git push server main
git push server master
cd ..
cd server/
git log
ls
cd ..
git clone server work
cd work/
git config user.name "Vadim" && git config user.email "vadim@mail.ru"
ls
nano readme.md
git add . && git commit -m "added readme"
git remote -v
git push origin master
cd ../server/
cd forgit
git pull
git pull server master
git checkout -b eugene-features
nano readme.md
git add . && git commit -m "Added Eugene to authors"
cs
cd ../work/
gls
ls
sl
nano  readme.md
git add . && git commit -m "Added Vadim to authors"
cd ..
cd work/
git push origin master
cd ../forgit
ls
git pull server master
ls
cat readme.md
git switch master
ls
cat readme.md
git pull server master
cat readme.md
git merge eugene-features
nano readme.md
git merge eugene-features
git branch
cat readme.md
nano readme.md
git merge eugene-features
git add .
git merge eugene-features
git commit -m "Fixed conflict"
git merge eugene-features
cat readme.md
git push server master
git log --graph
```

## Решение

## Задача 4

Написать программу на Питоне (или другом ЯП), которая выводит список содержимого всех объектов репозитория. Воспользоваться командой "git cat-file -p". Идеальное решение – не использовать иных сторонних команд и библиотек для работы с git.

## Решение
