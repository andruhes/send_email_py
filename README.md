# send_email_py
Моя базовая программа для отправки почты (по расписанию с windows server)


  Установите пакет python-dotenv:
pip install python-dotenv
#
# 
# 
# 
Если без аутентификации на smtp сервере, то:
---------------------------------------------
import smtplib
from email.message import EmailMessage

# Почтовые настройки
TO = 'it@andruhes.ru'
FROM = 'napominalka@andruhes.ru'
SUBJECT = 'Напоминание по работе сервера'
BODY = 'Выгрузить из РП ЗУП файл и отправить на почту мне'
SMTP_SERVER = '192.168.100.5'   # Адрес вашего SMTP-сервера

# Создаем экземпляр электронного письма
msg = EmailMessage()
msg['Subject'] = SUBJECT
msg['From'] = FROM
msg['To'] = TO
msg.set_content(BODY)

try:
    # Подключаемся к SMTP-серверу и отправляем письмо
    with smtplib.SMTP(SMTP_SERVER) as server:
        server.send_message(msg)
    print("Email успешно отправлен!")
except Exception as e:
    print(f"Произошла ошибка при отправке письма: {e}")
---------------------------------------------
  
  
  
  
Если с аутентификацией на smtp сервере, то:
---------------------------------------------
import smtplib
from email.message import EmailMessage


# Почтовые настройки
TO = 'it@andruhes.ru'
FROM = 'napominalka@andruhes.ru'
SUBJECT = 'Напоминание по работе сервера'
BODY = 'Выгрузить из РП ЗУП файл и отправить на почту мне'
SMTP_SERVER = '192.168.100.5'   # Адрес вашего SMTP-сервера
SMTP_PORT = 587                 # Порт SMTP-сервера (обычно 587 для STARTTLS)
USERNAME = 'ВашЛогин'           # Логин пользователя для входа на почтовый сервер
PASSWORD = 'ВашПароль'          # Пароль пользователя для входа на почтовый сервер

# Создаем экземпляр электронного письма
msg = EmailMessage()
msg['Subject'] = SUBJECT
msg['From'] = FROM
msg['To'] = TO
msg.set_content(BODY)

try:
    # Подключаемся к SMTP-серверу и отправляем письмо
    with smtplib.SMTP(SMTP_SERVER, SMTP_PORT) as server:
        server.starttls()              # Включаем шифрованное соединение TLS
        server.login(USERNAME, PASSWORD)  # Авторизуемся на сервере
        server.send_message(msg)
    print("Email успешно отправлен!")
except Exception as e:
    print(f"Произошла ошибка при отправке письма: {e}")
---------------------------------------------
