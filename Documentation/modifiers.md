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

Middlewares must return a promise which, if rejected stops the function from proceeding, else proceeds to the next middleware.

```javascript
const admins = ['mahdi', 'admin'];
bot.modifiers.middleware('hear', params => {
  const name = bot.find(params.user).name;
  if (admins.includes(name)) return Promise.resolve();
  
  return Promise.reject();
});
```
