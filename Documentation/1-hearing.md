#Hearing
 You want your bots to interact with others and answer questions, your bot must know how to hear and read.
 
 There are three ways to listen on messages, `hear`, `listen` and `command`.
 
 ###hear
  Hearing is the simplest case of hearing, you just enter a room (channel) and hear everything.
  People are not talking to you, but you still hear them, because they are not talking privately (in IM).
  
```javascript
bot.hear(/Who's there?/i, message => {
  message.reply("I am!");
});

let exclamation = 0;
bot.hear(message => {
  // process messages
  if (message.text.endsWith('!')) {
    exclamation++;
  }
  
  if (exclamation > 3) {
    message.reply("What's going on? You're all bumped up!");
    exclamation = 0;
  }
});
```

![OMG! Did you see that?! I just heard it!](hearing-hear.png)

###listen
 Imagine you're reading in a noisy room, you don't bother what people are saying unless they mention your name. In `slackbot-api` world, that's called listening.
 
 When you use this method, the function is called if you're @mentioned or directly messaged.
 
```javascript
'use strict';

const Bot = require('slackbot-api');

const bot = new Bot({ token: 'xoxb-40985785061-cHXNgAqKWILTfO4XfEmxuDVe' });

bot.listen(/Are you okay?/i, async message => {
  message.reply('Why do you even bother asking a robot!?');
});
```

![Bot doesn't answer if I don't mention him!](hearing-listen.png)

###command
 Sometimes you want to define a command with a syntax, or you just want to take some parameter from user, in these situations regex is hard!
