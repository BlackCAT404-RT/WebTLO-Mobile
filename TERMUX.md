# WebTLO на Android через Termux

1. Установите Termux из F-Droid: https://f-droid.org/en/packages/com.termux/
2. Скачайте **webtlo.zip** (**webtlo-win.zip** не подойдёт, он для Windows): https://github.com/keepers-team/webtlo/releases/latest/
3. Выполните:
   ```bash
   pkg update && pkg upgrade -y
   pkg install php unzip -y
   termux-setup-storage
   ```
4. Запросите и разрешите доступ :
   ```bash
   ls ~
   termux-setup-storage
   ```
5. Проверьте файл:
   ```bash
   ls ~/storage
   ls ~/storage/downloads
   ls ~/storage/downloads/webtlo.zip
   ```
6. Распакуйте файл:
   ```bash
   cp ~/storage/downloads/webtlo.zip ~/
   cd ~
   unzip webtlo.zip
   cd webtlo.local
   ```
   
7. Подготовьте папки:
   ```bash
   chmod +x bin/webtlo
   mkdir -p data
   ```
8. Запустите:
   ```bash
   php -S 127.0.0.1:8080 -t public
   ```
9. Откройте в браузере `http://127.0.0.1:8080`.

> **Не закрывайте Termux, пока программа работает.**

После перезапуска Termux нужно снова выполнить только запуск сервера:
```bash
cd ~/webtlo.local
termux-wake-lock
php -d error_reporting="E_ALL & ~E_DEPRECATED" -S 127.0.0.1:8080 -t public
```

# Обновление в будущем

Перед заменой файлов сохраните папку data (там база и конфиг), затем распакуйте новую версию и верните data на место.
