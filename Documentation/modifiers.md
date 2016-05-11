# Modifiers
 To increase flexibility of `slackbot-api` we wanted to allow developers to modify the behavior of methods.
 Modifiers give you three ways to modify a method:
 
 * Pre-process: Using pre-processors you can manipulate the arguments of a function.
 * Post-process: Using post-processors you get the ability to manipulate the output (return value) of a function
 * Middlewares: As you might be already familiar, middlewares let you modify a function's actual behavior. You can modify parameters, halt the function or just pass it to the next middleware.


Modifiers are explained in details below:

##Introduction
 Modifiers are registered through `bot.modifiers`, which includes the methods `preprocess`, `postprocess` and `middleware`.
 
 Each method of `slackbot-api` can be modified through modifiers. An example looks like this:
 
 ```javascript
bot.modifiers.preprocess('listen', (pattern, fn) => {
  if (typeof pattern === 'string') {
    let regex = new RegExp(pattern);
    return [regex, fn];
  }

  return [pattern, fn];
});
 ```
 
 This simple preprocessor above gives you the ability to use `.listen` with `string` instead of Regular Expressions.
 
 Each modifier returns an `id` which can later be used to remove the modifier using `bot.modifiers.remove`.
 
##Preprocess
Preprocessors take the arguments of the specified function, and you should return an array of arguments which are passed to the function.

```javascript
bot.modifiers.preprocess('listen', (pattern, fn) => {
  if (pattern === '*') {
    return [/./, fn];
  }
  
  return [pattern, fn];
});
```

##Postprocess
Postprocessors take the return value of a function, and their return value is then returned from the original function.

```javascript
bot.modifiers.postproess('listen', (bot) => {
  return bot.users[bot.users.length - 1]; // I have no idea why either :D
});
```

##Middlewares
Middlewares let you modify important parameters of a function and decide whether the function should proceed or not.

Middlewares must return a promise which, if rejected stops the function from proceeding, else proceeds to the next middleware until all middlewares are processed.

```javascript
bot.modifiers.middleware('hear', params => {
  const admins = params.admins || [];
  const name = bot.find(params.user).name;
  
  if (admins.includes(name)) return Promise.resolve();
  
  return Promise.reject();
});
```

Okay, let's go through the code above step by step.
First we register a middleware on `hear`, please note that `listen` just calls `hear` with the `mention: true` parameter which requires the bot to be mentioned, so they both go through this middleware.
Then we're reading `params.admins`, you might wonder what that means. Almost all methods accept a `params` as their last argument, as listen and hear do. Take a look:

```javascript
  listen(regex, listener, params = {}) {
    params.mention = true;

    return this.hear(regex, listener, params);
  }
```

Here, it means the user can specify an `admins` array on `listen` calls, like so:

```javascript
bot.listen(/sudo/, message => {
  message.reply('As you command!');
}, { admins: ['mahdi', 'admin'] });
```

This way, middlewares become even more flexible, they can read parameters from the user.
Let's continue with our function: After reading the `admins` array, we match the user sending us the message with the admins array. If the user is an admin, let the function proceed (in this case calling event listeners), otherwise, break the chain.


The example above is a simplified version of [`bolt-permissions`](https://github.com/slack-bolt/bolt-permissions) which includes usergroups and such.