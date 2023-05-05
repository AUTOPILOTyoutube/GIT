# __GIT - КРАТКОЕ РУКОВОДСТВО ПОЛЬЗОВАТЕЛЯ__

![Иллюстрация к проекту](https://github.com/autopilotyoutube/GIT/raw/main/files/pictures/Git_logo.png)

[ОФИЦИАЛЬНЫЙ САЙТ GIT](https://git-scm.com/)

### GIT - это система контроля версий файлов, находящаяся на локальном компьютере.
___

__УСТАНОВКА GIT__  
Для Ubuntu этот PPA предоставляет последнюю стабильную восходящую версию Git:

    sudo add-apt-repository ppa:git-core/ppa
    sudo apt update
    sudo apt upgrade
    sudo apt install git

__УЗНАТЬ ТЕКУЩУЮ ВЕРСИЮ УСТАНОВЛЕННОГО GIT__  
    
    git --version

__ДОБАВЛЯЕМ СВОЁ ИМЯ__

    git config --global user.name "[имя пользователя]"
- config - изменение конфигурации Git
- --global    - имя настроено глобально для всех репозиториев
- user.name   - настройка имени автора

__ДОБАВЛЯЕМ СВОЮ ПОЧТУ__

    git config --global user.email [почта]

Рекомендую указывать имя пользователя и почту как на githab.com

__ПРОВЕРИТЬ НАСТРОЙКИ GIT__

    git config --list

__Выйти из просмотра текстовой информации настроек__

    :q
___

__СОЗДАТЬ НОВЫЙ РЕПОЗИТОРИЙ GIT__

    git init

Эта команда вводится в папке, в которой мы хотим создать новый репозиторий git. Количество репозиториев неограничено.
Появится скрытая папка .git, она называется репозиторием git, и она создается автоматически в проекте.
___

__ОБЛАСТИ GIT__

- working directory   -рабочая директория
- staging area        -индекс (подготовка к коммиту)
- repository          -репозиторий

В __working directory__ находятся файлы и папки нашего проекта.  
В __staging area__ добавляем индексы файлов, подготавливаем файлы для коммита, которые хотим добавить в репозиторий git.  
В __repository__ добавляем все файлы из __staging area__.  
Все объекты git находятся в папке __.git/objects__. Здесь сохраняются разные версии файлов проекта.
___

__ДОБАВИТЬ ВСЕ файлы (новые и модифицированные) в индекс (staging area)__  
    
    git add .

__ДОБАВИТЬ ОДИН файл в индекс (staging area)__:  

    git add file.txt

__СОХРАНИТЬ ИЗМЕНЕНИЯ В РЕПОЗИТОРИИ (КОММИТ)__  
(Все файлы из индекса (staging area) будут перенесены и сохранены в репозитории)  

    git commit -m "[сообщение]"
___

__ПЕРЕЙТИ К ОПРЕДЕЛЁННОЙ ВЕРСИИ ПРОЕКТА__  
(Гит перемещает файлы из Репозитория в Рабочую директорию)  

    git checkout [commit hash]
    git checkout [branch name]
- commit hash - переход к определённому коммиту по его кешу SHA1, достаточно указать несколько первых символов кеша.
- branch name - переход в определенную ветку проекта по названию ветки. Ветка ссылается на последний коммит в ветке.  

Не рекомендуется, чтобы ссылка (указатель на метку) указывала на коммит. Ссылка должна указывать на ветку. Перевести ссылку на ветку:  
    
    git checkout master
- master - имя ветки

___
__ПОСМОТРЕТЬ ТЕКУЩЕЕ СОСТОЯНИЕ РЕПОЗИТОРИЯ Git__  

    git status

Мы увидим:
- Какие файлы были изменены
- Какие файлы были добавлены
- Какие файлы уже находятся в индексе (staging area)
___

__СТАТУСЫ ОТСЛЕЖИВАНИЯ ФАЙЛОВ__
- Untracked   -неотслеживаемый (новый файл)
- Staged      -подготовленный (добавленный в индекс)
- Unmodified  -немодифицированный (когда в рабочей директории и в репозитории находится один и тот же файл)
- Modified    -модифицированный (файл в рабочей директории отличается от файла в репозитории)
___

__ТИПЫ ОБЪЕКТОВ В GIT__
- Blob            -файл
- Tree            -папка
- Commit          -коммит (сохранение текущей версии проекта)
- Annotated Tag   -аннотированный тег

Каждый объект в Git имеет свой уникальный ID-хеш, сгенерированный с помощью хеш-функции SHA1, фиксированная длина хеша (160 бит - 40 шестнадцатеричных символов 1-10, А-F).
На сгенерированных хешах объектов основано название файлов или папок в папке objects.

Коллизия - когда двум объектам даётся одинаковый хеш, бывает очень редко.
___

__КОММИТ - ссылка на дерево (папку)__  
Гит создает уникальный объект для каждой папки и уникальный объект для каждого файла.

__СОЗДАНИЕ КОММИТА С ЗАПИСЬЮ ИЗМЕНЕНИЙ В РЕПОЗИТОРИЙ__  

    git commit -m "[message]"

__СТРУКТУРА КОММИТА:__  
Свой SHA1-хеш  
Имя и email автора  
Описание коммита  
Ссылка на Родительский(е) коммит(ы) (SHA1-хеш)  
Ссылка на Дерево (SHA1-хеш)  

Каждый следующий коммит ссылается на предыдущий. Все объекты гит связываются между собой с помощью SHA-1 хешей.

Первый коммит называется корневой коммит (root kommit).  
Второй коммит ссылается на первый коммит. Для второго коммита первый коммит является родительским.  
Если у коммита несколько родительских коммитов - значит они были получены путём слияния веток.
___

__ВЕТКИ (BRANCH)__  
 При инициализации нового репозитория создаётся ветка master (main).  
 Ветка всегда ссылается на самый последний коммит в этой ветке.  
 Рекомендуется переименовать ветку "master" на "main".

 __СПИСОК ВЕТОК__  
 
    git branch

__СОЗДАТЬ НОВУЮ ВЕТКУ__  

    git branch [имя_ветки]

__СОЗДАТЬ НОВУЮ ВЕТКУ И ПЕРЕКЛЮЧИТЬСЯ НА НЕЁ__  

    git checkout -b [имя_ветки]

 __ПЕРЕКЛЮЧЕНИЕ МЕЖДУ ВЕТКАМИ__  
 
    git checkout [имя_ветки]

 __ПЕРЕИМЕНОВАТЬ ТЕКУЩУЮ ВЕТКУ__  
 
    git branch -m [новое_имя_ветки]  
 Сначала необходимо переключиться на ветку, которую хотим переименовать.

 __УДАЛИТЬ ВЕТКУ__  
 
    git branch -d [имя_ветки]

 Текущую ветку удалить нельзя!

__СЛИЯНИЕ ВЕТОК__  
У нас имеется две ветки: "main" и "FEATURE_BRANCH".  
Выполним слияние ветки "FEATURE_BRANCH" в ветку "main":  

    git merge FEATURE_BRANCH

Перед слиянием необходимо перейти в ту ветку, в которую будет выполняться слияние, в нашем случае в ветку "main".  

После слияния в ветке "main" добавится новый коммит с содержимым ветки "FEATURE_BRANCH".

И теперь мы можем удалить ветку "FEATURE_BRANCH".

__Merge commit__ - коммит, объединяющий две ветки
___

__HEAD__ - указатель на ветку, которая ссылается на коммит. Он ссылается на определённый коммит. В рабочей директории мы видим ту версию проекта, на который ссылается указатель HEAD.


__ПРОСМОТР ИСТОРИИ ИЗМЕНЕНИЙ (КОММИТОВ)__  

    git log

Просмотр истории коммитов в текущей ветке.

__ПРОЧИТАТЬ СОДЕРЖИМОЕ ОБЪЕКТОВ GIT__  

    git cat-file -t 73e319f5d250  
    git cat-file -p 73e319f5d250

- 73e319f5d250 - хеш коммита (первые символы)

___
__РАБОТА С УДАЛЁННЫМ РЕПОЗИТОРИЕМ__
___
__КЛОНИРОВАНИЕ УДАЛЁННОГО РЕПОЗИТОРИЯ В ЛОКАЛЬНЫЙ РЕПОЗИТОРИЙ__

    git clone [url]

При клонировании удалённого репозитория создаётся ORIGIN - имя удалённого репозитория по-умолчанию. И теперь мы можем с ним работать с помощью команд git push, git pull.

Отобразить все ветки, которые находятся в удалённых репозиториях:  

    git branch -a

Перейти в любую ветку, в том числе и ту, которая находится удалённо:  

    git checkout [branch name]
___

__СВЯЗЬ СУЩЕСТВУЮЩЕГО ЛОКАЛЬНОГО РЕПОЗИТОРИЯ С УДАЛЁННЫМ__  
1. Создаём удалённый репозиторий на гитхаб  
2. В локальном репозитории добавляем новый сервер:  

        git remote add origin [url]

3. Переименовываем нашу ветку в "main"  

        git branch -M main
4. Загрузить изменения из локальной ветки "main" в удалённую ветку "main" на сервер, который называется "origin":  

        git push -u origin main

Чтобы загружать изменения в удаленный репозиторий надо получить ACCESS TOKEN. Для этого авторизуемся на гитхабе, кликаем по своей иконке - SETTINGS - Developer Settings - Personal access token - генерируем новый токен и ставим галочку "repo"

Загрузка изменений из локальной ветки в удалённую с созданием связи между ними:  
    
    git push -u origin [branch]  

Когда ветки связаны мы загружаем или скачиваем обновления с помощью команд git push, git pull.

__УЗНАТЬ, СВЯЗАНА ЛИ ЛОКАЛЬНАЯ ВЕТКА С ВЕТКОЙ В УДАЛЁННОМ РЕПОЗИТОРИИ__  

    git branch -vv

__УЗНАТЬ, ПОДКЛЮЧЕН ЛИ НАШ РЕПОЗИТОРИЙ К УДАЛЁННОМУ СЕРВЕРУ__  

    git remote
___

__ЗАГРУЗИТЬ ИЗМЕНЕНИЯ из ЛОКАЛЬНОГО РЕПОЗИТОРИЯ на УДАЛЁННЫЙ РЕПОЗИТОРИЙ (GITHUB)__  

    git push

Это загрузка изменений из локальной ветки в ветку удаленного репозитория.

__ПОЛУЧИТЬ ИЗМЕНЕНИЯ ИЗ УДАЛЁННОГО РЕПОЗИТОРИЯ (GITHUB) на ЛОКАЛЬНЫЙ РЕПОЗИТОРИЙ__  

    git pull

Это загрузка и применение изменений с удалённой ветки в локальную.
___