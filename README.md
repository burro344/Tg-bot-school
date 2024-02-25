# Tg-bot-school
.:
import telebot
from telebot import types
import Themes

token = '6462065863:AAHKxDdAz5CW7GMHkyjHZGhFYueGEZ2-AcA'
bot = telebot.TeleBot(token)


@bot.message_handler(commands=['start'])
def start_cmd(message):
    bot.send_message(message.chat.id, text="Привет, " + message.from_user.first_name + "! Я бот сделаный Пашкой")


@bot.message_handler(commands=['physics'])
def physics_cmd(message):
    keyboard = types.InlineKeyboardMarkup()
    for i in range(len(Themes.SECTIONS)):
        button = types.InlineKeyboardButton(
            text=Themes.SECTIONS[i],
            callback_data=Themes.SECTIONS_CALLBACK[i])
        keyboard.add(button)
    bot.send_message(message.chat.id, text="Выбери раздел физики, с которым тебе нужна помощь:", reply_markup=keyboard)


@bot.message_handler(commands=['commands'])
def commands_list_cmd(message):
    bot.send_message(message.chat.id, text="Вот список моих команд:"
                                           "\n/commands - узнать список команд с их описанием;"
                                           "\n/physics - получить справочный материал и лекции в "
                                           "видео-формате по определнной теме по физике для 9 класса.")


@bot.callback_query_handler(func=lambda call: call.data)
def callback_processor(call):
    message = call.message
    # chat_id = message.chat.id
    # message_id = message.message_id
    bot.send_message(message.chat.id, call.data)
    # bot.edit_message_text(chat_id=chat_id, message_id=message_id,
    #                     text='Данные сохранены!')


@bot.message_handler(content_types=['text'])
def func(message):
    if message.text == "Поздороваться":
        bot.send_message(message.chat.id, text="Привет!)")
    elif message.text == "помоги с физикой":
        bot.send_message(message.chat.id, text="Выбери раздел,а затем тему")

    elif message.text == "":
        bot.send_message(message.chat.id, "")
    elif message.text == "Что я могу?":
        bot.send_message(message.chat.id, text="Помочь с физикой))")
    elif message.text == "Вернуться в главное меню":
        bot.send_message(message.chat.id, text="Вы вернулись в главное меню")
    else:
        bot.send_message(message.chat.id, text="привет")


bot.polling(none_stop=True, interval=0)

SECTIONS = ['Механика', 'Молекулярная физика и термодинамика', 'Электродинамика', 'Оптика', 'Квантовая физика']
SECTIONS_CALLBACK = ['mechanic', 'mkt', 'electricity', 'optics', 'quantum']
