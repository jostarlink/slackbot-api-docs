# Utilities
 We provide some commonly used and useful utilities you probably need when creating a bot.
 
 

###find
 Probably the most useful method you'll need is `find`, with this method you can find a user, channel, bot, group or IM.
 This method accepts both Slack IDs and names, and either returns the object you're looking for or `null`.
 
```javascript
bot.listen(/Hello/i, message => {
  const user = bot.find(message.user);
  
  message.reply(`Hello ${user.profile.first_name}!`);
});
```

###random
 You don't want your bot to sound boring, that's why responding with random messages is a common thing in the bot world.
 
 This method selects one of the arguments with an equal chance.
 
```javascript
bot.listen(/Hello/i, message => {
  message.reply(bot.random('Hi', 'Hello', 'Hey'));
});
```

###emojis
 Calls [`emoji.list`](https://api.slack.com/methods/emoji.list), returning the list of emojis available.
 
###icon
 Sets the bot's icon, can be an emoji or a url.
 
```javascript
bot.icon(':fist');
bot.icon('http://some.url/image.png');
```

###call
 We do provide methods for all Slack API methods through `bot.api`, but you can also use this method to call Slack methods manually.
 
```javascript
// possible use case
const c = 'channels' || 'ims';
bot.call(`${c}.history`);
```