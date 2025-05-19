# send_email.py

**Описание**: Программа для автоматической отправки электронной почты по расписанию с Windows Server  
**Автор**: Маркушев Андрей 
**Версия**: 1.0  
**Год**: 2025  

## Описание программы

Эта программа предназначена для автоматической отправки электронных писем по заранее установленному расписанию с использованием почтового сервера (SMTP). Скрипт поддерживает работу как с авторизацией на сервере, так и без нее.

### Основные возможности:
- Поддерживает отправку сообщений через SMTP-сервер с/без авторизации
- Возможность интеграции с планировщиком задач Windows Server для регулярного запуска

## Установка пакетов

Перед началом убедитесь, что установлены нужные зависимости. Для установки пакета `python-dotenv` выполните команду:

#
pip install python-dotenv
#
#
#
#
Пример без авторизации на SMTP-сервере
#
---
import smtplib
from email.message import EmailMessage

# Почтовые настройки
TO = 'it@andruhes.ru'
FROM = 'napominalka@andruhes.ru'
SUBJECT = 'Напоминание по работе сервера'
BODY = 'Выгрузить из РП ЗУП файл и отправить на почту мне'
SMTP_SERVER = '192.168.100.5'   # адрес вашего SMTP-сервера

# Формирование письма
msg = EmailMessage()
msg['Subject'] = SUBJECT
msg['From'] = FROM
msg['To'] = TO
msg.set_content(BODY)

try:
    # Отправка письма через SMTP-сервер
    with smtplib.SMTP(SMTP_SERVER) as server:
        server.send_message(msg)
    print("Email успешно отправлен!")
except Exception as e:
    print(f"Произошла ошибка при отправке письма: {e}")
---
#
#
#
#
Пример с авторизацией на SMTP-сервере
#
---
import smtplib
from email.message import EmailMessage

# Почтовые настройки
TO = 'it@andruhes.ru'
FROM = 'napominalka@andruhes.ru'
SUBJECT = 'Напоминание по работе сервера'
BODY = 'Выгрузить из РП ЗУП файл и отправить на почту мне'
SMTP_SERVER = '192.168.100.5'     # адрес вашего SMTP-сервера
SMTP_PORT = 587                   # порт SMTP-сервера (обычно 587 для STARTTLS)
USERNAME = 'ВашЛогин'            # ваш логин для авторизации
PASSWORD = 'ВашПароль'           # пароль от аккаунта

# Формирование письма
msg = EmailMessage()
msg['Subject'] = SUBJECT
msg['From'] = FROM
msg['To'] = TO
msg.set_content(BODY)

try:
    # Отправка письма через SMTP-сервер с авторизацией
    with smtplib.SMTP(SMTP_SERVER, SMTP_PORT) as server:
        server.starttls()              # включение зашифрованного соединения TLS
        server.login(USERNAME, PASSWORD)  # авторизация на сервере
        server.send_message(msg)
    print("Email успешно отправлен!")
except Exception as e:
    print(f"Произошла ошибка при отправке письма: {e}")
---
