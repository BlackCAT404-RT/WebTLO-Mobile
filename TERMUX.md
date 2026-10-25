# WebTLO на Android через Termux

1. Установите Termux из F-Droid: https://f-droid.org/en/packages/com.termux/
2. Скачайте **webtlo.zip** (**webtlo-win.zip** не подойдёт, он для Windows): https://github.com/keepers-team/webtlo/releases/latest/
3. Выполните:
   ```bash
   pkg update && pkg upgrade -y
   pkg install php unzip -y
   termux-setup-storage
   ```
4. Распакуйте архив:
   ```bash
   cd ~
   cp ~/storage/emulated/0/downloads/webtlo.zip ~/
   unzip webtlo.zip
   cd webtlo.local
   ```
5. Подготовьте папки:
   ```bash
   chmod +x bin/webtlo
   mkdir -p data
   ```
6. Запустите:
   ```bash
   php -S 127.0.0.1:8080 -t public
   ```
7. Откройте в браузере `http://127.0.0.1:8080`.

> **Не закрывайте Termux, пока программа работает.**

После перезапуска Termux нужно снова выполнить только запуск сервера:
```bash
cd ~/webtlo.local
termux-wake-lock
php -S 127.0.0.1:8080 -t public
```

# Обновление в будущем

Перед заменой файлов сохраните папку data (там база и конфиг), затем распакуйте новую версию и верните data на место.
