RocketMQ-Nodejs-client
=======

[![NPM version][npm-image]][npm-url]
[![build status][travis-image]][travis-url]
[![David deps][david-image]][david-url]
[![node version][node-image]][node-url]

[npm-image]: https://img.shields.io/npm/v/ali-ons.svg?style=flat-square
[npm-url]: https://npmjs.org/package/ali-ons
[travis-image]: https://img.shields.io/travis/ali-sdk/ali-ons.svg?style=flat-square
[travis-url]: https://travis-ci.org/ali-sdk/ali-ons
[david-image]: https://img.shields.io/david/ali-sdk/ali-ons.svg?style=flat-square
[david-url]: https://david-dm.org/ali-sdk/ali-ons
[node-image]: https://img.shields.io/badge/node.js-%3E=_4.2.3-green.svg?style=flat-square
[node-url]: http://nodejs.org/download/

RocketMq Open Notification Service Client (base on opensource project [RocketMQ](https://github.com/ali-sdk/ali-ons))

Sub module of [ali-sdk](https://github.com/ali-sdk/ali-sdk).

## Install

```bash
npm install ax-rocketmq --save
```

## Usage

consumer

```js
'use strict';

const httpclient = require('urllib');
const Consumer = require('ax-rocketmq').Consumer;
const consumer = new Consumer({
  httpclient,
  consumerGroup: 'your-consumer-group',
  namesrvAddr: 'your-namesrv-address'
  // isBroadcast: true,
});

consumer.subscribe(config.topic, '*', async msg => {
  console.log(`receive message, msgId: ${msg.msgId}, body: ${msg.body.toString()}`)
});

consumer.on('error', err => console.log(err));
```

producer

```js
'use strict';

const httpclient = require('urllib');
const Producer = require('ax-rocketmq').Producer;
const Message = require('ax-rocketmq').Message;

const producer = new Producer({
  httpclient,
  producerGroup: 'your-producer-group',
  namesrvAddr: 'your-namesrv-address'
});

producer.ready(() => {
  console.log('producer ready');
  const msg = new Message('your-topic', // topic
    'TagA', // tag
    'Hello ONS !!! ' // body
  );

  producer.send(msg, (err, sendResult) => console.log(err, sendResult));
});
```

## License

[MIT](LICENSE)
