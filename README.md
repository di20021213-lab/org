Задание 1
Составьте команду rsync, которая позволяет создавать зеркальную копию домашней директории пользователя в директорию /tmp/backup
Необходимо исключить из синхронизации все директории, начинающиеся с точки (скрытые)
Необходимо сделать так, чтобы rsync подсчитывал хэш-суммы для всех файлов, даже если их время модификации и размер идентичны в источнике и приемнике.
На проверку направить скриншот с командой и результатом ее выполнения

<img width="833" height="665" alt="netology2" src="https://github.com/user-attachments/assets/7adaf4dd-86b7-46f4-8af5-fda9d238b357" />
<img width="950" height="768" alt="netology1" src="https://github.com/user-attachments/assets/1b587775-2074-4b21-9c2e-0dca2bdfa746" />
<img width="950" height="768" alt="netology" src="https://github.com/user-attachments/assets/9237fd25-d1ec-4acc-b0fb-1b82274bb39b" />












Задание 2
Написать скрипт и настроить задачу на регулярное резервное копирование домашней директории пользователя с помощью rsync и cron.
Резервная копия должна быть полностью зеркальной
Резервная копия должна создаваться раз в день, в системном логе должна появляться запись об успешном или неуспешном выполнении операции
Резервная копия размещается локально, в директории /tmp/backup
На проверку направить файл crontab и скриншот с результатом работы утилиты.
#!/bin/bash
# Исходная директория
SOURCE_DIR="/home/vboxuser"
# Целевая директория
TARGET_DIR="/tmp/backup"
# Команда rsync. Cтандартный вывод - в /dev/null, ошибки - в лог.
rsync -a --checksum --exclude=".*" "$SOURCE_DIR" "$TARGET_DIR" > /dev/null 2>> /var/log/backup.log
# Проверка кода завершения rsync и запись лога
if [ $? -eq 0 ]; then
    echo "[$(date)] Резервное копирование успешно выполнено" >> /var/log/backup.log
else
    echo "[$(date)] Ошибка при выполнении резервного копирования" >> /var/log/backup.log
fi

<img width="1208" height="777" alt="netology3" src="https://github.com/user-attachments/assets/37c3db7f-a048-4207-b70a-8e8eeed9633b" />
