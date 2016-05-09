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
 
```javascript
const msg = await bot.sendMessage('something wrong!');
msg.delete();

// equivalent:
// bot.deleteMessage(msg.channel, msg.ts);
```

###react
This method adds a reaction to a message, it's a shortcut for `bot.react`.

```javascript
bot.hear(/Thank you/i, message => {
  message.react(':pray:');
  
  // equivalent:
  // bot.react(message.channel, message.ts, ':pray:');
});
```

For more information on methods, see [Methods](https://api.slack.com/methods).

##Events
 The events received from Slack API server are not as easy to use, because you'll have to match the received event's message id with your message, so we do that for you.
 
 You can use `on` and `off` methods of messages to set listeners on events.
 
###update
 Triggers when a user updates their message.
 
```javascript
bot.hear(message => {
  message.on('update', () => {
    message.reply('You changed your mind?');
  });
});
```

###delete
 Triggers when a message is deleted.
 
```javascript
bot.hear(message => {
  message.on('delete', () => {
    message.reply('Oooo, looks like someone\'s hiding something');
  });
});
```

###reaction_added
 Triggers when someone adds a reaction to a message.
 
```javascript
const msg = await bot.sendMessage('Who wants me to dance?');
const votes = 0;
msg.on('reaction_added', event => {
  if (event.reaction === 'thumbsup') votes++;
  votes--;
});
```

###reaction_removed
 Triggers when someone removes their reaction from a message.
 
```javascript
const msg = await bot.sendMessage('Who wants me to dance?');
const votes = 0;
msg.on('reaction_added', event => {
  if (event.reaction === 'thumbsup') votes++;
  votes--;
});

msg.on('reaction_removed', event => {
  if (event.reaction === 'thumbsup') votes--;
  votes++;
});
```

For more information on the events, see [Events](https://api.slack.com/events).