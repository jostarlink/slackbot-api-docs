#Sending Messages
> Blessed are those with a voice.
 Okay, so you want to send messages, don't worry, we have you covered.
 
 There are two main methods for sending messages, and two other for updating and deleting messages.
 
 The main method to send a message is `sendMessage`:
 
```javascript
// bot.sendMessage(channel, text, params);
bot.sendMessage('music-recommendation', 'Yeaaaaah!');
bot.sendMessage('joe', 'Hey Joe, how are you?');

bot.sendMessage('general', "I'm pretending to be Joe", { username: 'Joe' });
```

There are three arguments.
`channel` – either name or ID of a channel/group/IM/user, whatever
`text` – self-explanatory

