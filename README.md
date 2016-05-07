# Introduction
 Hey! This is an introduction to `slackbot-api`, this introduction will get you started with writing a simple Slack Bot, and no, it's not hard!

###Slack Side
 Okay, first things first, we have to create a bot in our Slack Team (if you don't have a slack team, [create one](https://slack.com/)).

To do so, open [Custom Integrations](https://pichak.slack.com/apps/manage/custom-integrations), click **Bots** and **Add configuration**, enter a name (You can just go with Sibe) and done. In the next page, upload an image for your bot (Sibe's avatar!) or choose an emoji. You also find an **API Token** there, that's how you connect to your bot, you need it for the next step!

###Breathing life into your bot
 Now's the time when your bot actually does something.
 Initialize a project:
```bash
 mkdir bot
 cd bot
 npm init
 npm install slackbot-api
```
