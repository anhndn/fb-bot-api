# Facebook Bot Node API

[![NPM version][npm-image]][npm-url]
[![Downloads][downloads-image]][downloads-url]
[![Dependency Status][david-image]][david-url]
[npm-image]: https://img.shields.io/npm/v/fb-bot-api.svg?style=flat-square
[npm-url]: https://npmjs.org/package/fb-bot-api
[downloads-image]: http://img.shields.io/npm/dm/fb-bot-api.svg?style=flat-square
[downloads-url]: https://npmjs.org/package/fb-bot-api
[david-image]: http://img.shields.io/david/Voronchuk/fb-bot-api.svg?style=flat-square
[david-url]: https://david-dm.org/Voronchuk/fb-bot-api

## Getting Started

Use this library to communicate with the Facebook Messenger API to develop a bot for [Facebook Messenger](http://messenger.com/). Go to [developers.facebook.com](https://developers.facebook.com/docs/messenger-platform/implementation) to learn more and start building a bot.

[`npm install fb-bot-api`][npm-url]

## License 

The Facebook Messenger bot library is released under the terms of the MIT license. See [License](LICENSE.md) for more information or see https://opensource.org/licenses/MIT.

## Process

Sample config:
    
```javascript
var config = {
    WEBSERVER: {
        PORT: 8080,
        PROXY_CONFIG: 'loopback',
        URL_PREFIX: '/facebook'
    },
    FB_MESSAGE_URL: 'https://graph.facebook.com/v2.6',
    VERIFY_TOKEN: '...',
    APP_ID: '...',
    PAGE_ID: '...',
    PROFILE_TOKEN: '...',
    
    MESSAGE_DELIVERY_TRACKING_TIMEOUT: 30000 // Optional settings which enables tracking a delivery of sent messages
};
```

Make bot instance:
```javascript
var FacebookBot = require('fb-bot-api').Facebook;

var instance = new FacebookBot(config);
instance.on('message', function (sender, message) {
    ...
});
instance.on('message-image', function (sender, imageUrl) {
    ...
});
instance.on('message-postback', function (sender, postback) {
    ...
});
instance.on('error', function (error) {
    ...
});

// If MESSAGE_DELIVERY_TRACKING_TIMEOUT is set
instance.on('message-delivered', function (sender, signature) {
    ...
});

this.instance.listen();


// Welcome message
this.instance.bot.setWelcome('Hello world!');
this.instance.bot.setWelcome('Hello world!', [
    {
        type: 'postback',
        label: 'Start'
    },
    {
        type: 'postback',
        label: 'End'
    }
]);

// Normal messages with and without links
this.instance.bot.sendText(facebookUserId, 'Some message');
this.instance.bot.sendText(facebookUserId, 'Some message', [
    {
        type: 'postback',
        label: 'Answer'
    },
    {
        type: 'web_url',
        label: 'Google',
        content: 'https://google.com'
    }
]);

// Image messages
this.instance.bot.sendImage(facebookUserId, 'https://images.google.com/images/branding/googlelogo/2x/googlelogo_color_272x92dp.png');
this.instance.bot.sendImage(facebookUserId, '/local/path/to/file.png');
```

By default the system initialise Express 4 web-server instance to listen for FB Messenger webhook messages, if thats an overkill for you can pass custom web-server engine as the second param of FacebookBot constructor, like `new FacebookBot(config, express())`.

## Diclaimer

This library is still early in it's development, lacks tests and features, so use on your own risk. 