## Шпаргалка по Git

### Инициализация репозитория
Для того, чтобы добавить проект под контроль версий Git, необходимо перейти в папку с проектом и ввести команду:
```bash
git init
```
После применения команды Git создаст внтури вашего проекта папку .git, в которой будет храниться история изменений вашего проекта.

### Фиксация изменений
После внесения изменений в проекте (добавление, изменение, удаление файлов), можно посмотреть текущее состояние файлов командой:
```bash
git status
```
После выполнения команды, в выводе можно увидеть, какие файлы изменились. Если файл был создан, то он будет помечен как _Untracked_, то есть Git его видит, но данный файл не находится под системой контроля версий то его надо будет добавить в коммит, чтобы Git начал отслеживать в нем изменения. Если измененный или удаленный файл уже находился под системой контроля версий, то в выводе он будет помечен, _Unstaging_, то есть Git о нем знает, но он также не добавлен для внесения в коммит.


Чтобы добавить файлы для внесения их в коммит, необходимо выполнить команду _git add_. Добавить можно по-разному:
1. Добавить конкретный файл:
```bash
git add todo.txt
```
2. Добавить все файлы, которые как-либо изменились:
```bash
git add --all
```
3. Добавить папку целиком (аналогично команде с ключом --all):
```bash
git add .
```
После выполнения команды, все изменившиеся файлы будут готовы для внесения их в коммит.


Чтобы сделать коммит, то есть зафиксировать текущее состояние файлов и их изменений, необходимо выполнить следующую команду:
```bash
git commit -m <your-commit-message>
```
Ключ -m позволяет дать название вашему коммиту, который затем можно будет посмотреть в истории коммитов.
После выполнения команды создается коммит, который сохраняется в вашем локальном репозитории.

### Просмотр истории изменений
Чтобы посмотреть, какие коммиты были сделаны, можно выполнить следующую команду:
```bash
git log
```
После выполнения команды, в терминале отображаются все коммиты, которые были сделаны в данном проекте, в хронологическом порядке начиная с самого последнего коммита.

Чтобы получить сокращенный лог, где будут указаны только сокращенный хэш и название коммита, можно использоввать команду с ключом _--oneline_. Это полезно, когда в репозитории уже много коммитов и необходимо быстро найти нужный коммит по его названию. Сокращенный хэш можно использовать точно так же как и полный. Git сам выбирает, какой длины должен быть сокращенный хэш, чтобы он был уникальным в рамка одного репозитория.

### Отправка изменений на удаленный репозиторий
Для отправки изменений на удаленный репозиторий, находящийся например на платформе GitHub, необходимо выполнить несколько этапов.

1. Зарегистрироваться на платформе.
2. Создать SSH ключ, чтобы передавать данные в зашифрованном виде.
3. Создать репозиторий на платформе
4. Связать удаленный репозиторий с локальным
5. Выполнить отправку изменений в удаленный репозиторий

#### Создание SSH ключа
Чтобы создать ключ, необходимо выполнить команду
```bash
ssh-keygen -t rsa -b 4096 "<your-github-account-email>"
```
После выполнения команды в домашней директории, в папке .ssh появятся ключи id_rsa (приватный ключ) и id_rsa.pub (публичный ключ).
Публичный ключ необходимо скопировать и добавить в аккаунт на GitHub.

#### Связать удаленный репозиторий с локальным
Чтобы связать удаленный репозиторий с локальным необходимо выполнить команду:
```bash
git remote add origin <repository-address>
```
Команде передается два параметра имя удаленного репозитория и его URL. В качестве имени обычно используют _origin_
Чтобы посмотреть успешно ли выполнилась предыдущая команда, можно выполнить команду,
```bash
git remote -v
```
которая покажет все доступные связи локального репозитория с удаленным.

#### Отправка изменений на удаленный репозиторий
Чтобы отправить изменения на удаленный репозиторий необходимо выполнить команду _git push_.
Команда принимает два параметра, это имя удаленного репозитория (в нашем случае это _origin_) и ветку, в которую мы хотим добавить изменения.
Если это первое использование команды в репозитории, то необходимо добавить ключ -u
```bash
git push -u origin master
```
После выполнения данной команды все изменения будут отправлены на удаленный репозиторий.
Все дальнейшие вызовы этой команды уже можно делать без ключа -u
```bash
git push
```
Либо с указанием имени репозитория и ветки
```bash
git push origin master
```
