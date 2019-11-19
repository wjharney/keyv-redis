# @keyvjs/redis [<img width="100" align="right" src="https://raw.githubusercontent.com/keyvjs/keyv/master/media/logo.svg?sanitize=true" alt="keyv">](https://github.com/keyvjs/keyv)

> Redis storage adapter for Keyv

[![Build Status](https://travis-ci.com/keyvjs/redis.svg?branch=master)](https://travis-ci.com/keyvjs/redis)
[![Coverage Status](https://coveralls.io/repos/github/keyvjs/redis/badge.svg?branch=master)](https://coveralls.io/github/keyvjs/redis?branch=master)
[![npm](https://img.shields.io/npm/v/@keyvjs/redis.svg)](https://www.npmjs.com/package/@keyvjs/redis)

Redis storage adapter for [Keyv](https://github.com/keyvjs/keyv).

TTL functionality is handled directly by Redis so no timestamps are stored and expired keys are cleaned up internally.

## Install

```shell
npm install --save @keyvjs/keyv @keyvjs/redis
```

## Usage

```js
const Keyv = require('@keyvjs/keyv');

const keyv = new Keyv('redis://user:pass@localhost:6379');
keyv.on('error', handleConnectionError);
```

Any valid [`Redis`](https://github.com/luin/ioredis#connect-to-redis) options will be passed directly through.

e.g:

```js
const keyv = new Keyv('redis://user:pass@localhost:6379', { disable_resubscribing: true });
```

Or you can manually create a storage adapter instance and pass it to Keyv:

```js
const KeyvRedis = require('@keyvjs/redis');
const Keyv = require('@keyvjs/keyv');

const keyvRedis = new KeyvRedis('redis://user:pass@localhost:6379');
const keyv = new Keyv({ store: keyvRedis });
```

Or reuse a previous Redis instance:

```js
const KeyvRedis = require('@keyvjs/redis');
const Redis = require('ioredis');
const Keyv = require('@keyvjs/keyv');

const redis = new Redis('redis://user:pass@localhost:6379');
const keyvRedis = new KeyvRedis(redis);
const keyv = new Keyv({ store: keyvRedis });
```

## License

MIT © Luke Childs
