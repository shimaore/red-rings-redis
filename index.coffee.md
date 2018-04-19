Client for a Redis red-ring (typically used on a backend application)
---------------------------

    {RedRing} = require 'red-rings'

    class RedRingRedis extends RedRing

      constructor: (options) ->
        super()
        @redis = new Redis options
        return

      disconnect: ->
        @redis.disconnect()

Messages from the client to the bus are sent on the `msg` channel.

      send: (msg) ->
        @redis.publish 'msg', msg

Messages from the bus to the client are sent on the subscription channel.

      source_of: (key) ->
        most
        .fromEvent key, @redis
        .map ([_,msg]) -> msg

      subscribe: (key) ->
        @redis.subscribe key
        super key

      unsubscribe: (key) ->
        @redis.unsubscribe key
        super key

    module.exports = RedRingRedis
    Redis = require 'ioredis'
