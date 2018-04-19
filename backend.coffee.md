Redis backend compatible with abrasive-ducks
--------------------------------------------

    redis_backend = (options) ->
      redis = new Redis options

      (sources) ->

Messages from the bus to the client are sent on the subscription channels.

        sources
        .continueWith ->
          redis.disconnect()
          most.empty()
        .forEach (msg) ->
          redis.publish (msg.key ? msg.id), msg

Messages from the clients to the bus are received on the `msg` channel.

        redis.subscribe 'msg'
        most
        .fromEvent 'msg', redis
        .map ([_,msg]) -> msg

    module.exports = redis_backend
    Redis = require 'ioredis'
