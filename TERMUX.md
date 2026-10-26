# WebTLO на Android через Termux

1. Установите Termux из F-Droid: https://f-droid.org/ru/packages/com.termux/
2. Скачайте архив `webtlo.zip` со страницы релизов: https://github.com/keepers-team/webtlo/releases/latest/
   Нужен файл, который называется `webtlo.zip`. Файл `webtlo-win.zip` не подойдёт, он для Windows.
3. Откройте Termux и выполните:
```bash
pkg update -y && pkg upgrade -y
pkg install -y php unzip curl
termux-setup-storage
BASE=/storage/emulated/0/WebTLOMobile
mkdir -p "$BASE" && cd "$BASE" || exit 1
curl -fL --retry 5 --connect-timeout 10 -o webtlo.zip "https://github.com/keepers-team/webtlo/releases/latest/download/webtlo.zip" || { echo "Ошибка загрузки архива"; exit 1; }
unzip -oq webtlo.zip -d webtlo || { echo "Архив повреждён или не распакован"; exit 1; }
rm -f webtlo.zip
APP_DIR=$(dirname "$(find "$BASE/webtlo" -type d -name public -print -quit)")
if [ "$APP_DIR" = "." ] || [ ! -d "$APP_DIR" ]; then
echo "Не найдена папка с public. Содержимое архива:"
ls -R "$BASE/webtlo" | head -50
exit 1
fi
cd "$APP_DIR" || exit 1
echo "Запуск из: $PWD"
termux-wake-lock
php -d error_reporting="E_ALL & ~E_DEPRECATED" -S 127.0.0.1:8080 -t public
```
4. Откройте в браузере `http://127.0.0.1:8080`. Обязательно с `http://`, а не `https://`.

> **Не закрывайте Termux, пока программа работает.**

## После перезапуска Termux

Всё выше описанное повторять не нужно. Достаточно выполнить:

```bash
cd /storage/emulated/0/Download/webtlo/webtlo.local
termux-wake-lock
php -d error_reporting="E_ALL & ~E_DEPRECATED" -S 127.0.0.1:8080 -t public
```

## Обновление в будущем

Повторите всё выше описанное, но пропустите пункт `1` и строки:
```bash
pkg update -y && pkg upgrade -y
pkg install -y php unzip curl
```

