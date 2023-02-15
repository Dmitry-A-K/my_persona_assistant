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

    On branch main
    Your branch is up to date with 'origin/main'.
    Untracked files:
        (use "git add <file>..." to include in what will be committed)
        .replit
        1.1.-introduction-html-css/index.html
        index.html
        replit.nix
    nothing added to commit but untracked files present (use "git add" to track)
    
Тут речь про то, что в репозотории появились новые файлы. Они могли быть добавленны при написании кода, либо само приложение их добавляет автамотически. Как избавится от файлов приложения в отдельной статье. Остальные файлы могут быть созданны кодом либо самим приложением (например отчет о работе, логи и тп.) Для начала просто их добавим в репозиторий. Новые файлы отмеченны красным цветом.
##### 3.2.3 Разрешаем внести все изменения.
git add -A - команда для разрешения всех изменений. Для случаев когда нужно внести только отдельные измененя команда git add <имя файла>. В ответ просто shel перейдет на новую строку, без каких либо сообщений.
##### 3.2.4 Нужно сделать commit.
На git add все не заканчивается. Так как на git push выпадет очередное сообщение

        Everything up-to-date
        А git status выдаст
        On branch main
        Your branch is up to date with 'origin/main'.
        Changes to be committed:
        (use "git restore --staged <file>..." to unstage)
        modified:   1.1.-introduction-html-css/index.html
    
Измененный файл будет подсвечен зелёным цветом.
И то и другое говорит о том, что надо сделать commit. Для этого нужно ввести команду git commit.
В результате команды должен открыться редактор в котором нужно набрать свои комментарии к изменениям. Вид приблизительно такой:
    
        # Please enter the commit message for your changes. Lines starting
        # with '#' will be ignored, and an empty message aborts the commit.
        #
        # On branch main
        # Your branch is up to date with 'origin/main'.
        #
        # Changes to be committed:
        #	modified:   1.1.-introduction-html-css/index.html
        #
Теперь ВНИМАНИЕ! Обязательно нужно что то написать иначе после закрытия редактора git выдаст сообщение об ошибке и не даст сделать git push. Сообщение такое:
    
        Aborting commit due to empty commit message.
    
Поэтому нужно обязательно написать, хоть что то. При этом нельзя начинать свое сообщение со знака #, так как git его не воспринимает в качестве комментария. Поэтому в качестве рекомендации, можно написать например [1234 или имя] бла-бла. Где цифры (или имя) это заголовок, а далее текст комментария. Так же важно помнить, что когда репозиторий загрузиться на основное хранилище, то комментарий станет виден для всех. Поэтому без мата и других излишеств.

После написания нужно просто закрыть редактор и git выведет сообщение:
    
        [main e0908f0] [my]
        1 file changed, 1 insertion(+), 1 deletion(-)
    
Это значит, что комментарий принят и добавлен, репозиторий готов к отправке. Теперь можно командовать git push, и наблюдать это сообщение:
    
        Enumerating objects: 7, done.
        Counting objects: 100% (7/7), done.
        Delta compression using up to 8 threads
        Compressing objects: 100% (4/4), done.
        Writing objects: 100% (4/4), 456 bytes | 456.00 KiB/s, done.
        Total 4 (delta 2), reused 0 (delta 0)
        remote: Resolving deltas: 100% (2/2), completed with 2 local objects.
        ae8377f..e0908f0  main -> main
    
#### 4. Магия синхронизации
После всего этого можно смело отправляться в основной репозитарий и наблюдать пернос. Потом отдохнуть от трудов праведных. Только нельзя забывать, что пока мы этого не сделаем ничего не сихронизируется. Следовательно надо взять в привычку, по окончании работы отправить рабочий репозиторий в цент. Иначе работа (заказчик) может заставит делать это все ночью.


<i> Вопрос как все это автоматизировать подлежит дальнейшему обсуждению.
