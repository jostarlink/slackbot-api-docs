# Attachments
[Message attachments](https://api.slack.com/docs/attachments) are one of the greatest features of Slack API. They let you enrich your messages with beautiful formats.
 
 As fun as they might seem, writing attachment objects is not really that easy, sometimes the attachments become a large object which is hard to maintain.
 
 That's why we have an `Attachments` class which helps you create attachment formattings.
 
##Introduction
 The `bot.Attachments` class extends `Array`, so you can treat it just like an array.
 There are methods for most of your formatting needs:
 
 ###good, warning, danger! (and goodOr)
 These methods are aliases for colors `good`, `warning` and `danger`. danger`.
 
 They take the `text` as first parameter and another `params`. By default, the `fallback` value is set to something like: `Good: ${text}`.
 
 ```javascript
   const attachments = new bot.Attachments();
   attachments.good('You look good!');
   //^ { text: 'You look good!', color: 'good', fallback: 'Good: You look good!' }
   
   attachments.good('You look the best!', 
 ```
 
 ####goodOr
 You might wonder what this does. Sometimes you want your bot to either send a success message or show the errors.
 In these cases, you would have to check for some conditions, add errors, and if no error is found, you specify a success message. To make this easier, you can specify a `goodOr` message which is automatically removed if you add another attachment afterwards.
 
 ```javascript
    const attachments = new bot.Attachments();
    attachments.goodOr('Success!');
    
    // some time later, you find an error
    attachments.danger('Oops! Something bad happened.');
    
    console.log(attachments.length); // 1
 ```
 
 For more information see [Attachments#color](https://api.slack.com/docs/attachments#color).
 
 ###image, thumb
 These are pretty similar, they take a `url` and a `params` object.
 Default fallback of these types is `Image: ${url}` or `Thumb: ${url}`.
 
```javascript
   const attachments = new bot.Attachments();
   attachments.image('http://imgur.com/xswer');
```

See [Attachments#image_url](https://api.slack.com/docs/attachments#image_url) and [Attachments#thumb_url](https://api.slack.com/docs/attachments#thumb_url).

###author
Specifies the `author_name`, `author_link` and `author_icon`. Takes parameters for these properties in order.
Default fallback: `Author: ${name}, ${link}, ${icon}`.

```javascript
   const attachments = new bot.Attachments();
   attachments.author('Mahdi Dibaiee', 'http://dibaiee.ir', 'http://gravatar.com/...');
```

###title
Sets the `title` and `title_link` properties.
Default fallback: `Title: ${title}, ${link}`.

```javascript
   const attachments = new bot.Attachments();
   attachments.author('Mahdi Dibaiee', 'http://dibaiee.ir');
```