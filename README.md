# Hello, there!

### Это обзорный урок по git мотивам курса от [ЯндексПрактикум](https://practicum.yandex.ru "Yandex Practicum")

## GIt - это система контроля версий

---

По сути git является программой, установленной локально на машинах пользователей, и служит для упрощения совместной разработки.

## Начало работы и инициализация проекта

Для того, чтобы начать пользоваться git на вашем компьютере, можно использовать менеджер пакетов Homebrew (я пользуюсь MacOS, поэтому пишу применительно к этой системе)
Чтобы установить систему контроля версий на ваш компьютер достаточно перейти на страницу [Homebrew](https://brew.sh), проследовать инструкции и установить данный менеджер пакетов.

После чего в командной строке ввести команду

```sh
brew install git
```

Теперь мы можем воспользоваться Git!
Откройте Ваш проект и проинициализируйте git-репозиторий:

```sh
git init
```

### Работа с Git

Состояние вашего проекта можно отследить, используя команду:

```sh
git status
```

В любой непонятной ситуации, команда даст Вам подсказку для дальнейших действий, не пренерегайте ее использовать и **все у Вас будет отлично!**

Предположим Вы внесли какие-то изменения в Ваш проект, будь то:

- Создали новую папку
- Создали нвоый файл
- Внесли изменения в существующий файл

Алгоритм дальнейших действий будет следующий:

1. Начать следить за изменениями с помощью команды:

```sh
git add .
```

2. Зафиксировать (закоммитить изменения) с помощью команды:

```sh
git commit -m
```

После флага -m обычно пишут какое-либо сообщение, описывающее данный коммит

Мне понравилось объяснение на курсе [Практикума](https://practicum.yandex.ru), объясняющего разницу между командами "git add" и "git commit":

> Сначала вы просите друзей встать в ряд — это команда git add. И только после того, как все заняли свои места, поправили волосы и улыбнулись, вы нажимаете кнопку и делаете снимок — это команда git commit. Сам получившийся снимок и будет коммитом. В нашем случае на этой фотографии с обратной стороны ещё есть подпись «Мой первый коммит!».

Подпись к фотографии и есть то сообщение, которе мы указываем после флага -m, по ним в дальнейшем можно будет легко ориентироваться между коммитами.

_Есть еще очень полезная команда_

```
git log
```

Позволяет вывести список всех **commit**-ов с подробной информацией о дате, времени, собственном идентефикаторе коммита, а также об авторе.
_К слову об авторе_
При инициализации проекта следует оставить свои контактные данные использую команду

```
git config user.name/user.email
```

Файл git config хранит общую информацию о git-репозитории (название основной ветки по дефолту, к примеру), и располагается в домашней директории.
**Однако**, если Вы хотите вывести данные об этом файле в папке текущего проекта, следует обратиться к ней подобным образом:

```
% git config --list
```

и выведется содержимое файла конфигурации.

## GitHub

**GitHub** - удаленная платформа для работы с локальным репозиторием Git.
Существуют и другие к примеру _GitLab_ или _Bitbucket_
Git и GitHub существуют и работают независимо друг от друга
После того, как мы создали репозиторий локально с помощью Git, нужно связать его с удаленным репозиторием на GitHub.
Лучше всего связывать репозитории с помощь SSH-ключа.
**SSH** - это сетевой протокол безопасного обмена данных в сети. Базируется на принципах приватного и публичного ключа.

Публичный - для кодирования информации, доступен всем.

Приватный - доступен только пользователю и предназначен для декодирования информации.

Подробнее останавливаться на генерации SSH-ключа в этом тексте я останавливаться не буду, так как урок все таки про GitHub.
Просто знайте, что сделать это достаточно просто, следуя гайдам в сети.

**После того как мы создали удаленный репозиторий на сайте GitHub нужно:**

1.  Связать его с локальным с помощью команды

```
git remote add origin %URL удаленного репозитория%
```

origin - псевдоним для удобства обращения к главному репозиторию 2. Проверить, что репозитории связаны

```
git remote -v
```

3. Все, что остается сделать это синхронизировать репозитории (запушить изменения)

```
git push -u origin main
```

Запись такого вида используется только один раз, флаг **-u** позволяет синхронизировать репозитории, вместо **origin** возможно использовать имя удаленного репозитория, а **main** это название текущей ветки.
Для последующих **commit**-ов возможно использовать команду

```
git push
```

# Хеш

_Основным идентификатором коммита является Хеш_
Хеш коммита отображается при вызове команды

```
git status
```

По хешу можно узнать всю информацию о коммите и обладает важными особенностями:

- для одного и того же набора входных данных хеш гарантированно одинаковый
- если что-то меняется во входных данных, то хеш тоже изменится
  Иными словами каждое незначительное изменение (каждый коммит) обладает собственными хешем.

# Git log

Для структурированный работы с коммитами удобно использовать

```
 git log
```

Выведется вся информация о коммитах:

- Хеш коммита
- Автор коммита
- Дата и время коммита
- Сообщение коммита

_Можно использовать сокращенное логирование_,  
после чего выведется сокращенная запись хеша, информация о ветке, а также сообщение коммита

```
git log --oneline
```

# HEAD

### HEAD - служебный файл папки .git

Данный файл хранит информацию о последнем сделанном коммите

Внутри себя HEAD хранит ссылку на служебный файл, который в свою очередь хранит хеш последнего коммита

**При дальнейшей работе, если какой-то команде нужен хеш коммита, можно использовать HEAD, вместо него**
