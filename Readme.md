
# alopu-socket.io-parser

[![Build Status](https://secure.travis-ci.org/socketio/socket.io-parser.svg?branch=master)](http://travis-ci.org/socketio/socket.io-parser)
[![NPM version](https://badge.fury.io/js/socket.io-parser.svg)](http://badge.fury.io/js/socket.io-parser)

A simple modification of the standard socket.io-parser which supports Circular Stringification with use of [circular-json](https://github.com/WebReflection/circular-json) by [Web Reflection](https://github.com/WebReflection)

A socket.io encoder and decoder written in JavaScript complying with version `3`
of [socket.io-protocol](https://github.com/socketio/socket.io-protocol).
Used by [socket.io](https://github.com/automattic/socket.io) and
[socket.io-client](https://github.com/automattic/socket.io-client).

## Parser API

  socket.io-parser is the reference implementation of socket.io-protocol. Read
  the full API here:
  [socket.io-protocol](https://github.com/learnboost/socket.io-protocol).

## Example Usage

### Encoding and decoding a packet

```js
var parser = require('alopu-socket.io-parser');
var encoder = new parser.Encoder();
var packet = {
  type: parser.EVENT,
  data: 'test-packet',
  id: 13
};
encoder.encode(packet, function(encodedPackets) {
  var decoder = new parser.Decoder();
  decoder.on('decoded', function(decodedPacket) {
    // decodedPacket.type == parser.EVENT
    // decodedPacket.data == 'test-packet'
    // decodedPacket.id == 13
  });

  for (var i = 0; i < encodedPackets.length; i++) {
    decoder.add(encodedPackets[i]);
  }
});
```

### Encoding and decoding a packet with binary data

```js
var parser = require('alopu-socket.io-parser');
var encoder = new parser.Encoder();
var packet = {
  type: parser.BINARY_EVENT,
  data: {i: new Buffer(1234), j: new Blob([new ArrayBuffer(2)])}
  id: 15
};
encoder.encode(packet, function(encodedPackets) {
  var decoder = new parser.Decoder();
  decoder.on('decoded', function(decodedPacket) {
    // decodedPacket.type == parser.BINARY_EVENTEVENT
    // Buffer.isBuffer(decodedPacket.data.i) == true
    // Buffer.isBuffer(decodedPacket.data.j) == true
    // decodedPacket.id == 15
  });

  for (var i = 0; i < encodedPackets.length; i++) {
    decoder.add(encodedPackets[i]);
  }
});
```
See the test suite for more examples of how socket.io-parser is used.


## License

MIT
