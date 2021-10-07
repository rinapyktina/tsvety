# tsvety
tsvety v vaze demonstrate

```python
from twilio.rest import Client

def msg_mom_and_dad(event=None, context=None):

    # тут нужно использовать SID и токен аутентификации, которые вы получили на Twilio
    twilio_sid = 'AC84c9f1602d7fb6af4eda5b0c39a03b37'
    auth_token = '4a2021b28f1aa606d9c6945d3c248ebd'

    whatsapp_client = Client(twilio_sid, auth_token)

    # в этот словарь можно добавлять контактные сведения тех,
    # кому вы хотите отправлять сообщения
    contact_directory = {'daddy':'+919624666836'}

    for key, value in contact_directory.items():
        msg_loved_ones = whatsapp_client.messages.create(
                body = 'good morning {} !'.format(key),
                from_= 'whatsapp:+14155238886',
                to='whatsapp:' + value,

            )

        print(msg_loved_ones.sid)
```
- Строка 1. Импорт клиента для работы с REST-API Twilio.
- Строка 3. Создание функции msg_mom_and_dad. Эту функцию мы передадим AWS. Она будет вызываться ежедневно в заданное время.
- Строки 6-7. Здесь вам нужно заменить существующие в коде sid и auth_token на собственные (об их получении мы говорили в конце предыдущего раздела).
- Строка 9. Создание объекта клиента Twilio с использованием учётных данных.
- Строка 13. Создание словаря. В качестве ключа тут используется имя получателя сообщений, в качестве значения — номер его телефона. В этот словарь можно добавить и дополнительные контактные сведения.
- Строка 15. Цикл for, в котором осуществляется обход словаря (в нём пока имеется лишь одна запись). В body нужно указать текст сообщения. Я создал простое сообщение с текстом «good morning», за которым следует значение, взятое из ключа текущего элемента словаря. В моём случае это приводит к формированию сообщения «good morning daddy !». Во from_ указывается тот WhatsApp-номер, который мы получили ранее. В to записывают номер получателя сообщения — тот, с которого ранее отправляли запрос на подключение к WhatsApp-песочнице Twilio.
- Строка 23. Тут мы, в целях проверки состояния сообщения, выводим его SID. Мы этими сведениями пользоваться не будем.

Вам, чтобы воспользоваться этим кодом для отправки сообщений, нужно изменить в нём следующее:

twilio_sid
auth_token
contact_directory
from_
body (это необязательно)

- После того, как вы внесёте в код изменения, сохраните файл. Затем распакуйте архив aws_lambda_deploy.zip, замените файл whatsapp_messaging.py на ваш файл с тем же именем, после чего снова упакуйте всё в .zip-архив. Смысл этих действий сводится к тому, чтобы внести в код ваши учётные данные и сведения о тех, кому вы хотите отправлять сообщения. Всё остальное в пакете, предназначенном для развёртывания на AWS, осталось неизменным. Теперь займёмся работой с AWS.

# Python Random Module
import random

# Number of Variables
attempts = 0

# Choose a random number
number = random.randint(1, 20)
print("I am thinking of a number between 1 and 20.")

# While the player's guesses is less then 6
while attempts < 6:
    guess = input("Take a guess: ")
    guess = int(guess)

    attempts += 1

    # If the player's guess is too low
    if guess < number:
        print("Higher")

    # If the player's guess is too high
    if guess > number:
        print("Lower")
        
    # If the player won, stop the loop
    if guess == number:
        break

# If the player won
if guess == number:
    attempts = str(attempts)
    print(f"Good job! You guessed my number in {attempts} guesses!")

# If the player lost
if guess != number:
    number = str(number)
    print(f"Nope. The number I was thinking of was {number}")

