# Git

## Содержание

* [Словарь](#словарь)
* [Введение в системы контроля версий. Git](#введение-в-системы-контроля-версий-git)
* [Первичная настройка Git](#первичная-настройка-git)
  * [Ваша учетная запись](#ваша-учетная-запись)
  * [Ваш текстовый редактор](#ваш-текстовый-редактор)
  * [Имя ветки, используемой по умолчанию](#имя-ветки-используемой-по-умолчанию)
* [Основы работы с Git](#основы-работы-с-git)
  * [Создание репозитория Git](#создание-репозитория-git)
  * [Настройка входа по SSH](#настройка-входа-по-ssh)
  * [Работа с файлами](#работа-с-файлами)
  * [Коммиты (Commits)](#коммиты-commits)
    * [Отслеживание новых файлов](#отслеживание-новых-файлов)
    * [Фиксация изменений (commit changes)](#фиксация-изменений-commit-changes)
    * [Отмена изменений](#отмена-изменений)
    * [Сохранение изменений при переключении на другую ветку (stash)](#сохранение-изменений-при-переключении-на-другую-ветку-stash)
  * [Как заставить Git игнорировать файлы в рабочей директории?](#как-заставить-git-игнорировать-файлы-в-рабочей-директории)
* [Работа с удаленными репозиториями](#работа-с-удаленными-репозиториями)
  * [Добавление удаленного репозитория (remote add)](#добавление-удаленного-репозитория-remote-add)
  * [Получение изменений из удалённого репозитория (fetch и pull)](#получение-изменений-из-удалённого-репозитория-fetch-и-pull)
  * [Отправка изменений в удалённый репозиторий (push)](#отправка-изменений-в-удалённый-репозиторий-push)
* [Немного о ветках](#немного-о-ветках)
  * [Слияние веток](#слияние-веток)
    * [Конфликт слияния](#конфликт-слияния-merge-conflict)
* [Теги(Tags)](#теги)
* [Разные проблемы](#разные-проблемы)
  * [Не работает .gitignore](#не-работает-gitignore)

**Система контроля версий** - это система, которая записывает изменения в файле или наборе файлов на протяжении определенного времени, чтобы впоследствии можно было восстановить конкретные версии.

![Git commands](https://github.com/ilsinyakov/QA_Theory/blob/main/Pictures/git.jpg)

## Словарь

**Коммит (commit, фиксация)** - это способ сохранения изменений в коде в системе Git. Это своего рода мгновенный снимок кода в определенный момент времени.  
**Ветвь (branch, бранч)** - это параллельная версия рабочего каталога ("базы кода"). Ее можно рассматривать как отдельную последовательность коммитов на временной шкале разработки кода. Например, dev, master, staging.  
**Слияние (Мёрдж, merge)** - это процесс объединения изменений из одной ветки в другую.  
**Репозиторий (repository)** - это структура данных, в которой хранится история версий проекта. Он служит центральным местом хранения всех файлов, каталогов и метаданных, связанных с проектом  
**Git база данных (git database)** - в Git под термином "база данных" обычно понимается структура данных (хранящаяся в каталоге .git), используемая для хранения истории версий и других метаданных репозитория Git. Однако важно отметить, что Git не использует традиционные базы данных (СУБД), такие как MySQL или PostgreSQL.  
**Указатель (pointer)** - это метка, которая позволяет отслеживать определенные элементы в истории проекта, такие как коммиты, ветки или теги, что облегчает навигацию и позволяет ссылаться на различные версии.  
**Рабочая директория (working directory)** - каталог на локальной машине, в который клонирован или инициализирован Git-репозиторий. Это каталог, в котором вы можете видеть и изменять реальные файлы и каталоги вашего проекта.  
**База кода (codebase)** - это подмножество рабочих каталогов. Каталог, содержащий вложенные каталоги и файлы, которые, в свою очередь, содержат код вашего приложения.

## Введение в системы контроля версий. Git

Системы контроля версий позволяют решить целый ряд проблем, связанных с управлением изменениями кода или любых других данных, изменяющихся во времени. Вот несколько примеров:

* **Отслеживание изменений**. Системы контроля версий позволяют отслеживать изменения в коде с течением времени, включая информацию о том, кто и когда внес каждое изменение. Это позволяет вести учет истории базы кода, что может быть полезно для понимания того, как она развивалась, и для отладки проблем.
* **Совместная работа**. Системы контроля версий позволяют нескольким людям одновременно работать над одним и тем же кодом, не отменяя изменений друг друга. Они также предоставляют инструменты для разрешения конфликтов в случае их возникновения.
* **Откаты и отмена изменений**. Системы контроля версий предоставляют возможность отката изменений к предыдущей версии базы кода. Это может быть полезно в тех случаях, когда изменения приводят к ошибкам или вызывают другие проблемы.
* **Рецензирование кода**. Системы контроля версий позволяют просматривать изменения кода до их слияния с основной базой. Это позволяет гарантировать соблюдение стандартов качества кода и хорошую прослеживаемость изменений.
* **Ветвление и слияние**. Системы контроля версий предоставляют инструменты для создания и управления ветвями базы кода, что может быть полезно для работы над новыми функциями или исправления ошибок без нарушения работы основной базы кода. Они также предоставляют средства для внесения изменений в основную базу после их завершения.
* **Устойчивость**. Ваш компьютер перестал работать, и вы потеряли всю свою работу за последний месяц. Этого не произойдет, если вы используете git.

**Git** - это распределенная система управления версиями, которая используется для отслеживания изменений в исходном коде программного обеспечения и управления ими.

Слово "распределённая" означает, что эта система находится сразу на нескольких рабочих машинах. Например, это могут быть облачные сервера и/или компьютеры ваших коллег.  
Репозиторий - это место, где хранятся  изменения.

![Git](https://github.com/ilsinyakov/QA_Theory/blob/main/Pictures/git.png)

С точки зрения концепции, Git рассматривает свои данные, которые хранятся в репозитории,  скорее как последовательность снимков собственной файловой системы. В Git каждый раз, когда вы фиксируете  изменения (делаете коммит; коммит означает сохранение состояния вашего проекта как снимка), Git по сути дела делает снимок того, как выглядят все ваши файлы в данный момент, и сохраняет ссылку на этот снимок. Для повышения эффективности, если файлы не изменились, Git не сохраняет файл снова, а только ссылку на предыдущий идентичный файл, который он уже сохранял. Git рассматривает свои данные скорее как последовательность снимков.  
Это важное различие между Git и практически всеми другими системами контроля версий.

### Git для инженеров-тестировщиков

Инженеры по тестированию могут использовать Git для совершенствования рабочего процесса и взаимодействия с другими членами команды. Вот несколько примеров:

1. **Ветвление**. Git предоставляет возможность ветвления, что позволяет QA-инженерам тестировать несколько ветвей базы кода, каждая из которых представляет собой отдельную версию приложения. Например, тестировщик может создать новую ветку для конкретной версии приложения, а затем провести тестирование в этой ветке, не затрагивая основную ветку. Это позволяет параллельно тестировать различные версии приложения и легко переключаться между ними по мере необходимости.
2. **Управление тест-кейсами**. Тестировщики могут использовать Git для хранения и отслеживания версий тест-кейсов, что упрощает отслеживание изменений и совместную работу с другими членами команды. Они могут создавать новую ветку для каждого набора тест-кейсов и при необходимости объединять изменения других членов команды. Это позволяет гарантировать, что все работают с одним и тем же набором тест-кейсов, а изменения отслеживаются и документируются.
3. **Контроль версий для тестовых данных**. Инженерам тестировщикам часто приходится использовать тестовые данные, такие как образцы входных файлов или ответы API. Git может использоваться для контроля версий этих данных, обеспечивая использование одной и той же версии, а также отслеживание и документирование изменений. Это может быть особенно полезно при работе с большими или сложными наборами данных.
4. **Непрерывная интеграция и непрерывное развертывание (Continuous Integration and Continuous Deployment CI/CD)**. Инженеры тестировщики могут использовать Git hooks для автоматического запуска тестов в тот момент, когда код в репозитории изменяется. После прохождения таких тестов этот код может быть внедрен тоже автоматически.

## Первичная настройка Git

Git поставляется с инструментом git config , который позволяет получать и устанавливать конфигурационные переменные, управляющие всеми аспектами внешнего вида и работы Git. Эти переменные могут храниться в трех различных местах:

* `[path]/etc/gitconfig` - содержит значения, применяемые к *каждому пользователю в системе* и ко всем его репозиториям. Если передать опцию `--system` в git config, то он будет читать и записывать именно из этого файла. Поскольку это системный конфигурационный файл, для внесения в него изменений требуются права администратора или суперпользователя.
* `~/.gitconfig` или `~/.config/git/config` - значения, характерные лично для вас, как *пользователя*. Вы можете заставить Git читать и писать в этот файл специально, передав опцию `--global`, и это повлияет на все репозитории, с которыми вы работаете в своей системе.
* `config (.git/config)` - файл конфигурации в каталоге Git (т.е. .git/config) того *хранилища*, которое вы используете в данный момент: специфичен для данного репозитория. Вы можете заставить Git читать из этого файла и писать в него с помощью опции `--local`, но на самом деле этот вариант используется по умолчанию. Неудивительно, что для корректной работы этой опции необходимо находиться где-то в репозитории Git.

Каждый уровень отменяет значения предыдущего уровня, поэтому значения в `.git/config` переопределяют значения в `[path]/etc/gitconfig`.

### Особенности настройки в WIndows

В системах Windows Git ищет файл .gitconfig в домашней директории ($HOME), для большинства пользователей это `C:\Users\$USER`. Он также ищет файл`[путь]/etc/gitconfig`, но это относится к корневой директории MSys, которая находится в том месте, где вы решите установить Git на Windows при запуске установщика. Если вы используете версию 2.x или более позднюю Git для Windows, также существует файл конфигурации на уровне системы, расположенный в`C:\Documents and Settings\All Users\Application Data\Git\config` в Windows XP и в `C:\ProgramData\Git\config` в Windows Vista и более новых версиях. Этот файл конфигурации может быть изменен только командой `git config -f path_to_file` в режиме администратора.

Вы можете просмотреть все свои настройки и то, откуда они взяты, используя:  
`$ git config --list --show-origin`

### Ваша учетная запись

Первое, что необходимо сделать при установке Git, - задать имя пользователя и адрес электронной почты. Это важно, так как при каждой фиксации изменений в Git'е используется эта информация, и она неизменно закладывается в создаваемые вами коммиты:  
`$ git config --global user.name "John Doe"`  
`$ git config --global user.email johndoe@example.com`

Это нужно сделать только один раз, если вы передали параметр --global, с этого момента Git всегда будет использовать эту информацию для всех ваших действий в этой системе. Если вы хотите переопределить имя или адрес электронной почты для определенных проектов, то можете выполнить команду без опции --global, когда находитесь в этом проекте.

### Ваш текстовый редактор

Теперь, когда персональные данные указаны, можно настроить текстовый редактор, который будет использоваться по умолчанию, когда Git потребует ввести сообщение. Если редактор не указан, Git использует редактор по умолчанию, установленный в вашей системе.

Если вы хотите использовать другой текстовый редактор, например, nano, вы можете сделать следующее:  
`$ git config --global core.editor nano`

В Windows, если вы хотите использовать другой текстовый редактор, необходимо указать полный путь к его исполняемому файлу.

### Имя ветки, используемой по умолчанию

По умолчанию при создании нового репозитория с помощью "git init" Git создает ветку с именем master. О том, что такое "ветка", рассказано далее. Начиная с версии Git 2.28, вы можете задать другое имя для начальной ветки.

Чтобы задать "main" в качестве имени ветки по умолчанию, выполните следующее:  
`$ git config --global init.defaultBranch main`

## Основы работы с Git

### Создание репозитория Git

Обычно Git-репозиторий можно создать одним из двух способов:

* **Инициализация** - позволяет создать локальный каталог, не относящийся к системе контроля версий, и преобразовать его в Git репозиторий. Идеально подходит, когда вы создаете новый проект с нуля или хотите начать управление версиями для существующего проекта, который ещё не использует Git.  
Вы запускаете этот процесс с помощью команды `git init` в корневом каталоге вашего проекта. После инициализации, вы можете добавлять файлы, фиксировать изменения и создавать ветки.
* **Клонирование** - применяется, когда вы хотите получить копию удаленного репозитория, который уже существует. Это может быть полезно, если вы присоединяетесь к существующему проекту или хотите начать работать с проектом, разработанным другими разработчиками.  
Вы выполняете клонирование с помощью команды `git clone`, указывая URL удаленного репозитория. После клонирования у вас будет локальная копия репозитория с историей изменений, ветками и всем содержимым.

Создание локального репозитория (инициализация):  
`git init`  
Создать связь локального репозитория с удаленным репозиторием:  
`git remote add origin <адрес удаленного репозитория>`  
Удалить связь:  
`git remote rm origin`

Клонирование репозитория с использованием git clone:

* По SSH (рекомендуется)  
`$ git clone git@github.com:[your-account-name]/[repo-name].git demo`
* По HTTPS  
`$ git clone https://github.com/[your-account-name]/[repo-name]/.git demo`

demo - это имя каталога, в который будет скопирован весь репозиторий после выполнения одной из приведенных выше команд.
В случае если имя каталога не указано, git создаст/использует пустой каталог с именем репозитория из URL (demo-git) ИЛИ выдаст ошибку, если каталог уже существует и он не является пустым.

### Настройка входа по SSH

#### Bash

`ssh-keygen -t ed25519 -C "your_email@example.com"` - создаем пару SSH ключей. Указываем полный путь для сохранения.  
`ssh-keygen -t rsa -b 4096 -C "your_email@example.com"` - если не работает.  

`eval "$(ssh-agent -s)"` - запускаем SSH агент в фоне.

`ssh-add ~/.ssh/<путь к private key файлу>` - добавляем приватный ключ в систему

Для того, чтобы сертификат подгружался каждый раз при запуске терминала, добавить в .bashrc:  

```bash
# Автозапуск ssh-agent
env=~/.ssh/agent.env

agent_load_env () { 
    test -f "$env" && . "$env" >| /dev/null 
    # Проверяем, что переменные существуют
    if [ -n "$SSH_AGENT_PID" ] && ps -p "$SSH_AGENT_PID" > /dev/null; then
        export SSH_AUTH_SOCK
        export SSH_AGENT_PID
    else
        return 1
    fi
}

agent_start () {
    (umask 077; ssh-agent >| "$env")
    . "$env" >| /dev/null ;
    ssh-add ~/.ssh/git_lab  # Путь к вашему ключу
}

agent_load_env
if ! ps -p "$SSH_AGENT_PID" > /dev/null; then
    agent_start
fi
```

Проверить, что файл ~/.ssh/agent.env создается. Если нет - создать вручную:  
 `(umask 077; ssh-agent >| ~/.ssh/agent.env)`

#### PowerShell

`Start-Service ssh-agent`  
`Set-Service ssh-agent -StartupType Automatic`  
`ssh-add $env:USERPROFILE\.ssh\<путь к private key файлу>`

Прописываем публичный ключ в профиле на Github.

### Работа с файлами

Git имеет три основных состояния, в которых могут находиться файлы:

* **Измененное (modified)** - файл был изменен, но еще не зафиксирован в базе данных Git.
* **Индексированное  или промежуточное (staged)** - означает, что вы пометили измененный файл в его текущей версии для включения в следующий снимок (commit).
* **Зафиксированное  (committed)** - данные надежно сохранены в локальной базе данных.

Это приводит нас к трём основным разделам проекта в Git: рабочая директория (Working tree, Working Directory), область промежуточного состояния (Staging area) и Git-каталог (Git directory).

![Git stage](https://github.com/ilsinyakov/QA_Theory/blob/main/Pictures/git_stage.png)

**Рабочая директория** - это  единичный снимок (checkout) одной версии проекта. Эти файлы извлекаются из сжатой базы данных в каталоге Git и помещаются на диск, чтобы их можно было использовать или изменять.

**Область промежуточного состояния (Staging area)** - это файл, обычно содержащийся в каталоге Git (.git), в котором хранится информация о том, что войдет в следующий снимок (commit). Техническое название этого файла на языке Git - "индекс", однако словосочетание "область промежуточного состояния" подходит лучше.

**Git-каталог (Git directory) (.git)** - это место, где Git хранит метаданные и базу данных объектов проекта. Это наиболее важная часть Git'а, и именно она копируется при клонировании репозитория с другого компьютера.

Основной рабочий процесс Git выглядит примерно так:

1. Вы изменяете файлы в своем рабочем каталоге.
2. Вы выбираете только те изменения, которые хотите включить в следующий коммит, который добавляет только эти изменения в область staging.
3. Вы выполняете коммит (фиксацию), в результате которой файлы сохраняются в том виде, в котором они находятся в области постановки, и этот снимок навсегда сохраняется в вашем каталоге Git.

Если конкретная версия файла находится в каталоге Git, она считается зафиксированной (**committed**). Если она была изменена и добавлена в область постановки, то она считается установленной (**staged**). Если же он был изменен с момента последнего, но не был помещен в область хранения, то он считается модифицированным (**modified**).

### Коммиты (Commits)

Помните, что каждый файл в рабочем каталоге может находиться в одном из двух состояний: отслеживаемом (**tracked**) или неотслеживаемом (**untracked**).

**Отслеживаемые файлы** - это файлы, которые были в последнем снимке, а также все недавно помещенные файлы; они могут быть *неизмененными (unmodified*), *измененными (modified*) или *размещенными (staged*).  
Другими словами, отслеживаемые файлы - это файлы, о которых Git знает.

**Неотслеживаемые файлы** - это все остальное, любые файлы в рабочем каталоге, которых не было в последнем снимке и которые не находятся в области промежуточного состояния (staged area).

Когда вы впервые клонируете репозиторий, все ваши файлы будут иметь состояние "отслеживаемые" и "неизмененные" поскольку Git только что проверил их, и вы ничего не редактировали.

Когда вы редактируете файлы, Git видит их как изменённые, поскольку вы изменили их с момента последнего коммита. В процессе работы вы выборочно устанавливаете эти измененные файлы, а затем фиксируете все эти установленные изменения, и цикл повторяется.

![modifying files](https://github.com/ilsinyakov/QA_Theory/blob/main/Pictures/modifing_files.png)

#### Отслеживание новых файлов

Для отслеживания уже созданного файла:  
`git add <имя файла>`  
Файл добавляется в область промежуточного состояния (staged area).

`git diff` - показывает изменения, внесенные в файлы (до добавления в staged area)

#### Фиксация изменений (commit changes)

`git commit -m "<Сообщение>"`

Флаг -m задает сообщение для коммита. Это сообщение позволяет другим пользователям получить немного больше информации о  зафиксированных изменениях.

После коммита изменений файл README становится *отслеживаемым немодифицированным (unmodified)*.

`git commit -a -m "<Сообщение>"` - добавляет отслеживаемые измененные файлы в область промежуточного состояния и делает коммит. (Не нужно использовать git add)

В разделе `git log` отображаются изменения, которые были сделаны на данный момент.

Подробнее о том, как использовать git log, можно прочитать в [учебнике по Git](https://git-scm.com/book/ru/v2/Основы-Git-Просмотр-истории-коммитов).

С помощью команд git можно не только добавлять файлы в базу данных git, но также удалять и перемещать. Вы также можете отменять действия и исправлять сообщения о коммитах. Подробнее об этом читайте в учебнике по Git, в разделах [Запись изменений в репозиторий](https://git-scm.com/book/ru/v2/Основы-Git-Запись-изменений-в-репозиторий) и [Операции отмены](https://git-scm.com/book/ru/v2/Основы-Git-Операции-отмены).

#### Отмена изменений

`git rm <file>` - удаление файла с одновременной подготовкой к коммиту (не нужно делать git add).

Отмена добавления файлов в область промежуточного состояния (staged area):  
`git restore --staged <file>`

`git checkout <file>` - возврат состояния файлов к последнему коммиту (до того, как они добавлены в staged area)

Откат состояния файла к определенному коммиту с сохранением в истории инфы об откате:  
`git restore --source=<commit_hash> <file>`

`git reset --hard HEAD` - приводит файлы к состоянию, на которое указывает HEAD. На месте HEAD может быть любой коммит.  
`--hard` - приводит к потере информации. Файлы изменяются. Использовать осторожно.  
`--soft` - откатывается только commit. Сами файлы не меняются.  
-без ключей - откатывается commit и add. Сами файлы не меняются.

#### Сохранение изменений при переключении на другую ветку (stash)

```sh
git stash        # Сохраните изменения во временный стек
git checkout new-branch-name  # Переключитесь на новую ветку
git stash pop    # Верните сохранённые изменения
git add .
git commit -m "Ваш коммит"
```

### Как заставить Git игнорировать файлы в рабочей директории?

Файл `.gitignore` - это конфигурационный файл, используемый в Git'е для указания файлов и каталогов, которые не должны отслеживаться системой контроля версий. Он позволяет исключить коммит определенных файлов или шаблонов или отображение их в качестве неотслеживаемых файлов в репозитории Git.

Файл .gitignore может использоваться в следующих случаях:

* **Игнорирование временных или кэш-файлов**. Некоторые файлы, создаваемые редакторами кода, такие как временные файлы, файлы кэша или файлы автосохранения, могут загромождать репозиторий и не имеют смысла для контроля версий. Файл .gitignore может быть использован для исключения таких файлов и поддержания чистоты репозитория.
* **Игнорирование конфигурационных файлов**. Проекты часто содержат файлы, содержащие конфиденциальную или специфическую для среды информацию, например ключи API или учетные данные баз данных. Файл .gitignore позволяет исключить эти файлы из системы контроля версий, чтобы исключить их случайный коммит и последующий публичный доступ. Добавление файлов, содержащих конфиденциальную информацию, в Git-репозиторий считается нежелательной практикой.
* **Игнорирование артефактов сборки**. При разработке программного обеспечения в процессе сборки проекта часто автоматически создаются файлы, которые не являются необходимыми для проекта и могут быть проигнорированы, например отчеты или журналы сборки.
* **Игнорирование личных предпочтений**. Некоторые разработчики имеют личные предпочтения в отношении редакторов, таких как Vim или Emacs, и у них могут быть определенные файлы или каталоги, которые можно игнорировать с помощью файла .gitignore, чтобы избежать ненужного контроля версий.

Файл .gitignore поддерживает использование шаблонов и спецсимволов для определения того, что должно быть проигнорировано. Он может быть размещен в корневом каталоге репозитория Git или в определенных подкаталогах для применения правил игнорирования на разных уровнях.

Использование файла .gitignore позволяет вести более упорядоченную историю контроля версий, предотвращать излишнее нагромождение информации, а также гарантировать, что файлы, содержащие конфиденциальные данные,  или временные файлы не будут опубликованы или зафиксированы в репозитории.

Ниже приведены примеры записей, которые можно найти в файле .gitignore:  

Исключение конкретного файла  
`myfile.txt` - Эта запись игнорирует файл с именем "myfile.txt" в репозитории

Исключить определенную директорию  
`mydirectory/` - Эта запись игнорирует каталог с именем "mydirectory" и все его содержимое

Игнорировать файлы на основе шаблонов  
`/docs/*.pdf`  
`!/docs/important.pdf` - Эта запись игнорирует все PDF-файлы в каталоге "docs", кроме "important.pdf"

Игнорировать файлы или каталоги рекурсивно  
`logs/`  
`tmp/` - Эта запись позволяет рекурсивно игнорировать каталог "logs" и каталог "tmp", а также все их содержимое. Игнорируемые файлы и папки будут исключены из обработки на всех уровнях вложенности

## Работа с удаленными репозиториями

`git remote` - Команда выводит список удаленных репозиториев.

Если вы клонировали свой репозиторий, то можете увидеть *origin*  - это имя, которое Git по умолчанию присваивает серверу, с которого выполнялось клонирование.

### Добавление удаленного репозитория (remote add)

Если удаленного репозитория еще нет, то его можно добавить:  
`git remote add origin https://gitlab.com/USERNAME/my-repo.git`

Если нужно переименовать текущую ветку (например из `master` в `main`):  
`git branch -M main`

Отправить локальную ветку в удаленный репозиторий:  
`git push -u origin main`

`-u` - это эквивалент `--set-upstream` - эта опция при первом пуше устанавливает «upstream-ветку» для вашей локальной ветки. Это значит, что в будущем вам не придётся каждый раз указывать ни имя удалённого репозитория, ни имя ветки.

### Получение изменений из удалённого репозитория (fetch и pull)

Чтобы получить данные из удалённого репозитория "origin", можно выполнить команду:  
`git fetch origin main`  
С помощью этой команды можно обратиться к удаленному проекту и извлечь из него все данные, которых еще нет в текущем репозитории (например, изменения файлов и каталогов вашими коллегами). Важно отметить, что команда `git fetch` только **загружает** данные в ваш локальный репозиторий. Она **не изменяет** то, над чем вы работаете в данный момент.

`git merge origin/main` - слить полученные изменения с локальным репозиторием.

Для того, чтобы получить все изменения из удаленного репозитория вам необходимо выполнить следующую команду:  
`git pull origin main`  
по сути эта команда выполняет то же, что `fetch + merge`

### Отправка изменений в удалённый репозиторий (push)

Когда ваш проект достигает той стадии, на которой вы хотите им поделиться, необходимо выполнить операцию синхронизации с удаленным репозиторием.  Для этого необходимо выполнить следующую команду:  
`git push <remote> <branch>`

Если вы хотите перенести изменения в удаленный репозиторий (как правило, при клонировании она настраивается автоматически ), то вы можете выполнить эту команду, чтобы отправить все сделанные вами коммиты на сервер:  
`git push origin main`

Эта команда работает только в том случае, если вы клонировали с сервера, к которому у вас есть доступ на запись, и если за это время никто не выполнял push.

## Немного о ветках

![branch](https://github.com/ilsinyakov/QA_Theory/blob/main/Pictures/branch.png)

**Ветка (branch)** - это последовательность коммитов (commits). Каждый следующий коммит  имеет ссылку на своего родителя (предшественника) и таким образом образуется их последовательность, составляющая ветку (branch).  Главное преимущество веток заключается в том, что они позволяют вам работать над разными задачами параллельно, не затрагивая основную линию разработки.

Давайте представим, что ваш проект - это дерево. Основная ветка, которая создается по умолчанию и называется обычно main или master, представляет собой ствол этого дерева. Когда вы создаете новую ветку, вы создаете новую "ветку" в дереве, которая начинается от определенной точки на стволе. Вы можете назвать эту ветку, например, feature-branch или bug-fix-branch, чтобы отражать её назначение.

Затем вы можете свободно вносить изменения в файлы в этой ветке, фиксировать их в коммитах и даже создавать другие ветки от вашей текущей ветки. Это позволяет удобно организовывать и управлять рабочим процессом. Когда ваша работа в ветке завершена, вы можете влить изменения обратно в основную ветку, что называется **слиянием (merge)**.

`git branch` - список веток

`git branch <имя новой ветки>` - создание ветки

`git checkout -b <имя новой ветки>` - создание ветки c одновременным переключением на нее

`git checkout <имя ветки>` - переключение на другую ветку.  
Если переключиться на другую ветку без коммита, то файлы в другой ветке будут также перенесены с изменениями.

`git branch -d <удаляемая ветка>` - удалить ненужную ветку. Если изменения из ветки не слиты, то удалить ее так нельзя. Также нельзя удалить ветку, на которой мы находимся в данный момент.

 `git branch -D <удаляемая ветка>` - удалить принудительно.

### Слияние веток

Слияние в ветку main:  
`git checkout main` - переключаемся на ветку main  
`git merge <сливаемая ветка>` - сливаем ветку в main

#### Конфликт слияния (Merge conflict)

`git merge --abort` - отменить слияние

 В случае конфликта, нужно вручную поправить конфликтующие файлы и сделать коммит:  
`git commit -m "Fix merge conflict"`

## Теги

`git tag <new_tag>` - создает тег на текущем коммите

`git tag` - выводит список существующих тегов

`git push origin --tags` - отправить теги из локального репозитория в удаленный

`git reset <new_tag>` - вернуть репозиторий к состоянию, отмеченному тегом

## Разные проблемы

### Не работает .gitignore

Если, например, в VSCode не работает .gitignore, имеет смысл очистить кеш гита.  
`git rm -r --cached .` - очищаем кеш

`git add .` - фиксируем изменения в стейдж

`git commit -m ".gitignore is now working"` - делаем коммит
