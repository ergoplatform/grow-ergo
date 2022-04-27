## Bridging Chats

All ecosystem projects are welcome to a channel that is bridged between their server/telegram using [matterbridge](https://github.com/42wim/matterbridge). See #ergodex, #sigmavalley or #comet on the Ergo Discord for examples of this in action.

Follow these simple steps to get bridged;

**1.** Invite @BridgeBot#9505 to your server using [this invite link](https://discordapp.com/oauth2/authorize?&client_id=910495131646455808&scope=bot&permissions=536870912)

> You can set up your [your own bot](https://github.com/42wim/matterbridge/wiki/Discord-bot-setup) but will need to send @Glasgow the `Token` ID if you want it bridged to existing ergo chats. **You only need to grant the bot the ability to see/read messages and set webhooks in the channel you want to bridge.** 

**2.** Invite [ErgoBridgeBot](https://t.me/ErgoBridgeBot) to your Telegram

> You'll need to use `/allowInvitingBots` if Shieldy is enabled.  

**3.** Tag @Glasgow and let him know what channel/server you want to be bridged so it can be added to the configuration. 

**Limitations**:
- Discord doesn't give bots the ability to reply to messages when spoofing someone. 
  - Still working on making this prettier, currently, the username is repeated. (Set by `QuoteFormat` in the config below).
  - [Allow webhooks to use reply messages#3282](https://github.com/discord/discord-api-docs/discussions/3282)
- [Telegram API doesn't report deleted messages](https://github.com/42wim/matterbridge/wiki/FAQ#matterbridge-is-not-deleting-messages-from-telegram-to-other-bridges). This means any spam deleted on Telegram will remain on Discord.  
   - **Workaround**: New Telegram users should be restricted from speaking until verifying. Shieldy or [OrgRobot](http://orgrobot.io/) work best here. 

Other than that, works pretty well. 
- Names/profile-photos will be spoofed if they're set and the names are similar. (I can also map names manually). But the profile photos need to be re-cached when a new bridge is added. 
- Responses will reply to the message on both platforms so people will see notifications. 

### Config

Example config `bridge.toml`

```
# / 
# SERVERS
# / 
[telegram]
    [telegram.mytelegram]
        Token="REDACTED"
        RemoteNickFormat="<{NICK}> "
        MessageFormat="HTMLNick: "
        QuoteFormat="re @{QUOTENICK}: {QUOTEMESSAGE} \n \n {MESSAGE}"
        QuoteLengthLimit=46
        ReplaceNicks=[
            ["Daniumy","dann"], 
            ["tortodelivery","Torto"],
            ["C4lculista","JOFLITO"],
            ["kushti_ru","kushti"],
            ["Ile","Vesi Hiisi"],
            ["bennykonan","bennyk2"],
            ["TheRealErgoGod","J - The Ergod"],
            ["ergomergoadargo","Jεnniε D"],
            ["mewtoshi","Satergo"],
            ["Rlabs","REROLABS"],
            ["FlyingSheep1","flyingsheep"],
            ["erdoge1","max"],
            ["gilgaMesh_98","gilgaMesh"],
            ["MaSter_vierolean","Vierolean"],
            ["大鎧"," ERGYOROI | 大鎧 | ergyoroi.com"],
            ["seedubya","CW"]
            ]
            
            IgnoreMessages="^/ https://t.me @everyone @here 100x 💎 ⚡️ ✅ 🚀 👈 👇 😱 ✍️  elon pump 🎉 🎊 😳 🤗 airdrop"


[discord]
    [discord.mydiscord]
        Token="REDACTED" 
        Server="668903786361651200" # picked from guilds the bot is connected to
        RemoteNickFormat="{NICK}"
        AutoWebhooks=true
        UseLocalAvatar=["telegram"]
        IgnoreMessages="@everyone @here"
        PreserveThreading=false
    
    [discord.cometdiscord]
        Token="REDACTED" 
        Server="937354367340789771" # picked from guilds the bot is connected to
        RemoteNickFormat="{NICK}"
        AutoWebhooks=true
        UseLocalAvatar=["telegram"]
        IgnoreMessages="@everyone @here"
        PreserveThreading=false

    [discord.sigmavalley]
        Token="REDACTED" 
        Server="905938516276559952" 
        RemoteNickFormat="{NICK}"
        AutoWebhooks=true
        UseLocalAvatar=["telegram"]
        IgnoreMessages="@everyone @here"
        PreserveThreading=false

    [discord.ergodex]
        Token="REDACTED" 
        Server="881237412628533258" 
        RemoteNickFormat="{NICK}"
        AutoWebhooks=true
        UseLocalAvatar=["telegram"]
        IgnoreMessages="@everyone @here"
        PreserveThreading=false



[matrix.mymatrix]
    Server="https://matrix.org"
    Login="ergobridge"
    Password="REDACTED"
    RemoteNickFormat="[{PROTOCOL}] <{NICK}> "


# / 
# GATEWAYS
# / 

[[gateway]]
name="support"
enable=true

    [[gateway.inout]]
    account="telegram.mytelegram"
    channel="-1001327051344"

    [[gateway.inout]]
    account="discord.mydiscord"
    channel="❓│support"

[[gateway]]
name="Agora"
enable=true

    [[gateway.inout]]
    account="telegram.mytelegram"
    channel="-1001474698940"

    [[gateway.inout]]
    account="discord.mydiscord"
    channel="🏛│agora"

    [[gateway.inout]]
    account="matrix.mymatrix"
    channel="#ergoagora:matrix.org"

[[gateway]]
name="Indonesian"
enable=true

    [[gateway.inout]]
    account="telegram.mytelegram"
    channel="-1001212963159"

    [[gateway.inout]]
    account="discord.mydiscord"
    channel="🇮🇩│indonesian" 

[[gateway]]
name="sigmavalley"
enable=true

    [[gateway.inout]]
    account="telegram.mytelegram"
    channel="-1001521807237"

    [[gateway.inout]]
    account="discord.mydiscord"
    channel="sigmavalley" 

    [[gateway.inout]]
    account="discord.sigmavalley"
    channel="🌈│townhall" 


[[gateway]]
name="ergodex"
enable=true

    [[gateway.inout]]
    account="telegram.mytelegram"
    channel="-1001149832351"

    [[gateway.inout]]
    account="discord.mydiscord"
    channel="ergodex"

    [[gateway.inout]]
    account="discord.ergodex"
    channel="telegram-bridge"
```