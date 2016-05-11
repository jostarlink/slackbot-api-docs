# Attachments
 Message attachments are one of the greatest features of Slack API. They let you enrich your messages with beautiful formats.
 
 As fun as they might seem, writing attachment objects is not really that easy, sometimes the attachments become a large object which is hard to maintain.
 
 That's why we have an `Attachments` class which helps you create attachment formattings.
 
##Introduction
 The `bot.Attachments` class extends `Array`, so you can treat it just like an array.
 There are methods for most of your formatting needs:
 
 ###good, warning, danger! (and goodOr)
 These methods are aliases for `color: good | warning | danger`.
 
 They take the `text` as first parameter and another `params`. By default, the `fallback` value is set to: `Good: ${text}`.
 
 ```javascript
   
 ```