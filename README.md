# GroupAgree Bot
The [@groupagreebot](https://t.me/groupagreebot) is an advanced poll bot for Telegram. It features fully customizable polls for organizing your group chats and keeping the spam to a minimum.

An example: You want to hang out with your friends, but don't know when they are free? Normally, you would just ask when to meet, resulting in dozens of messages being send and staying on top of it getting out of hand. So, instead of whipping out the old pen and paper and counting people by hand, just ask the GroupAgree Bot kindly to do that for you:

![Screenshot](https://telegra.ph/file/ab7f9a071c55c4d42b1b2.png)
 
Just try it out yourself: Visit https://telegram.me/groupagreebot
 
The **license** for this project is AGPLv3, please read the license file in this repo before modifying or cloning this repo.

# Quick start using Docker:

### 1. Clone this Git repo, install [Docker](https://docs.docker.com/install/) and [Docker-compose](https://docs.docker.com/compose/install/)

### 2. Create a new bot through [@botfather](https://t.me/botfather)
    /newbot
    Group Agree Test  (your displayed bot name here)
    groupagreetestbot   (your bot username here)
    
    /setinline
    @groupagreetestbot
    Search polls...
    
    /setinlinefeedback
    @groupagreetestbot
    Enabled
    
    /setjoingroups
    @groupagreetestbot
    Disable
    
    /setcommands
    @groupagreetestbot
    
    start - 📝 Create a new poll
    list - 📋 List all polls
    cancel - 🚫 Cancel the current operation
    help - ℹ️ Get help
    lang - 🗣Change language

### 3. Specify your bot id and token in `groupagreebot_database_05_05_2019.sql`
    INSERT INTO `instances` VALUES (
            **BOT_ID_HERE**, '**BOT_TOKEN_HERE**',
            '{\"id\":1333337,\"first_name\":\"John\",\"username\":\"johndoe\"}',
            0,0,'2019-01-01 00:00:00',0,'[]',NULL
    );

### 4. Run!
    docker-compose up --build -d --scale adminer=0
    
    (on first run bot might come alive in 20 seconds or so because of MySQL initialization)

## Debugging Docker setup

### Looking at logs, Start/Stop
Bot logs: `docker-compose logs -f` — you should see "beacon ..." line for every message your bot receives.

Bot containers will restart automatically on system reboot, alongside Docker daemon.  
Manual stop: `docker-compose stop`  
Manual start: `docker-compose start db groupagree`

### Accessing the database
    docker-compose up adminer
    # access web interface at http://your-ip:8080/, username: gab, password: gab
    Ctrl-C or `docker-compose stop adminer` when you're finished

### Database backup and restore
Backup: `docker-compose exec -T db mysqldump -ugab -pgab groupagreebot_beta > backup.sql`

Restore: re-create the containers from scratch, replacing `groupagreebot_database_05_05_2019.sql` with your `backup.sql` 

### Containers teardown and cleanup
To remove all containers and data (!): `docker-compose down -v --rmi local`


# How to set it up manually:

**You need**

Xamarin Studio / MonoDevelop: http://www.monodevelop.com/download/ (or another C# IDE)

(For Windows: .NET 4.5.X Developer Pack https://www.microsoft.com/net/targeting)

MySQL: https://dev.mysql.com/downloads/

JSON.NET: http://www.newtonsoft.com/json (should be integrated by now through nuget tho)

**Setup**

This is a C# project, so you need mono for non Microsoft operating systems or .NET 4.5 (or higher) for Windows to run it.

Start by installing Xamarin / MonoDevelop and MySQL.

Set you bot up through [@botfather](https://t.me/botfather).
	Allow inline queries, disable groups and set inline query feedback to 100%.

Use the chat id as mysql username and the key as password (format: chat_id:botkey, like `1122334455:AABBCCDDEEFFGG11223344`).
	This is to make multiple instances on one machine possible.

__Temporary solution for the db layout__
Modify [this script](groupagreebot_v_4_0_database.sql) for the use with your bot (replace bot_chat_id with your bots chat id).

Start Xamarin / MonoDevelop (maybe you need to install the version control addon, but Xamarin/MonoDevelop should prompt you)

Go to Version Control and select Checkout, add this repo (or your fork ;D, seriously) and Checkout, now you should have the source code ready and imported in your IDE.

Modify the file GroupAgreeBot/Globals.cs with your bot key and name (I currently have three configurations, just use Debug for a local instance) and optionally WJClubBotFrame/Notifications.cs with your logging bots api key and your logging chats chat id (can be yours or any other chat, you just have to add the bot to it)

Now **release your source code** (seriously, once you start the bot you have to release the source code, read the license)

Click start in your IDE and you should be good to go, your bot should be up and running :D

Any questions or concerns, ask in [@groupagreebotdevelopment](https://t.me/groupagreebotdevelopment) or pm us [@wjclub](https://t.me/wjclub)
If you found bugs, want to contribute to this project etc, use GitHubs features, we love to see them in action. (And have no fear, we won't laugh at you for stupid issues)
	
	

**Happy polling**

browny99, the guy who wrote this whole piece of dark art
