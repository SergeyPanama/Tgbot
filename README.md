# Tgbot
import telebot
from telebot import types

bot = telebot.TeleBot('5944452163:AAESFGExKfVPmbPQTr1Xz_qm9t76ZhxeXVE')


@bot.message_handler(commands=['start'])
def start(message):
    mess = f'Привет<b>{message.from_user.first_name} <u>{message.from_user.last_name}</u></b>'
    bot.send_message(message.chat.id, mess, parse_mode='html')


# @bot.message_handler(content_types=['text'])
# def get_user_text(message):
#     if message.text == "Hello":
#         bot.send_message(message.chat.id, "И тебе привет!", parse_mode='html')
#     elif message.text == "id":
#         bot.send_message(message.chat.id, f"Твой ID: {message.from_user.id}", parse_mode='html')
#     elif message.text == "photo":
#         photo = open('i.webp', 'rb')
#         bot.send_photo(message.chat.id, photo)
#     else:
#         bot.send_message(message.chat.id, "Я тебя не понимаю", parse_mode='html')


@bot.message_handler(commands=['website'])
def open_website(message):
    markup = types.InlineKeyboardMarkup()
    markup.add(types.InlineKeyboardButton("Перейдите на сайт", url="https://pypi.org/project/pyTelegramBotAPI/"))
    bot.send_message(message.chat.id, 'Перейдите на сайт!', parse_mode='html', reply_markup=markup)


@bot.message_handler(commands=['help'])
def website(message):
    markup = types.ReplyKeyboardMarkup(resize_keyboard=True)
    btn1 = types.KeyboardButton('Website')
    btn2 = types.KeyboardButton('Start')
    markup.add(btn1, btn2)
    bot.send_message(message.chat.id, 'Выбери кнопку', reply_markup=markup)


@bot.message_handler(content_types=['help'])
def bot_message(message):
    if message.chat.type == 'private':
        if message.text == 'Start':
            mess = f'Привет<b>{message.from_user.first_name} <u>{message.from_user.last_name}</u></b>'
            bot.send_message(message.chat.id, mess, parse_mode='html')


bot.polling(none_stop=True)
