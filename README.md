# simple-test-server
[![js-happiness-style](https://img.shields.io/badge/code%20style-happiness-brightgreen.svg)](https://github.com/JedWatson/happiness)

Simple server responds to any HTTP request with details about the request.

## Install
```javascript
npm install @streammedev/simple-test-server;
```

## Usage
First, import the class:
```javascript
import SimpleTestServer from '@streammedev/simple-test-server';
```
Next, instantiate it:
```javascript
const server = new SimpleTestServer();
```
Next, start it:
```
server.start();
```
Your server is now accepting requests at `http://localhost`.

Once you're done, stop the server by calling `stop`, ie:

```javascript
server.stop();  
```

## API
`constructor(port)` - Instantiates a new server instance on the specified (optional) port. Whether it is set explicitly or not, server.port will be set to the port once the server has started.

`start(cb)` - Starts the server, then calls the (optional) callback.

`stop(cb)` - Stops the server, then calls the (optional) callback.

## Example
```javascript
import SimpleTestServer from '@streammedev/simple-test-server';
import assert from 'assert';
import request from 'request';

describe('do some test', function () {
	let testServer;
	before(function (done) {
		testServer = new ApiTestServer(port);
		testServer.start(done);
	});
	after(function (done) {
		testServer.stop(done);
	});
  it('should get my endpoint', function(done) {
    request('http://localhost/my-endpoint?q=findme', function (error, response, body) {
      assert.ifError(error);
      assert.ifError(response.statusCode !== 200);
      assert.strictEqual(body.method, 'GET', 'it should be a GET request');
      assert.strictEqual(body.path, 'my-endpoint', 'it should have the right path');
      assert.strictEqual(body.query.q, 'findme', 'it should set the q query parameter');
      })
    })
  })
}
```
