![Это Git](pic_git.png)

**Контроль версий (контроль исходного кода)** — практика, которая позволяет отслеживать изменения исходного кода и управлять ими.

Контроль версий необходим, чтобы:
* **Хранить разные версии проекта.** Хранение версий сводится к созданию копий информации на компьютере или сервере.
* **Возвращаться к разным версиям проекта.** Функцию возврата реализуют за счёт восстановления предыдущих версий. 

**Cистема контроля** — это реализованная возможность замены информации с использованием сохраненных версий.

**Git — система контроля версий.** Программа Git берёт на себя контроль версий проекта и позволяет переключаться между ними. Git хранит не файлы целиком, а отличия между ними. Это позволяет экономить память.

Скачать Git можно с сайта https://git-scm.com/downloads/ 

# Принципы работы Git

1. Файлы в Git могут находиться в трех основных состояниях: зафиксированном, модифицированном и индексированном.

    * Зафиксированное (*committed*) состояние означает, что данные надежно сохранены в локальной базе. 
    * Модифицированное (*modified*) состояние означает, что изменения уже внесены в файл, но пока не зафиксированы в базе данных. 
    * Индексированное (*staged*) состояние означает, что вы пометили текущую версию модифицированного файла как предназначенную для следующей фиксации.

2. В результате Git-проект разбивается на три основные области: папка Git, рабочая папка и область индексирования

3. Базовый рабочий процесс в Git выглядит так:
    1. Редактируют файлы в рабочей папке. Перед выполнением следующих шагов необходим сохранить файлы - CTRL+S.
    2. Индексируют файлы, добавляя их снимки в область индексирования (команда git add).
    3. Выполняют фиксацию, беря файлы из области индексирования и сохраняя снимки в папке Git (команда  git commit).

При установке Git **первым делом** следует указать имя пользователя и адрес электронной почты. Это важно, так как данную информацию Git будет включать в каждую фиксируемую вами версию, и она обязательно включается во все создаваемые вами коммиты (зафиксированные данные):
* git config --global user.name "Имя пользователя"
* git config --global user.email example@example.com

>Передача параметра --global позволяет сделать эти настройки всего **один раз**, так как в этом случае Git будет использовать данную информацию для **всех действий** в системе. 

Если для конкретного проекта требуется указать другое имя или адрес электронной почты, надо войти в папку с проектом и выполнить эту команду без параметра --global.

Команда **git config --list** выводит список всех обнаруженных в текущий момент параметров.

Доступ к странице со справочной информацией по любой Git-команде:
* **git help <команда>**
* **git <команда> --help**


К примеру, справка по команде config открывается так:
git help config


# Git init
## Инициализация репозитория в существующей папке
Чтобы начать слежение за существующим проектом, перейдите в папку этого проекта и введите команду
**git init**

Чтобы начать управление версиями существующих файлов, укажите файлы, за которыми должна следить система, и выполните первую фиксацию изменений. Для этого потребуется несколько команд git add, добавляющих файлы, за которыми вы хотите следить, а затем команда git commit

После этого в файлы можно вносить изменения и **фиксировать** их, как только проект достигнет состояния, которое вы хотели бы **сохранить**.

ВАЖНО! Редактирование файла после выполнения команды git add требует **повторного** запуска этой команды для индексирования самой последней версии файла.
# Git add
Это многоцелевая команда, **позволяющая начать слежение за
новыми файлами**, произвести индексирование файлов. 

Команда **git add** перемещает из рабочей папки в область индексирования предназначенное для следующей фиксации содержимое.

>Возможно, целесообразнее воспринимать
эту команду как «добавление содержимого к следующему коммиту», а не как «добавление файла к проекту»

* __git add имя_файла_с_расширением__ - индексировать конкретный файл
* __git add .__ - индексировать все файлы в папке

# Git commit
Все проиндексированные файлы готовы к фиксации изменений. Фиксация выполняется командой git commit:
**git commit -m "Текст комментария"**

Лучше комментарий писать сразу, иначе без параметра -m попадаешь в редактор, из которго нужно знать как выйти с сохранением.

>Если передать команде git commit параметр -a, то система Git начнет автоматически индексировать все отслеживаемые файлы перед их фиксацией, позволяя обойтись без команды git add

**git commit -a -m "Текст комментария"**

# Git status (Краткий отчет о состоянии)
**git status --short** - упрощенный вариант вывода отчета
Рядом с именами стоит знак:
* ?? - новый неотслеживаемый файл
* А - новые файлы, добавленные в область предварительной подготовки
* М - модифицированные файлы
Пометки выводятся в два столбца: в первом указывается, индексирован ли файл, а во втором — вносились ли в него изменения. 

# Git log
Команда позволяет просматривать истории версий (Журнал изменений).

По умолчанию при отсутствии параметров команда git log выводит в **обратном хронологическом порядке** список сохраненных в данный репозиторий версий. То есть первыми показываются самые свежие коммиты. 

>Рядом с каждым коммитом указывается его контрольная сумма SHA-1, имя и электронная почта автора, дата создания и сообщение о фиксации.

Команда имеет много дополнительных параметров, позволяющих форматировать вывод

Например, **git log -p** (показывает разницу, внесенную каждым коммитом)


# Git checkout
Используется для перехода на существующую ветку или к какой-либо версии документа

**git checkout номер_коммит** - вводим 4 символа коммита и нажимаем TAB (подставяется весь номер)

**git checkout master** - возвращаемся к актуальной версии документа

# Git branch
>**ЗАПОМНИ!** Так как создание веток никак не влияет на память или жесткий диск, лучше и проще разбивать свою работу на множество маленьких веток, чем хранить все изменения в большой ветке.

**git branch [name]** - создает новую ветку с именем [name]

Например, **git branch newImage** - создает новую ветку и ветка newImage теперь указывает на последний созданный коммит.

ВАЖНО! При создании новой ветки мы туда автоматически НЕ ПЕРЕХОДИМ!

После создания ветки нужно:
* **git checkout newImage** - перейти на ветку newImage
* **git commit** - создать комментарий уже в ветке **newImage**

>**Лайфхак!** Можно создать новую ветку и переключиться на неё с помощью одной команды: **git checkout -b [name]**

# Объединение изменений в ветках

# Git merge

# Git rebase

# Перевод сообщений

* On branch master - Находимся на ветке master
* Untracked files - Неотслеживаемый файл - указанное состояние означает, что Git видит файл, отсутствующий в предыдущем снимке состояния (в коммите); без явного указания Git не будет добавлять этот файл в число коммитов. 
* Changes to be committed - Изменения, которые необходимо зафиксировать - все проиндексированные файлы (для которых была выполнена команда git add) перечисляются под этим заголовком
* Changes not staged for commit - Отслеживаемый файл из рабочей папки был изменен, но пока не проиндексирован.
* Nothing to commit, working tree clean - нет измененных файлов в проекте (или измененные, но не сохраненные)
