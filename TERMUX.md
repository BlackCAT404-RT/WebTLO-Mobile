# WebTLO на Android через Termux

1. Установите Termux из F-Droid: https://f-droid.org/en/packages/com.termux/
2. Выполните:
   ```bash
   pkg update && pkg upgrade -y
   pkg install php unzip -y
   termux-setup-storage
   ```
3. Распакуйте архив:
   ```bash
   cd ~
   cp ~/storage/downloads/webtlo.zip ~/
   unzip webtlo.zip
   cd webtlo.local
   ```
4. Подготовьте папки:
   ```bash
   chmod +x bin/webtlo
   mkdir -p data
   ```
5. Запустите:
   ```bash
   php -S 127.0.0.1:8080 -t public
   ```
6. Откройте в браузере `http://127.0.0.1:8080`.

> **Не закрывайте Termux, пока программа работает.**
