# Шпаргалка. Базовые команды в консоли

## Навигация

pwd (от англ. print working directory, «показать рабочую папку») — покажи, в какой я папке;
ls (от англ. list directory contents, «отобразить содержимое директории») — покажи файлы и папки в текущей папке;
ls -a — покажи также скрытые файлы и папки, названия которых начинаются с символа .;
cd first-project (от англ. change directory, «сменить директорию») — перейди в папку first-project;
cd first-project/html — перейди в папку html, которая находится в папке first-project;
cd .. — перейди на уровень выше, в родительскую папку;
cd ~ — перейди в домашнюю директорию (/Users/Username);
cd / — перейди в корневую директорию.

## Работа с файлами и папками

### Создание

touch index.html (англ. touch, «коснуться») — создай файл index.html в текущей папке;
touch index.html style.css script.js — если нужно создать сразу несколько файлов, можно напечатать их имена в одну строку через пробел;
mkdir second-project (от англ. make directory, «создать директорию») — создай папку с именем second-project в текущей папке.

###Копирование и перемещение

cp file.txt ~/my-dir (от англ. copy, «копировать») — скопируй файл в другое место;
mv file.txt ~/my-dir (от англ. move, «переместить») — перемести файл или папку в другое место.

### Чтение

cat file.txt (от англ. concatenate and print, «объединить и распечатать») — распечатай содержимое текстового файла file.txt.

### Удаление

rm about.html (от англ. remove, «удалить») — удали файл about.html;
rmdir images (от англ. remove directory, «удалить директорию») — удали папку images;
rm -r second-project (от англ. remove, «удалить» + recursive, «рекурсивный») — удали папку second-project и всё, что она содержит.

### Полезные возможности
Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами (&&).

У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх (↑) и вниз (↓).

Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать Tab. Если файл или папка есть в текущей директории, командная строка допишет путь сама.

Например, вы находитесь в папке ```dev```. Начните вводить ```cd first``` и дважды нажмите **Tab**. Если папка ```first-project``` есть внутри ```dev```, командная строка автоматически подставит её имя. Останется только нажать **Enter**.


# Что такое Git и зачем он нужен

Git — это система контроля версий, которая помогает отслеживать изменения в проекте. Этот инструмент можно использовать как для индивидуальной, так и для командной работы.
Git позволяет сохранять изменения локально и при необходимости возвращаться к предыдущим версиям проекта. Также можно создать удалённую копию на хостинг-платформе, которая работает с Git, и поделиться результатом с другими.

## Установка GitBash не представляет сложностей. На официальном сайте скачивается файл инсталляции, который запускаем после.

## Работа с файлом настройки **.gitconfig**

Пока работаем в одиночку, но в дальнейшем может понадобиться использовать Git в команде. Чтобы участникам проекта было понятно, кто и какие изменения вносил, нужно представиться и указать имя пользователя и адрес электронной почты.
```
git config --global user.name "User Namovich" 
# имя или ник нужно написать латиницей и в кавычках

git config --global user.email username@yandex.ru
# здесь нужно указать свой настоящий email
```
Все глобальные настройки Git хранит в файле .gitconfig в домашней директории. Убедимся в этом:
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
git add README.md
```

# Делаем первый коммит

Коммит — это одна из основных сущностей в Git (и в других системах контроля версий). Коммит гарантирует, что изменения будут сохранены в истории и при необходимости к ним можно будет «откатиться». 

```
git commit -m "Мой первый коммит!"
```

Команда выведет информацию о коммите.

**Просмотреть историю коммитов —** ```git log```

#GitHub

Сейчас используем Git локально: проект first-project хранится только на компьютере. Но одно из ключевых преимуществ Git — удобство командной работы над файлами. Чтобы поделиться репозиторием — например, с коллегами, — нужно завести его удалённую версию. 

Процесс командной работы может выглядеть так: работаета над файлами проекта, например пишется код, на персональном компьютере и сохраняется в локальном репозитории. Как только накапливается достаточно правок, чтобы поделиться ими с остальными, они передаются на удалённый репозиторий. Там коллеги смогут посмотреть то, что получилось, и даже скачать себе на компьютер.

Есть несколько платформ для такой командной работы. Самая популярная — GitHub

GitHub подходит, чтобы отточить навыки работы с Git. Здесь можно завести аккаунт и вместе со своей командой работать над любыми задачами. Можно создавать проекты разных типов:
 
* приватный — только для вас;
* командный — только для членов команды;
* публичный — будет виден всем.

Также можно присоединиться к чужому open source проекту и работать над ним вместе с другими людьми со всего мира. 

* GitHub — платформа, которая работает с Git и упрощает командное взаимодействие.
* Кроме GitHub, существуют и другие подобные платформы, например GitLab, Bitbucket и так далее.
* Git — это консольный инструмент для работы с локальными и удалёнными репозиториями. Он не связан напрямую ни с одной из платформ и развивается отдельно от них.

# Регистрация на GitHub

Для работы с GitHub сначала надо зарегистрироваться на [GitHub](https://github.com). Для этого кликнем на Sign up и пройдем процедуру регистрации - укажем свой мейл, логин и пароль.

## Создание репозитория на GitHub

После регистрации и авторизации на сайте переходим на вкладку Repositories (она пока пуста), нажимае кнопку New и указываем имя нашего проекта first-project. Больше никаких других настроек на данном этапе нам не потребуется.

Репозиторий удаленный создан. Но для безопасной работы с ним нам прежде нужно сгенерировать и подключить SSH-ключ.

# Что такое SSH
Когда компьютеры обмениваются данными в сети, они следуют сетевым протоколам (англ. network protocols) — правилам обмена данными между компьютерами.
Один из наиболее распространённых сетевых протоколов — SSH (от англ. Secure Shell Protocol). Он обеспечивает безопасный обмен данными в сети. С помощью этого протокола можно получать данные с удалённого компьютера или отправлять их на него. Трафик шифруется, поэтому протокол безопасен.

SSH использует пару ключей для обеспечения безопасности — публичный и приватный: 
1 Приватный ключ (англ. private key) хранится только на вашем компьютере и не должен передаваться кому-либо ещё. Он используется для шифрования данных.
2 Публичный ключ (англ. public key) доступен всем и используется для расшифровки данных, которые были зашифрованы приватным ключом.

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

В командную строку нельзя вставить текст из буфера обмена с помощью привычного сочетания Ctrl+V.
На Windows (в Git Bash) и Linux для этого используется сочетание Ctrl+Shift+V, 
а на macOS — Cmd+V.
Также можно нажать правую кнопку мыши и выбрать пункт Paste (англ. «вставить») в выпадающем меню.


## бедиться, что репозитории связаны
```
$ git remote -v
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (fetch)
origin    git@github.com:%ИМЯ_АККАУНТА%/%ИМЯ-ПРОЕКТА%.git (push)
```
# Синхронизируем локальный и удалённый репозитории

## Основная ветка
Каждый коммит сохраняет актуальное состояние файлов. Сами же коммиты хранятся в ветках (англ. **branch**).
Если коммит — это снимок состояния файлов, то ветка — временна́я шкала, на которой расположены эти снимки. Ветка всегда начинается от одного из коммитов.
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

### ненумерованный список создаётся звёздочкой с пробелом в начале строки либо дефисом с пробелом.

```- первый пункт ненумерованного списка;```
* первый пункт ненумерованного списка;
```* второй пункт ненумерованного списка```
- второй пункт ненумерованного списка

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

line 
another line

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