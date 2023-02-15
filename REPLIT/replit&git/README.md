Впервые начав работотать с replit мне довелось столкнутся с несколькими вопросам по синхронизаций его и git.
В целом repllit заявляет поддерку работы с ним. Но для меня как начинающего стали возникать вопросы к тому как они взаимодействуют. Поэтому по пунктам пришлось разбираться.

#### 1. Как их соединить?
С помощью оболочки replit. Для этого надо зайти в "Profil" своего аккаунта, на странице редактирования профиля пролистать до блока "Connected services" в котором есть возможность связать профиль с другими сервисами (GitHub, Google, Facebook, Apple) нажать кнопку и действовать последовательно, как будет указанно.
С помощю shel кототорый тоже присутствует в оболочке replit. Надо будет вводить команды get. Метод мной еще не опробован.

#### 2. Как загрузить свой репозиторий на replit?
С помощью оболочки replit. Нажать Create, выскачит модальное окошко (создания нового проекта), обычно в нем нужно выбрать язык программирования и изменить имя проекта по умолчанию. Но в данном случаи достаточно выбрвть в правом верхнем углу "Import from GitHub" окошко изменится и появится возможность вставить ссылку на репозиторий. А вслучии уже состоявшегося присоединения как в пункте 1, появится список доступных репозиториев.
С помощю shel кототорый тоже присутствует в оболочке replit. Надо будет вводить команды get. Метод мной еще не опробован.

#### 2.1 Видимость доступных репозиториев?
Настройка видимости осуществляется в самом сервисе их хранения. У replit под полем ссылки на репозиторий появляется ссылка "Manage the GitHub repos Replit can import", при нажатии на которую, открывется вход на сервис (в новом окне).

#### 3. Как push'ить (обновлять на сервисе) репозиторий?
Как говорится тут придется попыхтеть, так как все не так просто. Все эксперементы проводил с помощю shel кототорый тоже присутствует в оболочке replit. В которой много ответных сообщений, в них сложно по началу разобраться. В зависимости от разных состояний синхронизаций между репозиториями, приходится проходить разные команды.
#### 3.1 Основная команда на отправку
git push - набирается в комадной сторке затем Enter. Если репозиторий на replit в готовом сотоянии, то он просто передастся на основной сервер. Далее варианты:
##### 3.1.1 Ответ shel который говорит, о том что изменения ушли на сервер. Примерно так:
    Enumerating objects: 12, done.
    Counting objects: 100% (10/10), done.
    Delta compression using up to 8 threads
    Compressing objects: 100% (6/6), done.
    Writing objects: 100% (6/6), 730 bytes | 730.00 KiB/s, done.
    Total 6 (delta 3), reused 0 (delta 0)
    remote: Resolving deltas: 100% (3/3), completed with 3 local objects.
##### 3.1.2 Ответ shel который говорит, о том что репозитории произошли изменения и его надо подготовить к отпраке. Примерно так:
    Everything up-to-date
Переходим к пункту подготовки репозитория. Готовим и снова повторяем git push.

##### 3.1.3 Ответ shel который говорит, о том что в репозитории на основном сервере произошло изменение. Примерно так:
    To https://github.com/Dmitry-A-K/netology_homework_html-css-javascript
    ! [rejected]        main -> main (fetch first)
    error: failed to push some refs to 'https://github.com/Dmitry-A-K/netology_homework_html-css-javascript'
    hint: Updates were rejected because the remote contains work that you do
    hint: not have locally. This is usually caused by another repository pushing
    hint: to the same ref. You may want to first integrate the remote changes
    hint: (e.g., 'git pull ...') before pushing again.
    hint: See the 'Note about fast-forwards' in 'git push --help' for details.
Это значит, что пока мы работали на replit в основном репозитории что то изменилось, а значит надо добавить эти изменния в наш репозиторий.
##### 3.1.4 Командой git pull надо получить эти изменения. Ответ примерно такой:
    remote: Enumerating objects: 14, done.
    remote: Counting objects: 100% (14/14), done.
    remote: Compressing objects: 100% (10/10), done.
    remote: Total 13 (delta 5), reused 1 (delta 0), pack-reused 0
    Unpacking objects: 100% (13/13), 3.02 KiB | 442.00 KiB/s, done.
    From https://github.com/Dmitry-A-K/netology_homework_html-css-javascript
      b611b5b..f880b12  main       -> origin/main
    Removing replit.nix
    Removing .replit
    Merge made by the 'recursive' strategy.
    .gitignore |   2 +
    .replit    | 179 ---------------------------------------------------------
    replit.nix |   6 --
    3 files changed, 2 insertions(+), 185 deletions(-)
    create mode 100644 .gitignore
    delete mode 100644 .replit
    delete mode 100644 replit.nix
##### 3.1.5 В этой части предстоит понять, что делать дальше?
Следует разобраться в ситуации. Понять как новые изменеия отразились на нашем коде. Если пользователь репозитория один, то он должен понимать что он менял и скорее всего изменения ему не навредят. Тогда можно смело использовать команду git push, которая просто отправит репозиторий обратно.

Если ведется командная работа, то тут придется глобально разбираться какие файлы затронуты и как они повлияют на код. Отдельная тема.

#### 3.2 Подготовка репозитория к отправке
git status - идеальная команда, для того что бы понять какие действия надо предпринять.
##### 3.2.1 В репозитории произошли изменения, редактировались файлы
    On branch main
    Your branch is up to date with 'origin/main'.
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
    modified:   1.1.-introduction-html-css/index.html
    no changes added to commit (use "git add" and/or "git commit -a")
В часности речь про то, в файле 1.1.-introduction-html-css/index.html были внесенны изменения
##### 3.2.2 В репозитории произошли изменения, добавились новые файлы
