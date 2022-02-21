## ТЕРМИНАЛ bash

[ССЫЛКА НА КУРС](https://ru.hexlet.io/courses/cli-basics)

### ОБЩИЕ МОМЕНТЫ
У команд бывают аргументы и опции (их также называют флагами).<br>
Опции всегда начинаются с одного или двух дефисов. Опции можно комбинировать.<br>

Большинство утилит имеет две версии одной и той же опции: одна из них длинная, другая — короткая. Например -v и --version.

`GUI` (Graphical User Interface — графический интерфейс)<br>
`CLI` (Command Line Interface — интерфейс командной строки)<br>

**man (manual)** - просмотреть документацию команды. Например man ls<br>
`https://explainshell.com` - сюда можно вбить команду и сервис разложит её по полочкам<br>

---

### [НАВИГАЦИЯ](https://ru.hexlet.io/courses/cli-basics/lessons/navigation/theory_unit)
**pwd** (print working directory) - рабочая директория (текущее местоположение)

#### cd (change directory)
`cd` - перемещение по файловой системе<br>
`cd ..` - переход на директорию выше. Можно так: `cd ../../..`<br>

`cd music` и `cd ./music` эквивалентны. Ординарная точка - это текущая директория<br>
`cd без аргументов` перебрасывает в домашнюю директорию текущего пользователя<br>
`cd ~` (тильда) - тоже возвращает в домашнюю директорию<br>


#### ls
`ls` - список файлов в тек. директории<br>
`ls` принимает аргумент - директорию, которую нужно проанализировать (можно использовать относительные и абсолютные пути)

#### Навигация.дополнительно
`echo $PWD` можно использовать для получения текущего местоположения<br>
`/` - вершина файловой системы<br>
`stat` - информация о файле или директории<br>
`абсолютный путь` - путь от корня (от /)<br>
`относительный путь` - начинается от текущей директории<br>
`/etc` - содержит конфигурацию программ в обычных текстовых файлах<br>
`/home` - содержит домашние директории пользователей системы (исключением является суперпользователь root, его домашний каталог обычно находится по адресу /root)<br>

`/var/log` - логи самого линукса и большинства программ<br>
`https://ru.wikipedia.org/wiki/FHS` - тут подробнее<br>
`.file-name` - точка перед именем сделает файл скрытым<br>

В отличие от Windows, в *nix-системах отсутствует понятие "расширение файла". Точка — полноправная часть имени.<br>

---

### [ЧТЕНИЕ ФАЙЛОВ](https://ru.hexlet.io/courses/cli-basics/lessons/read-files/theory_unit)
**cat** - просто читает файлы (не открывает). Ожидает аргументы - пути до файлов.<br>

**head** и **tail** читают первые/последние 10 строк файла (это можно менять флагом -n): head -n 11 /home/fileName.<br>
`tail -f path/to/log/file` поможет смотреть логи (последние 10 строк) в фоновом режиме (флаг -f).<br>

**less** открывает файл и остаётся в этом режиме (редактировать нельзя). Хорошо подходит для просмотра больших файлов, так как загружает только отображаемую на экране часть файла (выход `-q`, вперед/назад `- f/b`).
Если набрать `/`, затем начать вводить буквы и нажать Enter, то выполнится поиск введённого текста. Перемещение по найденным совпадениям выполняется командой `n` (переход к следующему совпадению) и командой `N` (переход к предыдущему совпадению).

#### grep (global regular expression print)
**grep**<br>- выполняет поиск по файлу или файлам определённого текста.<br>
Для поиска во всей директории указывается путь до директории.<br>

Еесли открыть man
`PATTERN` — это то, что ищется (строка или регулярка)<br>
`FILE` — путь до файла<br>

Количество выводимых соседних строк регулируется опциями -B, -A и -C.<br> 
`-B --before-context`<br>
`-A --after-context`<br>
`-C --context`<br>

---

### [МАНИПУЛИРОВАНИЕ ФАЙЛОВОЙ СТРУКТУРОЙ](https://ru.hexlet.io/courses/cli-basics/lessons/filetree-manipulations/theory_unit)
Утилита **touch**.
Основная задача утилиты — поменять время последнего доступа к файлу, но она обладает побочным эффектом. Если файла не существует, то он будет создан — именно поэтому её используют для создания файлов, хотя это не основное предназначение.<br>

**rm (remove files)** - удаление файлов.<br>

**mv (move)** - перемещение файлов: `mv source destination`<br> 
В *nix-системах нельзя "переименовать файл". Переименование всегда равносильно перемещению, которое выполняется командой `mv (move)`.<br>

**cp (copy)** - копирование файлов: `cp file file-copy`.<br> 
Для копирования директории нужно добавить флаг `-r (recursive)`.<br>

**mkdir (make directory)** - создание директориии.<br> 
Чтобы создать вложенные директории, надо восользовтся флагом `-p`, который создаёт директории рекурсивно.<br>
`mkdir -p one/two/three`.<br>

**rm -r** - удаление директорий выполняется той же утилитой, что и для файлов, но с флагом `-r` (r — recursion).<br>

**rm -f** - флаг `-f(или --force)` позволяет игнорировать несуществующие файлы и не запрашивать подтверждение на удаление.<br>

Утилита **tree** позволяет красиво показать фалойвую структуру в указанной директории.<br> 
Надо устонавливать: `sudo snap install tree`.<br>

---

### [ПОТОКИ](https://ru.hexlet.io/courses/cli-basics/lessons/streams/theory_unit)
При старте любой программы операционная система связывает с ней три так называемых потока: 
- `STDIN` (Standard Input)<br>
- `STDOUT` (Standard Output)<br>
- `STDERR` (Standard Error)<br>
Для языка программирования они выглядят как файлы. ОС позволяет подменять эти потоки при старте системы.<br>

Вывод любой команды, запущенной в bash, можно записать в файл вместо вывода на экран: 
`ls > fileName` - эта операция называется `перенаправлением потоков`. Символ > означает, что нужно взять вывод из команды, указанной слева, и отправить его в файл, указанный справа.<br>

`>` перезаписывает файл.<br>
`>>` добавляет в файл.<br>

 
`STDIN` работает в обратную сторону: через него программа может получать данные на вход.<br>
`wc -l < result`
Cтрелка меняет своё направление в другую сторону и содержимое файла отправляется в STDIN запускаемой программы `wc`.<br>
Встроеная утилита `wc` (word count — "количество слов"), которая умеет считать количество слов, строк или символов в файле<br>


Поток `STDERR` - как и STDOUT, по умолчанию идёт на экран. Позволяет отделить нормальный вывод программы от возникающих ошибок.<br>

`ls lala 2>&1 > output` - так не сработает. Нужно перенаправить `STDERR` в `STDOUT`: 
`ls lala > output 2>&1` - Сначала STDOUT перенаправляется в файл, затем STDERR перенаправляется в STDOUT, продолжая запись в файл.<br>
Cуществуют следующие стандартные потоки ввода-вывода: STDIN — 0, STDOUT — 1, STDERR — 2.<br>

Утилита **tee** - считывает стандартный ввод и записывает его одновременно в стандартный вывод и в один или несколько подготовленных файлов.<br> 
`tee file_name` - вводим что угодно в терминале и это попадает в файл `file_name` а заодно ещё и выводится.

---

### [ПАЙПЛАЙН](https://ru.hexlet.io/courses/cli-basics/lessons/pipeline/theory_unit)
`|` — этот символ называется пайп, он указывает шеллу взять STDOUT одного процесса, и соединить его с STDIN другого процесса. 

---

### [ПЕРЕМЕННЫЕ ОКРУЖЕНИЯ](https://ru.hexlet.io/courses/cli-basics/lessons/environment-variables/theory_unit)
Основное предназначение переменных окружения — конфигурирование системы и программ.
Посмотреть установленные переменные можно командой `env (environment)`.<br>
 
Существует некоторый базовый набор переменных, которые всегда устанавливаются bash при старте. Они используются большим количеством утилит и нужны для нормального функционирования системы. Одну из таких переменных мы уже знаем — это `HOME`.<br>

Установить/поменять переменную окружения: `HOME`=/ (без пробелов вокруг =)<br>

Посмотреть переменну окружения: `echo $HOME`.<br>

При помощи команды export можно установить несколько переменных окружения. Для этого достаточно указать их через пробел: `export name1=value1 name2=value2`<br>

---

### [ИСТОРИЯ](https://ru.hexlet.io/courses/cli-basics/lessons/history/theory_unit)
История команд `bash` хранится в специальном файле `.bash_history`, который лежит в домашней директории пользователя.<br>

За то, какое количество команд хранится в истории, отвечает переменная окружения `HISTFILESIZE`.<br>

Посмотреть историю можно и более простым способом, достаточно выполнить команду `history`<br>
Если набрать `history 5`, то отобразятся только 5 последних введённых команд.<br>

При необходимости историю всегда можно погрепать: `history | grep PATTERN`.<br>

Cамое интересное — `реверсивный поиск`. Если нажать комбинацию `Ctrl + r`, то запустится специальный поиск по истории. Он ожидает ввода символов и сразу отображает ближайшую команду. Eсли найденное соответствие вас не устроило, то `повторное нажатие Ctrl + r` выберет следующее соответствие из истории. Нажатие на `Enter` выполнит команду.

---


### [SUDO](https://ru.hexlet.io/courses/cli-basics/lessons/sudo/theory_unit)
Иногда бывает нужно выполнить команду из-под пользователя, отличного от root. Тогда придётся добавить флаг `-u`.<br>

Если стоит задача произвести сразу пачку действий от имени другого пользователя, то для этого можно запустить новую оболочку внутри текущей (говорят что мы стартуем новую сессию): `sudo -i`. Главное — не забыть переключиться обратно после завершения необходимых манипуляций. Для этого наберите exit.<br>

C sudo надо быть аккуратным. Запуск команды, которая создаёт файлы и директории из-под sudo, приводит к тому, что владельцем этих файлов становится пользователь root. Фактически все последующие обращения к этому файлу без sudo начнут выдавать ошибку об отсутствии прав доступа.<br>
Наиболее общее правило может быть таким: всё, что лежит в личных директориях пользователя, должно принадлежать пользователю, а не суперпользователю. Всё, что требует дополнительных прав, так как находится в системных путях (вне домашней директории пользователя), скорее должно запускаться с sudo (но это необязательно).<br>

---

### [ПАКЕТНЫЙ МЕНЕДЖЕР](https://ru.hexlet.io/courses/cli-basics/lessons/package-manager/theory_unit)

**apt** - Пакетный менеджер.<br> 
`apt install Name` - так устанавливаются пакеты.<br>
`apt remove Name` - так удаляются пакеты.<br>
`sudo apt update` - обновление локального индекса (подробнее в ссылке)<br>

---
