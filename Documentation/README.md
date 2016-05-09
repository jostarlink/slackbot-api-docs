#Documentation
 Here you find the `slackbot-api` documentation, we've tried to make the documentation as simple as possible.
 
 Before we begin explaining custom methods and events defined by `slackbot-api`, you should now, all the original methods and events are available.
 
[ Slack methods](https://api.slack.com/methods/) are avaialble through `bot.api`:
 
```javascript
bot.api.channels.setTopic({ channe: 'general', topic: 'Let\'s have some fun!' });
```

[ Slack events](https://api.slack.com/events) are also available, you can just listen to all events using `on` and remove them using `removeListener`.
 
 There is an exception with the `message` event, the `message` event is only for messages with `type: message`. For the original `message` event, use `raw_message`.
 
 Also, all message `sub_type`s can be listened on directly, see [Message subtypes](https://api.slack.com/events/message#message_subtypes).
 
```javascript
bot.on('message', message => {

});

bot.on('channel_join', event => {

});
```