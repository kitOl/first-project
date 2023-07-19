# Шпаргалка. Базовые команды в консоли

## Навигация

**pwd** (от англ. *print working directory*, «показать рабочую папку») — показать, в какой я папке;  
**ls** (от англ. *list directory contents*, «отобразить содержимое директории») — показать файлы и папки в текущей папке;  
**ls -a** — показать также скрытые файлы и папки, названия которых начинаются с символа ```.```;
**cd first-project** (от англ. *change directory*, «сменить директорию») — перейти в папку **first-project**;  
**cd first-project/html** — перейти в папку **html**, которая находится в папке **first-project**;
**cd ..** — перейти на уровень выше, в родительскую папку;  
**cd ~** — перейти в домашнюю директорию (__ /Users/Username __);  
**cd /** — перейти в корневую директорию.

## Работа с файлами и папками

### Создание

**touch index.html** (англ. *touch*, «коснуться») — создать файл **index.html** в текущей папке;  
**touch index.html style.css script.js** — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;  
**mkdir second-project** (от англ. *make directory*, «создать директорию») — создать папку с именем **second-project** в текущей папке.

### Копирование и перемещение 

**cp file.txt ~/my-dir** (от англ. *copy*, «копировать») — копирует файл в другое место;  
**mv file.txt ~/my-dir** (от англ. *move*, «переместить») — переместить файл или папку в другое место.

### Переименование

Чтообы переименовать файл, используем команду перемещения:
```
mv "old location" "new location"

mv /home/user/my_static /home/user/static # пример

```

Гораздо больше возможностей предоставляет специальная команда переименования

```
rename [опции] 's/старое_имя/новое_имя' файлы

Или

rename [опции] старое_имя новое_имя файлы

```
**опции утилиты:**
* **-v** - вывести список обработанных файлов;  
* **-n** - тестовый режим, на самом деле никакие действия выполнены не будут;  
* **-f** - принудительно перезаписывать существующие файлы

Например, переименуем все htm файлы из текущей папки в .html:
```
 rename 's\.htm/\.html/' *.htm
```

### Чтение

**cat file.txt** (от англ. *concatenate and print*, «объединить и распечатать») — распечатай содержимое текстового файла **file.txt**.

### Удаление

**rm about.html** (от англ. *remove*, «удалить») — удалить файл about.html;  
**rmdir images** (от англ. *remove directory*, «удалить директорию») — удалить папку **images**;  
**rm -r second-project** (от англ. *remove*, «удалить» + *recursive*, «рекурсивный») — удалить папку **second-project** и всё, что она содержит.

### Полезные возможности
Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами (&&).

У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх **(↑)** и вниз **(↓)**.

Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать **Tab**. Если файл или папка есть в текущей директории, командная строка допишет путь сама.

Например, вы находитесь в папке ```dev```. Начните вводить ```cd first``` и дважды нажмите **Tab**. Если папка ```first-project``` есть внутри ```dev```, командная строка автоматически подставит её имя. Останется только нажать **Enter**.


# Что такое Git и зачем он нужен

**Git** — это система контроля версий, которая помогает отслеживать изменения в проекте. Этот инструмент можно использовать как для индивидуальной, так и для командной работы.
**Git** позволяет сохранять изменения локально и при необходимости возвращаться к предыдущим версиям проекта. Также можно создать удалённую копию на хостинг-платформе, которая работает с **Git**, и поделиться результатом с другими.

## Установка GitBash 

На официальном сайте скачивается файл инсталляции, который запускаем после.

## Работа с файлом настройки **.gitconfig**

Пока работаем в одиночку, но в дальнейшем может понадобиться использовать Git в команде. Чтобы участникам проекта было понятно, кто и какие изменения вносил, нужно представиться и указать имя пользователя и адрес электронной почты.
```
git config --global user.name "User Namovich" 
# имя или ник нужно написать латиницей и в кавычках

git config --global user.email username@yandex.ru
# здесь нужно указать свой настоящий email
```
Все глобальные настройки Git хранит в файле **.gitconfig** в домашней директории. Убедимся в этом:
```
cat ~/.gitconfig
```


# Инициализируем репозиторий
## Сделать папку репозиторием - ```git init```

Чтобы Git начал отслеживать изменения в проекте, папку с файлами этого проекта нужно сделать Git-репозиторием. Для этого следует переместиться в эту директорию и ввести команду
```
git init
```
Создадим в домашней директории папку с нашими проектами и в ней - папку нашего первого проекта:
```
mkdir ~/dev
mkdir ~/dev/first-project
cd dev/first-project
git init
```
**Совет:** *cтрочки кода можно объединить в одну:* 
```
mkdir ~/dev ~/dev/first-project && cd dev/first-project && git init
```

В результате на локальном компьютере будет создан репозиторий Git, в корне папке проекта создается скрытая системная папка ```.git```, в которой хранится служебная информация, необходимая для отслеживания изменений в проекте.


Если инициализация репозитория по-ошибке была сделана не в той директории, можно текущую директорию разгитить - достаточно просто удалить скрытую папку ```.git```:

```
$ cd <папка с репозиторием> # перешли в папку

$ rm -rf .git # удалили подпапку .git
```

**Важно:** *репозитории не должны быть вложенными!*


После инициализации репозитория проверим статус его:
```
git status
```
Команда git status выведет:
* название текущей ветки: ```On branch master``` или ```On branch main```;
* сообщение о том, что в репозитории ещё нет коммитов: ```No commits yet```;
* сообщение, которое говорит: «чтобы что-нибудь закоммитить (то есть зафиксировать), нужно сначала это создать» — ```nothing to commit (create/copy files and use "git add" to track)```

Теперь создадим наш первый файл проекта README.md и внесем в него изменения:
```
touch README.md
notepad README.md
```
Откроется программа Блокнот, где введем первые строки. Сохраним изменения и закроем файл.

**Совет:** *новый файл можно было создать одной командой вызова Блокнота - программа сообщит, что такого файла не существует и спросит "создать этот файл"?*

Если теперь снова запросить у Git статус, то программа сообщит, что в проекте есть ```untracked``` файл ```README.md```. 
Подготовим этот файл к сохранению в репозитории:

```
git add .
```
- подготовили всю папку. Или
```
git add --all
```
- будут отслежены все изменения всех файлов. 
Если же отслеживать нужно только один файл, то используем команду:
```
git add <filename>
```

# Делаем первый коммит

Коммит — это одна из основных сущностей в Git (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». 

```
git commit -m "Мой первый коммит!"
```

Команда выведет информацию о коммите.

**Просмотреть историю коммитов —** ```git log```

# GitHub

Сейчас используем **Git** *локально*: проект **first-project** хранится только на компьютере. Но одно из ключевых преимуществ **Git** — удобство командной работы над файлами. Чтобы поделиться репозиторием — например, с коллегами, — нужно завести его удалённую версию. 

Процесс командной работы может выглядеть так: работаета над файлами проекта, например пишется код, на персональном компьютере и сохраняется в локальном репозитории. Как только накапливается достаточно правок, чтобы поделиться ими с остальными, они передаются на удалённый репозиторий. Там коллеги смогут посмотреть то, что получилось, и даже скачать себе на компьютер.

Есть несколько платформ для такой командной работы. Самая популярная — **GitHub**

**GitHub** подходит, чтобы отточить навыки работы с **Git**. Здесь можно завести аккаунт и вместе со своей командой работать над любыми задачами. Можно создавать проекты разных типов:

* **приватный** — только для вас;
* **командный** — только для членов команды;
* **публичный** — будет виден всем.

Также можно присоединиться к чужому open source проекту и работать над ним вместе с другими людьми со всего мира. 

* **GitHub** — платформа, которая работает с Git и упрощает командное взаимодействие.
* Кроме **GitHub**, существуют и другие подобные платформы, например **GitLab, Bitbucket** и так далее.
* **Git** — это консольный инструмент для работы с локальными и удалёнными репозиториями. Он не связан напрямую ни с одной из платформ и развивается отдельно от них.

# Регистрация на GitHub

Для работы с **GitHub** сначала надо зарегистрироваться на [GitHub](https://github.com). Для этого кликнем на ```Sign up``` и пройдем процедуру регистрации - укажем свой мейл, логин и пароль.

## Создание репозитория на GitHub

После регистрации и авторизации на сайте переходим на вкладку **Repositories** (она пока пуста), нажимае кнопку ```New``` и указываем имя нашего проекта *first-project*. Больше никаких других настроек на данном этапе нам не потребуется.

Репозиторий удаленный создан. Но для безопасной работы с ним нам прежде нужно сгенерировать и подключить SSH-ключ.

# Что такое SSH
Когда компьютеры обмениваются данными в сети, они следуют сетевым протоколам (англ. network protocols) — правилам обмена данными между компьютерами.
Один из наиболее распространённых сетевых протоколов — **SSH** (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.

SSH использует пару ключей для обеспечения безопасности — публичный и приватный: 

1. **Приватный ключ** (англ. private key) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для шифрования данных.
2. **Публичный ключ** (англ. public key) доступен всем и используется для расшифровки данных, которые были зашифрованы приватным ключом. 

# Проверка наличия SSH-ключа

Прежде чем генерировать SSH-ключи, убедитесь, что у вас их ещё нет. По умолчанию директория с SSH-ключами находится в домашней директории пользователя.  
Обычно SSH-ключи находятся в директории .ssh/. Проверить наличие этой директории и файлов в ней можно с помощью следующей команды.
```
$ ls -la ~/.ssh/ # вывели список созданных ключей 
```

Если папка пустая или её нет, всё в порядке. 

## Генерация SSH-ключа
```
$ ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"
```
Будет предложено сохранить пару ключей в Домашней директории:
```
> Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter]
```
Также программа запросит кодовую фразу к ключу. На данном этапе в этом нет необходимости, оставим поле пустым.

Проверим, что ключи созданы:
```
ls -a ~/.ssh
или
ls -la ~/.ssh
```
Получим два файла id_ed25519, один из них - с раширением ```.pub``` - этот ключ мы и будем использовать для связи с удаленным репозиторием.
**Важно!** *Ключ без расширения никому нельзя передавать!*

# Привязываем SSH-ключ к GitHub

Наш ключ пока не привязан к аккаунту. Чтобы сделать эту привязку, копируем в буфер обмена **публичный** ключ:
```
clip < ~/.ssh/id_ed25519.pub
или
cat ~/.ssh/id_ed25519.pub # далее выделяем мышкой и копируем
или
notepad ~/.ssh/id_ed25519.pub # выделяем и копируем в буфер обмена
```

Дадее переходим на **GitHub** и выбираем пункт **Settings** в меню в правой части экрана.
Слева появится меню, в котором выбираем **SSH and GPG keys**.
В открывшейся вкладке выбираем **New SSH key**, 
в поле **Title** называем ключ **Personal key**, 
в поле **Key type** должно быть **Authentication Key**,
в поле **Key** вставляем из буфера обмена наш ключ.

Нажимаем **Add SSH key**.

Проверим правильность ключа командой:
```
ssh -T git@github.com
```

При первом использовании ресурсом появится предупреждение, что нужно проверить ключ SHA256 сервера.

Проверяем ключ сервера по [ссылке](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/githubs-ssh-key-fingerprints)

# Связываем локальный и удалённый репозитории

Переходим на страницу удалённого репозитория, выбераем тип **SSH** и копируем **URL**.

Открываем Консоль, переходим в папку проекта и связываем репозитории:
```
cd ~/dev/first-project
git remote add origin git@github.com:%ИМЯ_АККАУНТА%/first-project.git
```
**origin** — стандартный псевдоним, с помощью которого можно обращаться к главному удалённому репозиторию (обычно такой репозиторий один). Это значительно упрощает работу.

**Совет:** *Как выполнить вставку в командную строку?*

В командную строку нельзя вставить текст из буфера обмена с помощью привычного сочетания **Ctrl+V**.
На **Windows (в Git Bash) и Linux** для этого используется сочетание **Ctrl+Shift+V**, 
а на **macOS** — **Cmd+V**.
Также можно нажать правую кнопку мыши и выбрать пункт **Paste** (англ. «вставить») в выпадающем меню.


## Убедимся, что репозитории связаны
```
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)
```
# Синхронизируем локальный и удалённый репозитории

## Основная ветка
Каждый коммит сохраняет актуальное состояние файлов. Сами же коммиты хранятся в ветках (англ. **branch**).
Если *коммит* — это снимок состояния файлов, то *ветка* — временна́я шкала, на которой расположены эти снимки. Ветка всегда начинается от одного из коммитов.
В репозитории может существовать сразу несколько веток — параллельных историй изменений. Также они могут соединяться друг с другом.

Самая первая ветка в репозитории появляется автоматически и называется **main** (англ. «основная») или **master**. Её имя нужно указывать при отправке коммитов на удалённый репозиторий или при получении их из него.

## Отправить изменения на удалённый репозиторий

Уже прошли весь «цикл коммита»: подготовили файлы с помощью **git add**, закоммитили их с комментарием командой **git commit -m**. Осталось загрузить содержимое локального репозитория на GitHub. За это отвечает команда **git push**.

**В первый раз** эту команду нужно вызвать с флагом **-u** и параметрами **origin** (имя удалённого репозитория) и **main** или **master** (название текущей ветки). 
```
git push -u origin main # Если команда приведёт к ошибке, попробуйте 
                          # заменить main на master.
```
Если при настройке SSH-ключей была указана кодовая фраза, её нужно будет ввести.

После успешной синхронизации заходим на GitHub. В репозитории проекта должны появиться файлы с изменениями.

Дальнейшая синхронизация производится без параметров:
```
git push
```

## Графический интерфейс GitHub

Предоставляет множество инструментов для удобной работы: просмотр коммитов, кода и проч.

# Файл README.md
Чтобы другие пользователи, а также потенциальные клиенты или работодатели могли понять, что представляет собой проект, его нужно описать. Такое описание принято указывать в файле README.md

Как правило, в README.md проекта можно найти следующую информацию:
1. Название проекта и его краткое описание: кем создан, для чего, какие решает задачи и какие закрывает проблемы.
2. Технологии, которые применяются в проекте. В чём его отличие от аналогичных.
3. Документация проекта — подробная инструкция о том, что представляет собой проект.
4. Планы проекта, если они есть.

## Как создать и оформить README.md

**README.md** — текстовый файл, который можно создать командой touch, а затем редактировать так же, как и любой другой текстовый документ. Например, в блокноте.
Преимущество **README.md** в том, что средства командной работы (такие, как GitHub) могут отображать его содержимое в браузере в виде удобной разметки. Для этого нужно не просто залить текст, но и настроить шрифт, заголовки и отступы с помощью **markdown**. **Маркда́ун** — это специальный язык разметки. Он позволяет красиво отформатировать текстовый документ.

# Шпаргалка markdown

## Выделение текста

Можно выделять текст в markdown с помощью символов `_` или `*`. Например:

Курсив — это ```*звёздочки*``` *звёздочки* или ```_подчёркивания_``` _подчёркивания_.

Пример _курсива_ и **жирного** текста.

Полужирный шрифт — двойные ```**звёздочки**``` **звёздочки** или двойные ```__подчёркивания__``` __подчёркивания__.
Можно совместить выделение **звёздочки и _подчёркивания_**.

```~~Зачёркнутый текст.~~``` ~~Зачёркнутый текст.~~

## Заголовки

Заголовки можно создавать с помощью символа `#`. Чем больше `#`, тем меньше заголовок. Например:

# Заголовок первого уровня
## Заголовок второго уровня
### Заголовок третьего уровня

## Списки

### нумерованные
Для оформления нумерованного списка достаточно поставить в начало строки цифры с точкой.

1. Первый пункт нумерованного списка.
2. Второй пункт.

### ненумерованный список
создаётся звёздочкой с пробелом в начале строки либо дефисом с пробелом.

```- первый пункт ненумерованного списка;```
* первый пункт ненумерованного списка;
```* второй пункт ненумерованного списка```
- второй пункт ненумерованного списка

## список задач

создается дефисом с пробелом, далее квадратные скобки с пробелом, символ ```x``` 
вместо пробела помечает решенную задачу:

```
- [x] 1: issue 1
- [ ] 2: issue 2
- [ ] 3: issue 3
```
- [ ] 1: задача 1
- [ ] 2: задача 2
- [x] 3: задача 3


## Разбивка текста

### Разрыв строки

Чтобы сделать разрыв строки, нужно поставить два пробела (в примере ниже они обозначены точками ⋅⋅) или сочетание символов ```<br>```:

Текст до переноса⋅⋅  
Текст после переноса <br>
Текст после второго переноса

### Новый параграф (абзац)

Чтобы начать новый параграф, в конце предыдущей строки должно стоять два символа переноса. Для этого нужно нажать Enter два раза.

line

another line 

Если сделать один перенос строки, как в примере ниже, и не поставить два пробела, текст сольётся в одну строку:

```markdown
line 

another line

```


## Выделение кода

Чтобы выделить текст как код, поместите его в тройные обратные кавычки (грависы) `````. После первой тройки указывается язык программирования, на котором написан код (необязательно).

```
mkdir my_project
cd my_project
git init
```
А теперь немного HTML:

```html
<h1>А я просто текст</h1>
```

Чтобы сделать ссылкой часть текста, его заключают в квадратные скобки, а затем указывают нужный адрес в круглых скобках:

[Яндекс](https://www.yandex.ru "Я Yandex!")

Это лишь некоторые функции markdown.

# Git status

## HEAD файл

При выолнение команды ```git log``` коммиты отображаются в обратном порядке - первым идет самый последний коммит. И в поле хэш-кода отображается запись ```(HEAD -> master)```. 
Файл HEAD - один из служебных файлов папки **.git**. Он указывает на коммит, который сделан последним. Его содержимое простое (прочитаем командой **cat**)
```
$ cat ~/dev/first-project/.git/HEAD
ref: refs/heads/master # ссылка на другой служебный файл, содержащий хэш последнего коммита
```
Многие команды Git принимают в качестве параметра хеш коммита. Если нужно передать последний коммит, то вместо его хеша можно просто написать ```HEAD```.

# Статусы файлов в Git

Всего различают четыре статуса: **untracked / tracked, staged и modified**.

1. **untracked** - так помечаются новые файлы проекта
2. **staged** - этот статус получают новые файлы проекта и измененные файлы после выполнения команды ```git add```.
3. **tracked** - файл отслеживается. Сюда относятся файлы после команд ```git commite и git add```
4. **modified** - Git сравнил содержимое файла с последней сохраненной версией и обнаружил изменения.

## Про **staged** и **modified**

Команда ```git add``` добавляет в *staging area* только текущее содержимое файла. Если, например, сделать ```git add file.txt```, а затем измените **file.txt**, то новое содержимое файла не будет находиться в **staging**.
**Git** сообщит об этом с помощью статуса **modified**: файл изменён относительно той версии, которая уже в **staging**. Чтобы добавить в **staging** последнюю версию, нужно выполнить ```git add file.txt``` ещё раз.

# Как читать *git status*

Частая ошибка при использовании Git — закоммитить лишнее или, наоборот, забыть добавить важный файл в коммит. Этого легко избежать, если не забывать проверять статусы файлов с помощью команды ```git status```.

## Исследуем *git status*

Создадим новый проект по исследованию *git status*, а в нем - файл README.md
```
mkdir ~/dev/git-status-lesson
cd ~/dev/git-status-lesson	# перешли в директорию нового проекта
git init	# инициализация git
touch README.md	# создали новый файл README.md
			# его статус **untracked**
git add README.md # добавили наш файл в отслеживание
			# теперь его статус **staged**
git commit -m 'Добавлен файл README' # первый коммит проекта
			# файл был сохранен в репозитории
```
Теперь откроем файл в редакторе, добавим в него произвольный текст, сохраним и закроем. Если вызвать теперь команду ```git status```, то она покажет нам новый статус файла - **modified** в красном цвете. Также в последней строке сообщается, что изменения пока не добавлены в коммит:
```
no changes added to commit (use "git add" and/or "git commit -a")
```

Подготовим файл к сохранению изменений командой:
```
git add README.md
```

Теперь команда ```git status``` сообщит нам, что изменения добавлены в коммит, статус файла прежний -**modified**- но подсвечен он зеленым.
И нет предупреждения о том, что есть какие-то изменения не внесенные в коммит.

Допустим, что перед самим коммитом пришлось опять изменить файл - мы вновь его отредактировали и сохранили. Команда ```git status``` покажет нам, что файл вновь изменен (цвет изменится на красный), и эти изменения еще не добавлены в коммит. Тут же рекомендация: для сохранения изменений нужно вновь выполнить ```git add <file>```.

#### Также сообщается, что отменить изменения можно командой ```git restore <file>```


# Оформление сообщений к коммитам

То, как написаны сообщения коммитов, тоже может подчиняться определённым правилам. Иногда эти правила продиктованы культурой команды, а иногда техническими ограничениями.
Например, в выводе команды ```git log --oneline``` умещается максимум 
**72 первых символа** сообщения, поэтому многие правила включают пункт: *«Сообщение не должно быть длиннее 72 символов»*.

## Зачем вообще писать сообщения

У каждого коммита в Git есть сообщение — то, что передаётся после параметра **-m**. Например: ```git commit -m "Добавить урок про оформление сообщений коммитов"```.

Сообщения коммитов можно сравнить с надписями на коробках в кладовке. Если надписей нет, то нужную коробку будет сложно найти: придётся заглянуть в каждую, чтобы понять, что там. А если надписи есть, то нужная найдётся сразу.

Как и надпись на коробке, сообщение коммита должно помочь определить, что внутри. Например, надпись на коробке «всякое разное» не очень полезная. Сообщение коммита «небольшие исправления» тоже: непонятно, что было исправлено в таком коммите и зачем.

**Есть общие рекомендации по тому, как правильно составить сообщение. Оно должно быть:**
* относительно коротким, чтобы его было легко прочитать;
* информативным.

## Стили оформления

Все люди разные и у всех есть предпочтения — в том числе, как формулировать сообщения коммитов. Кто-то использует **инфинитивы**: ```Исправить сообщение об ошибке E123```, кто-то — **глаголы в прошедшем времени**: ```Исправил…```, кто-то — **существительные**: ```Исправление…```.

**Без единообразия коммитов** нет и эффективной работы в **Git**. Это может показаться мелочью, но когда коммиты с сообщениями в разных стилях идут друг за другом,** их может быть сложно читать**.

Чтобы упростить работу, команды или даже целые компании часто договариваются об определённом стиле (то есть о правилах) оформления сообщений коммитов.
Например, правила могут быть такие:
* длина сообщения от 30 до 72 символов;  
* первое слово — глагол в инфинитиве («исправить», «дополнить», «добавить» и другие);  
* и так далее.


## Корпоративный

Во многих компаниях применяется **Jira** — система для организации проектов и задач. У каждой задачи в **Jira** есть идентификатор из нескольких заглавных латинских букв и номера. Например, **LGS-239** значит, что это это **239**-я задача в проекте **LGS** (сокращение от англ. *logistics* — «логистика»).
В корпоративном стиле в начале сообщения обычно указывают **Jira-ID**, а после — текст сообщения.


## Conventional Commits

Стандарт **Conventional Commits** (англ. «соглашение о коммитах») отличается качественной документацией и подробной проработкой. Он подходит для репозиториев с исходным кодом программ. Использовать его для других типов проектов (например, для перевода книги) было бы неудобно.
**Conventional Commits** предлагает такой формат коммита: 
<type>: <сообщение>. 
Первая часть *type* — это тип изменений. Таких типов достаточно много. Вот два примера:
* feat (англ. «навык») — для новой функциональности;  
* fix (от англ. «исправить», «устранить») — для исправленных ошибок.

Более подробный список можно увидеть на сайте с [описанием этого стиля](https://www.conventionalcommits.org/ru/v1.0.0-beta.4/#спецификация).

Пример такого коммита:
```
git commit -m "feat: добавить подсчёт суммы заказов за неделю"
```

## GitHub-стиль

**GitHub** можно использовать не только для хранения файлов проекта, но и для ведения списка задач (англ. *issue*) этого проекта. Если коммит «закрывает» или «решает» какую-то задачу, то в его сообщении удобно указывать ссылку на неё. Для этого в любом месте сообщения нужно указать #<номер задачи>. Например, вот так:
```
$ git commit -m "Исправить #334, добавить график температуры"
```
В таком случае GitHub свяжет коммит и задачу.

**Совет. Инфинитив и императив**

Для сообщений на русском языке часто рекомендуют использовать инфинитивы. Например: ```Добавить тесты для PipkaService```, ```Исправить ошибку #123``` и так далее.

Для сообщений на английском рекомендуется использовать повелительное наклонение (англ. imperative). Например: ```Use library mega_lib_300```, ```Fix exit button``` и так далее.

Эти рекомендации сложились исторически, и им следуют многие проекты.

## Формат описания схем Mermaid.

Принцип такой: описывается схема в специальном текстовом формате, а GitHub превращает описание в полноценную схему с блоками и стрелками.

Чтобы получить ```mermaid```-схему в ```README.md```, нужно добавить блок кода типа ```mermaid```.
```
HEAD -- это голова.
Коммит -- это всему голова.
Статусы файлов:
<тут пустая строка!>

```mermaid
%% описание схемы

<и тут пустая строка!>
```

* Блоки кода в маркдауне начинаются и заканчиваются тремя символами ```. После первых трёх ``` можно указать, какой именно код будет внутри блока. Например: ```mermaid , ```bash, ```python, ```javascript и так далее. Если ничего не указать, GitHub будет считать весь код простым текстом.

###  Перед блоком и после него нужны пустые строки, иначе GitHub может не понять, что это блок кода.

* Два символа %% обозначают в mermaid строку-комментарий. 
* Чтобы сделать схему, нужно указать формат: **graph LR**. **Graph** — это простейший тип схем; для шпаргалки его будет достаточно.
* Чтобы добавить элементы и связи (стрелки), используют строки вида ```A --> B```. Такая строка создаст квадратные блоки ```А``` и ```B``` и соединит их стрелкой.

Дополнительно можно указывать текст на стрелке. Например, так: ```A -- "text" --> B```.

## Заготовка для схемы статусов файлов:

```mermaid
graph LR;
  untracked -- "git add" --> staged;
  staged    -- "git commit -m"     --> tracked/comitted;

%% стрелка без текста для примера: 
  A --> B;
```

# Изменить коммит

## Меняем подпись коммита

Бывают случаи, когда комментарий коммита по-ошибке дублирует предыдущий, или текс комментария получился неинформативный.
Всегда можно исправить этот текст.
Например, текст последнего коммита правится командой:
```
git commit --amend -m "Новое название коммита"
```

Сложнее, если требуется изменить коммит не последний коммит.
1. Сначала выполнить команду: 
```git log --oneline```

Далее просматриваем список коммитов и определяем смещение изменяемого коммитаотносительно **HEAD**.
2. Теперь запускаем в интерактивном режиме ```rebase```:
```
git rebase -i HEAD~<смещение изменяемого коммита>
```

3. В открывшемя редакторе в строках коммита меняем команду ```pick``` на ```reword```.
Сохраняем файл и выходим.
4. Начнется ребейз и автоматически откроется файл редактирования коммита, где после ```tmp``` вводим новую подпись к коммиту.
Сохраняем файл и выходим.

**Важно.** Мы изменили коммиты только локально. Чтобы запушить ветку на сервер, нужно использовать флаг ```--force```:
```
git push --force
```

## Меняем состав коммита

Иногда забывают включить в коммит еще один какой-то важный файл. Исправить ситуацию поможет команда с флагом ```--no-edit```.
Но прежде, нужно добавить нужный файл:

```
git add <важный файл>
git commit --amend --no-edit
```

# Как откатиться назад, если «всё сломалось»

На разных этапах работы с Git могут происходить похожие ситуации:
* В список на коммит попал лишний файл (например, временный). Нужно «вынуть» его из списка.  
* Последние несколько коммитов ошибочные: например, сделали не то, что было нужно, или нарушили логику. Хочется «откатить» сразу несколько коммитов, вернуть «как было вчера».  
* Случайно изменился файл, который вообще не должен был меняться. Например, вы открыли не тот файл в редакторе и начали его исправлять.

## Выполнить unstage изменений — git restore --staged <file>

Допустим, мы создали или изменили какой-то файл и добавили его в список «на коммит» (**staging area**) с помощью ```git add```, но потом передумали включать его туда. Убрать файл из **staging** поможет команда 
```
git restore --staged <file>
```

Чтобы «сбросить» все файлы из **staged** обратно в **untracked/modified**, можно воспользоваться командой ```git restore --staged .```: она сбросит всю текущую папку (.).

## «Откатить» коммит — git reset --hard <commit hash>

Иногда нужно «откатить» то, что уже было закоммичено, то есть вернуть состояние репозитория к более раннему. Для этого используют команду
```
git reset --hard <commit hash> # <commit hash> - хеш коммита, предшествующий удаляемому
```

## «Откатить» изменения, которые не попали ни в staging, ни в коммит, — git restore <file>
Может быть так, что мы случайно изменили файл, который не планировали. Теперь он отображается в **Changes not staged for commit (modified)**. Чтобы вернуть всё «как было», можно выполнить команду
```
git restore <file>
```


# Просматриваем изменения в файлах

При работе с Git часто нужно узнать, что конкретно изменится или уже изменилось после того или иного коммита. Вот примеры таких ситуаций:
* необходимо сделать коммит, но перед этим проверить (или перепроверить), какие именно изменения в него попадут.  
* Вчера ваш коллега сделал коммит с сообщением small fix (англ. «небольшое исправление»), после чего тесты проекта начали «падать». Чтобы разобраться в ситуации, нужно посмотреть, что изменилось в этом коммите.  

Всё это позволяет делать команда ```git diff``` (от англ. *difference* — «отличие», «разница»)

Команда ```git diff``` сравнит последнюю закоммиченную версию файла с той, что находится в состоянии modified.
Команда ```git diff --staged```  покажет изменения в staged-файлах относительно последних закоммиченных версий.

Команда выводит несколько строк:

​	*красный* цвет строки < some string > значит, что *эта строка была удалена*;
​	*зелёный* цвет строки < some string > значит, что *она была добавлена*.
​	
Не все консоли умеют выводить цвета, поэтому строки помечаются не только цветом, но и знаком **-** или **+**. **Минус** — это *удалённые* строки, **плюс** — это *добавленные*.

Коротко разберём остальные строки вывода команды:

- Первые две строки (`diff --git a/... b/...` и `index 901da07..ac459e1 100644`) — это низкоуровневая техническая информация. Мы не будем на ней останавливаться.
- Строки `--- a/teremok.txt` и `+++ b/teremok.txt` говорят, что дальше будет выведен результат сравнения файлов `a/teremok.txt` и `b/teremok.txt` — исходной и текущей версий.
- Строка `@@ -1,2 +1,2 @@` сообщает, какие строки файла попали в сравнение. Выражение `1,2` (неважно, с плюсом или с минусом) говорит, что были использованы две строки, начиная с первой. Если бы было, например, написано `+15,7`, это значило бы, что в сравнении участвуют 7 строк, начиная с 15-й. 
  Выражение со знаком минус (`-1,2`) относится к «оригинальной» версии файла (`a/teremok.txt`), а со знаком плюс (`+1,2`) — к «изменённой» (`b/teremok.txt`).

💡 

### Просматриваем изменения в staging area

Если файл подготовлен к коммиту (команда ```git add <file>```), то команда ```git diff``` уже не отобразит изменения.

Чтобы изменения увидеть, нужно запустить команду с параметром ```--staged```:

```
git diff --staged
```



# Сопоставляем коммиты

### Дописываем строку в файл

Дописать файл можн не открывая его. Для этого используется команда ```echo```. 

Сама по себе эта команда просто выводит в консоль то, что ей передали в качестве параметра:

```bash
$ echo "Привет!"
Привет!
```

Но если скомбинировать `echo` с символами перенаправления вывода `>>` (два знака «больше»), то всё, что должно было попасть на экран, вместо этого будет записано в файл.

```
$ cat file.txt
Первая строка файла

$ echo "Вторая строка файла" >> file.txt
$ cat file.txt
Первая строка файла
Вторая строка файла 
```

Оператор `>>` — это возможность командной строки (Bash). Его можно использовать не только с `echo`, но и с любой другой командой, которая выводит что-то на экран.

Одинарный символ `>` тоже перенаправит вывод команды в файл, **но перед этим сотрёт содержимое файла, то есть перезапишет файл целиком**.

```bash
$ cat file.txt
Первая строка файла
$ echo "Новая строка" > file.txt
$ cat file.txt
Новая строка 
```

Обратите внимание, что после использования символа `>` `Первая строка файла` исчезла.

### Селим всех остальных

Вернёмся к сказке. Сделайте по коммиту для каждого нового персонажа. Используйте команду `echo` или дописывайте строки вручную в любом текстовом редакторе.

```bash
$ echo "Лягушка-квакушка" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить лягушку-квакушку"
# пропускаем вывод команды commit

$ echo "Зайчик-побегайчик" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить зайчика-побегайчика"

$ echo "Лисичка-сестричка" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить лисичку-сестричку"

$ echo "Волчок -- серый бочок" >> teremok.txt
$ git add teremok.txt
$ git commit -m "Поселить волчка -- серого бочка"

# Пришла очередь медведя косолапого.
# Как известно, конструкция теремка не была рассчитана на массу медведя
# и теремок развалился.
# Обратите внимание на одинарный символ >
$ echo "Теремок развален" > teremok.txt
$ git add teremok.txt
$ git commit -m "Попытаться поселить медведя косолапого" 
```



Если сейчас выполнить команду `git log --oneline`, получится примерно следующее.

```bash
$ git log --oneline
48fe3dc (HEAD -> master) Попытаться поселить медведя косолапого
318ebdb Поселить волчка -- серого бочка
470c115 Поселить лисичку-сестричку
e4ede9c Поселить зайчика-побегайчика
31cf9b3 Поселить лягушку-квакушку
d7d797a Поселить мышку-норушку
1c29af6 Исходное состояние теремка 
```

Обратите внимание: у вас могут быть другие хеши, потому что они зависят в том числе от автора и времени, когда был сделан коммит.

### Сравниваем коммиты

Теперь, когда сказка рассказана и у вас есть история коммитов, попробуйте сравнить состояния файла `teremok.txt` между коммитами.

Например, чтобы получить максимально сокращённую версию сказки, можно сравнить состояние файлов на момент первого коммита (у нас это `1c29af6`) и последнего (у нас `48fe3dc`). Ваши хеши могут отличаться.

Передайте команде `git diff` хеши обоих коммитов, перечислив их после имени команды через пробел. Состояние файлов на момент первого переданного коммита будет сравниваться с состоянием файлов на момент второго.

```bash
git diff 1c29af6 48fe3dc
```

Вместо `48fe3dc` можно было использовать `HEAD`: `git diff 1c29af6 HEAD`, потому что `HEAD` указывает на последний коммит.

### Порядок аргументов `git diff`

По сути команда `git diff A B` выводит список инструкций: как превратить состояние `A` в состояние `B`. Если поменять `A` и `B` местами (`git diff B A`), то и инструкции будут обратные: как превратить `B` в `A`. При этом все зелёные строки станут красными, и наоборот.

Попробуйте `git diff <конец сказки> <начало>`. Вместо `HEAD` (конец сказки) можно также передать хеш.

Получится пересказ "задом наперед".



