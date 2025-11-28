# Discord-bot template version 0.1

### Contains:
- Roll
- Say
- Greet

New version is coming out soon.

# Please be make sure you are on a pc.

# Please install python:
Step 1. Go to microsoft store.
Step 2. Search for python 3.13
Step 3. Download python 3.13
Step 4. Wait till its downloaded and then close microsoft store.

Step 1. Add a folder on your desktop. OPTIONAL: Rename the folder
Step 2. Inside the folder, add a notepad.
Step 3. Rename it to whatever you want. (We will call it BOT.)
Step 4. Add another notepad and rename it to "token". Your os will already know its "token.txt".
Step 5. Go to https://discord.com/developers/applications.
Step 6. Click on "Add application"
Step 7. Give the application a name.
(Optional: Give the application a description)
Step 8. Go to OAUTH2
Step 9. Scroll down till you see scopes.
Step 10. Select the scope "bot".
Step 11. Under bot permissions select administrator.
Step 12. Scroll down till you see "Generated URL"
Step 13. Copy the URL.
Step 14. In a new tab, enter inside of the URL bar the Generated Url.
Step 15. Authorize your bot.
Step 16. Go back to the developer portal and go to "Bot" tab.
Step 17. Reset your token.
Step 18. Copy your token.
Step 19. Go back to token.txt paste the token.
Step 20. Save the token.txt.
Step 21. Press win + r and type "cmd", hit enter.
Step 22. Run pip install discord.py
Step 23. Wait for it to install discord.py and then close the terminal.
Step 24. Go back to the developer portal and go to the tab "bot".
Step 25. Scroll down till you see "Privileged Gateway Intents".
Step 26. Enable every gateway intent.
Step 27. Go to your folder and edit the BOT's source code (Enter the following code in there thats here):
import os
import discord
from discord.ext import commands
from discord import app_commands
import asyncio
import signal
import random


your_user_id = 00000000000000


intents = discord.Intents.default()
intents.message_content = True
intents.members = True


token_abspath = os.path.abspath(__file__)
token_path = os.path.dirname(token_abspath)
token_file = os.path.join(token_path, "token.txt")

with open(token_file, "r") as file:
    TOKEN = file.read().strip()


bot = commands.Bot(command_prefix=".", intents=intents)


async def shutdown():
    for guild in bot.guilds:
        channel = discord.utils.get(guild.text_channels, name="general")
        try:
            member = await bot.fetch_user(your_user_id)
        except discord.NotFound:
            print(f"User {your_user_id} not found in {guild.name}")
            continue
        if channel and member:
            try:
                await channel.send(f"{bot.user.mention} is going offline (Shutdown by {member.mention})")
            except:
                pass
    await bot.close()

def signal_handler(sig, frame):
    asyncio.create_task(shutdown())

signal.signal(signal.SIGINT, signal_handler)


@bot.event
async def on_ready():
    print(f"{bot.user} is online!")
    for guild in bot.guilds:
        channel = discord.utils.get(guild.text_channels, name="general")
        member = await bot.fetch_user(your_user_id)
        if channel and member:
            await channel.send(f"{bot.user.mention} is online! (Hosted by {member.mention})")
    await bot.tree.sync(guild=None)

@bot.tree.command(name="greet", description="Greet someone")
@app_commands.describe(member="Who do you want to greet?")
async def greet(interaction: discord.Interaction, member: discord.Member):
    embed = discord.Embed(
        title="Greet",
        description=f"{interaction.user.mention} has greeted {member.mention}!",
        color=discord.Color.red()
    )
    await interaction.response.send_message(embed=embed)

	

@bot.tree.command(name="say", description="make the bot say something")
@app_commands.describe(text="what should the bot say")
async def say(ctx: discord.Interaction, text: str):
	await ctx.response.send_message(text)

@bot.tree.command(name="roll", description="roll a number from the chosen minimal and maxium amount")
@app_commands.describe(min="the minimal amount", max="the maxium amount")
async def roll(interaction: discord.Interaction, min: int, max: int):
	num = random.randint(min, max)
	embed = discord.Embed(
		title="Roll",
		description=f"Minimal: {min}, Maxium: {max}",
		color=discord.Color.red()
	)

	embed.add_field(name="Rolled", value=num, inline=True)
	
	await interaction.response.send_message(embed=embed)


bot.run(TOKEN)

Step 28. Go to line 10 and paste your userid; TUTORIAL ON HOW TO GET YOUR USERID:
Go to discord
Click on user settings
Scroll down till you see app settings
Click on advanced
Turn on developer mode
Exit user settings
Click on your profile picture thats near user settings
Click copy user id
Step 29. Click on file and save as
Step 30. Click on file type and then all types.
Step 31. Rename it to your bot's name and .py
Step 32. Save it in the folder thats token.txt is in
Step 33. Delete the BOT.txt (Not BOT.py.)
HOW TO START YOUR BOT:
Step 1. Right click BOT.py
Step 2. Open as python 3.13
Your bot is started! Congrats!
