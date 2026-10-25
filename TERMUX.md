# WebTLO на Android через Termux

1. Установите Termux из F-Droid: https://f-droid.org/en/packages/com.termux/
2. Скачайте архив `webtlo.zip` со страницы релизов: https://github.com/keepers-team/webtlo/releases/latest/
   Нужен файл, который называется `webtlo.zip`. Файл `webtlo-win.zip` не подойдёт, он для Windows.
3. Откройте Termux и выполните:
   ```bash
   pkg update && pkg upgrade -y
   pkg install php unzip -y
   termux-setup-storage
   ```
   Подтвердите разрешение на доступ к файлам.
4. Проверьте, что файл виден:
   ```bash
   ls ~/storage/downloads/webtlo.zip
   ```
   Если команда выводит имя файла, всё в порядке. Если «No such file», проверьте имя командой `ls ~/storage/downloads`.
5. Скопируйте и распакуйте архив:
   ```bash
   cd ~
   cp ~/storage/downloads/webtlo.zip ~/
   unzip webtlo.zip
   cd webtlo.local
   ```
6. Подготовьте папки:
   ```bash
   chmod +x bin/webtlo
   mkdir -p data
   ```
7. Запустите сервер:
   ```bash
   termux-wake-lock
   php -d error_reporting="E_ALL & ~E_DEPRECATED" -S 127.0.0.1:8080 -t public
   ```
8. Откройте в браузере `http://127.0.0.1:8080`. Обязательно с `http://`, а не `https://`.

> **Не закрывайте Termux, пока программа работает.**

## После перезапуска Termux

Установку и распаковку повторять не нужно. Достаточно выполнить:

```bash
cd ~/webtlo.local
termux-wake-lock
php -d error_reporting="E_ALL & ~E_DEPRECATED" -S 127.0.0.1:8080 -t public
```

## Обновление в будущем

Перед заменой файлов сохраните папку `data` (там база и конфиг), затем распакуйте новую версию и верните `data` на место.

## Частые ошибки

**`php: command not found`**
PHP не установлен. Выполните `pkg install php -y`, затем проверьте `php -v`.

**`unzip: command not found`**
Выполните `pkg install unzip -y`.

**`ls: cannot access '.../storage/downloads'`**
Доступ к файлам не выдан. Выполните `termux-setup-storage` и нажмите «Разрешить». Если окна не было, включите разрешение вручную: Настройки Android → Приложения → Termux → Разрешения → Файлы и мультимедиа.

**`Соединение было сброшено` в браузере**
Сервер не запущен или адрес открыт через `https://`. Откройте именно `http://127.0.0.1:8080` и проверьте, что в Termux написано `Development Server ... started`.

**`Address already in use`**
Порт 8080 занят другим процессом. Запустите сервер на другом порту, например `php -S 127.0.0.1:8090 -t public`, и откройте `http://127.0.0.1:8090`.

**`Failed opening required .../vendor/autoload.php`**
Архив распакован не полностью. Удалите папку `webtlo.local` (`rm -rf ~/webtlo.local`) и повторите распаковку.

**`Deprecated: Method PDO::sqliteCreateFunction()...`**
Это предупреждение, а не ошибка, программа работает. Чтобы оно не мешало, запускайте сервер командой из инструкции с `-d error_reporting="E_ALL & ~E_DEPRECATED"`.
