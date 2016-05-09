
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
 When trying to read some parameter from the user, regexes look weird and hard to understand.
 That's why we have `command`, a way to listen on messages with the ability to read parameters with a cleaner syntax.
 
 Take a look at an example, then I'll explain it for you.
 
```javascript
bot.command('Say <string>', message => {
  const [str] = message.match;
  
  message.reply(str);
});

// equivalent regex: /Say (.*)/gim
```

Damn, that's much more understandable than the equivalent regular expression.

The rules are:

* Parentheses `()`: passive, non-capturing groups `(?:expression)`
* Tags `<>`: required, capturing groups `(expression+)`
* Brackets `[]`: optional, capturing groups `(expression*)`
* Types: You can either put a word, or a type inside (), [] and <>, types are as follows:
  * string: anything, `.`
  * number: digits, `\d`
  * alphanumeric: digits and alphabet, `[A-Za-z0-9]`
  * alphabet: alphabet, `[A-Za-z]`
  * word: `\w`
  * char: `\S`
* Spaces, tabs and anything matching `\s` is replaced with `\s*`, making it optional
* The `gim` flags are enabled for all `command`s

Here are some examples to give you more insight of what can be done using this syntax:

```javascript
bot.command('buy <char> [string]', message => {
  const [user, item] = message.match;
  
  message.reply(`I'll buy ${item} for ${user} and deliver it at 10pm.`);
});

bot.command('I love [string] music', message => {
  const [genre] = message.match;
  
  switch (genre.trim().toLowerCase()) {
    case 'metal':
    case 'rock':
      message.reply('Hell yeah!');
      break;
    case 'rap':
    case 'hip hop':
      message.reply('Only god can judge me.');
      break;
    case '':
      message.reply('Who doesn\'t?!');
      break;
    default:
      message.reply('I\'ll keep that in mind!');
  }
});
```

![Me: I love music! Bot: Who doesn't?, Me: I love rock music Bot: Hell yeah!, Me: I love hip hop music Bot: Only god can judge me, Me: I love funk music Bot: I'll keep that in mind](hearing-command-music.png)
