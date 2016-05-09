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
 This method updates the message, it's a shortcut for `bot.updateMessage`.
 
```javascript
bot.command('count from <number>', async message => {
  let [num] = message.match;
  num = parseInt(num, 10);
  const msg = await message.reply(num);
  
  setInterval(() => {
    msg.update(--n);
    
    // equivalent:
    // bot.updateMessage(msg.channel, msg.ts, --n);
  }, 1000);
});
```

###delete
 This method deletes the message, it's a shortcut for `bot.deleteMessage`.

###react
This method adds a reaction to a message, it's a shortcut for `bot.react`.

```javascript
bot.hear(/Thank you/i, message => {
  message.react(':pray:');
  
  // equivalent:
  // bot.react(message.channel, message.ts, ':pray:');
});
```