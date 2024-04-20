# Шпаргалка по работе с Git:

## Знакомство с Git

* Система контроля версий, или VCS (SCM), — программа, позволяющая контролировать изменения в проекте.
* Git — один из примеров системы контроля версий: он позволяет хранить, изменять и анализировать историю проекта.
* Git — незаменимый в команде инструмент, ведь он помогает объединять результаты работы нескольких человек.

## Навигация в командной строке

* `pwd` - просмотр текущей директории
* `cd [PATH]` - смена директории  
   - (`~` - переход к домашней директории)  
   - (`..` - переход к родительской директории)  
* `ls` - вывести содержимое директории  
   - (`~` - содержимое домашней директории)  
   - (`..` - содержимое родительской директории)  
   - (`-a` - расширенный список)  

## Операции с папками и файлами: создание, копирование, перемещение, чтение, удаление

* `touch [FILE_NAME]` - создать файл
* `mkdir [DIR_NAME]` - создать папку
   - (`-p [][]..` - создать вложенные папки)
* `cp [NAME][WHERE]` - копировать файл(ы), папку(-и)
* `mv [NAME][WHERE]` - переместить файл(ы), папку(-и)
* `cat [FILE_NAME]` - прочитать файл текстового формата (txt, html, css, js, json, xml, csv, и т.д.)
* `rm [FILE_NAME]` - удалить файл
   - (`-r [DIR_NAME]` - удалить папку и все вложенные файлы и папки)
* `rmdir [DIR_NAME]` - удалить папку(ошибка, если папка не пуста)

## Полезные возможности

* Команды необязательно печатать и выполнять по очереди. Можно указать их списком — разделить двумя амперсандами (`&&`).
* У консоли есть собственная память — буфер с несколькими последними командами. По ним можно перемещаться с помощью клавиш со стрелками вверх (`↑`) и вниз (`↓`).
* Чтобы не вводить название файла или папки полностью, можно набрать первые символы имени и дважды нажать `Tab`. Если файл или папка есть в текущей директории, командная строка допишет путь сама.
* Например, вы находитесь в папке `dev`. Начните вводить `cd first` и дважды нажмите `Tab`. Если папка `first-project` есть внутри `dev`, командная строка автоматически подставит её имя. Останется только нажать `Enter`.

## Настройка Git

* `git config --global user.name "User Name"`
* `git config --global user.email username@mail.com`

* `git config --list` - вывести содержимое файла конфигурации `.gitcofig`

## Работа с Git и GitHub

* `git init` - инициализировать папку как git-репозиторий
* `git status` - проверить статус репозитория
* `rm -rf .git` - “разгитить” папку путем удаления папки `.git`
   - (`-f` - force remove)
* `git add [OPTION]` - подготовить файл к сохранению
	- `--all` - подготовить к сохранению все файлы
	- `.` - подготовить к сохранению текущую папку со всеми ее файлами
* `git commit [OPTION]` - создать коммит. В коммит попадает то, что было предварительно добавлено командой `git add`
	- `-m` - присвоить коммиту сообщение
* `git log` - просмотреть историю коммитов
   - `--oneline` - вывести сокращенные логи
* `git push` - отправить изменения на удалённый репозиторий
	- (`-u origin main` - если изменения отправляются первый раз)

## Инструкция по генерации SSH-ключа:

* SSH — протокол, который обеспечивает безопасный обмен данными в сети и использует для этого ключи.
* SSH-ключ — ваш виртуальный идентификатор в GitHub. Как ключ от квартиры, он позволяет получить доступ к GitHub-репозиторию. Также SSH используется для доступа к другим удалённым серверам.
* SSH-ключ состоит из двух частей — публичной и приватной. Публичный ключ зашифрует данные, а приватный — расшифрует. Приватным ключом ни в коем случае нельзя делиться, иначе любой сможет расшифровать все ваши секреты!

----

1. Для генерации SSH-пары можно использовать программу `ssh-keygen`. Откройте терминал и введите следующую команду:
   - `ssh-keygen -t ed25519 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"`

   или

   - `ssh-keygen -t rsa -b 4096 -C "электронная почта, к которой привязан ваш аккаунт на GitHub"`

2. Укажите место хранения ключей. Простой вариант — сделать домашний каталог пользователя путём по умолчанию. Для этого нажмите `Enter`.

   - `> Enter a file in which to save the key (C:\Users\<имя_пользователя>\.ssh\):[Press enter]`

3. Программа запросит **кодовую фразу** (англ. passphrase) для доступа к SSH-ключу. Вы можете оставить поле пустым. Для этого нажмите `Enter`, а затем ещё раз `Enter` для подтверждения.
   - `> Enter passphrase (empty for no passphrase): [Type a passphrase]`
   - `> Enter same passphrase again: [Type passphrase again]`

## Привязываем SSH-ключ к GitHub

1. После выполнения команды `ssh-keygen` из предыдущего урока в директории `~/.ssh` будет создано два файла — `id_ed25519` и `id_ed25519.pub` (или `id_rsa` и `id_rsa.pub` — в зависимости от того, какой алгоритм вы использовали):
   - `id_ed25519/id_rsa` — приватный ключ (файл без `.pub` в конце). Ни в коем случае не копируйте его и не делитесь им.
   - `id_ed25519.pub/id_rsa.pub` — публичный ключ (на это указывает расширение `.pub`).
   - Скопируйте содержимое файла с публичным ключом в буфер обмена.

      * `clip < ~/.ssh/id_ed25519.pub` - скопировать содержимое в буфер обмена

2. Перейдите на GitHub и выберите пункт **Settings** (англ. «настройки») в меню аккаунта.
3. В меню слева нажмите на пункт **SSH and GPG keys**.
4. В открывшейся вкладке выберите **New SSH key** (англ. «новый SSH-ключ»).
5. В поле **Title** (англ. «заголовок») напишите название ключа. Например, **Personal key** (англ. «личный ключ»).
6. В поле **Key type** (англ. «тип ключа») должно быть **Authentication Key** (англ. «ключ аутентификации»).
7. В поле Key скопируйте ваш ключ из буфера обмена.
8. Нажмите на кнопку **Add SSH key** (англ. «добавить SSH-ключ»).
9. Проверьте правильность ключа с помощью следующей команды:
   - `ssh -T git@github.com`

## Связываем локальный и удалённый репозитории

* `git remote add origin git@github.com:%ИМЯ_АККАУНТА%/%НАЗВАНИЕ_РЕПОЗИТОРИЯ%.git` - связать локальный и удаленный репозиторий
* `git remote -v` - убедиться, что репозитории связаны
	- (`-v` - короткая форма флага `--verbose` (англ. «подробный»). Он позволяет показать больше информации в выводе)

## Дополнительный раздел про хеш-коммита и HEAD

* Git преобразует информацию о коммитах с помощью алгоритма SHA-1 и для каждого из них рассчитывает уникальный идентификатор — **хеш**.
* **Хеш** — основной идентификатор коммита и позволяет узнать его автора, дату и содержимое закоммиченных файлов.
* Все хеши, а также таблицу соответствий `хеш → информация о коммите` Git хранит в папке `.git`.


## Статусы файлов в Git

* `untracked` - неотслеживаемый (новый файл, который еще не был добавлен с помощью команды `git add` и не был зафиксирован командой `git commit`)

* `staged` - После выполнения команды `git add` файл попадает в **staging area**, то есть в список файлов, которые войдут в коммит. В этот момент файл находится в состоянии `staged`.

* `tracked` - Состояние `tracked` — это противоположность `untracked`. Оно довольно широкое по смыслу: в него попадают файлы, которые уже были зафиксированы с помощью `git commit`, а также файлы, которые были добавлены в staging area командой `git add`. То есть все файлы, в которых Git так или иначе отслеживает изменения.

* `modified` - Состояние `modified` означает, что Git сравнил содержимое файла с последней сохранённой версией и нашёл отличия. Например, файл был закоммичен и после этого изменён.