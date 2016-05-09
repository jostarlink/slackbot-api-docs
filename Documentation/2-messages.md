#Messages
 Message objects provide useful methods and events to make your life easier.
 
##Methods
 Messages have four methods:
 
 ###reply
  As you've probably already seen in the examples, this method sends a reply to a message.
  Slack doesn't have real _reply_ s, as Telegram does, so this method just sends a message to the same channel as the message.
  
```javascript
bot.listen(/Turn on coffee machine/i, message => {
  message.reply('Consider it done!');
  
  // equivalent:
  // bot.sendMessage(message.channel, 'Consider it done!');
});
```

###update
 This method updates the message, it's just a shortcut for `bot.updateMessage`.
 
```javascript
bot.command('count from <number>', async message => {
  const msg = await message.reply(
});
```