import discord
from discord.ext import commands
import random

# Создаем бота с префиксом "!"
bot = commands.Bot(command_prefix='!')

# Создаем словарь для хранения баланса пользователей
user_balances = {}

# Помощник для получения баланса пользователя
def get_balance(user_id):
    return user_balances.get(user_id, 0)

# Помощник для изменения баланса
def update_balance(user_id, amount):
    if user_id in user_balances:
        user_balances[user_id] += amount
    else:
        user_balances[user_id] = amount

# Команда для проверки баланса пользователя
@bot.command()
async def баланс(ctx):
    user_id = ctx.author.id
    balance = get_balance(user_id)
    await ctx.send(f"Ваш баланс: {balance} монет.")

# Первый способ заработка: Ежедневный бонус
@bot.command()
async def бонус(ctx):
    user_id = ctx.author.id
    reward = random.randint(50, 150)  # Случайный бонус от 50 до 150 монет
    update_balance(user_id, reward)
    await ctx.send(f"Вы получили {reward} монет в качестве ежедневного бонуса!")

# Второй способ заработка: Работа
@bot.command()
async def работа(ctx):
    user_id = ctx.author.id
    earnings = random.randint(100, 300)  # Случайный заработок от 100 до 300 монет
    update_balance(user_id, earnings)
    await ctx.send(f"Вы успешно поработали и заработали {earnings} монет.")

# Третий способ заработка: Азартная игра
@bot.command()
async def ставка(ctx, amount: int):
    user_id = ctx.author.id
    balance = get_balance(user_id)
    
    if balance < amount:
        await ctx.send(f"У вас недостаточно монет для ставки. Ваш текущий баланс: {balance} монет.")
        return
    
    # Шанс на выигрыш
    if random.choice([True, False]):
        update_balance(user_id, amount)  # Удвоение ставки
        await ctx.send(f"Поздравляем! Вы выиграли {amount} монет. Ваш баланс теперь {get_balance(user_id)} монет.")
    else:
        update_balance(user_id, -amount)  # Потеря ставки
        await ctx.send(f"К сожалению, вы проиграли {amount} монет. Ваш баланс теперь {get_balance(user_id)} монет.")

# Запуск бота
bot.run('YOUR_TOKEN_HERE')
