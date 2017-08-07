[![Build Status](https://travis-ci.org/Colored-Coins/request-id.svg?branch=master)](https://travis-ci.org/Colored-Coins/request-id)
[![Coverage Status](https://coveralls.io/repos/github/Colored-Coins/request-id/badge.svg?branch=master)](https://coveralls.io/github/Colored-Coins/request-id?branch=master)
[![npm version](https://badge.fury.io/js/cc-request-id.svg)](https://badge.fury.io/js/cc-request-id)
# request-id
Express.js request-id middleware.<br>
Generates and sets a new request UUID in each request header (by default in `request-id` header).<br>
Generates and sets a new correlation UUID if not already exists (by default in `correlation-id` header).<br>
Responds with the remote ID if given (allows server clients to pass their own identifier).<br>
Encapsulates an HTTP client ([request](https://github.com/request/request)) within the request object as `req.service.request` which by default will pass forward the remote ID (if given) and the correlation ID headers.
## Installation
```sh
$ npm install cc-request-id
```
## Running the tests
```
$ npm install
$ mocha
```
## API
```javascript
var requestId = require('cc-request-id')
```
### requestId(options)
Create new request-id middleware.
#### options
See [request-id options](https://github.com/wilmoore/request-id.js#options).
Exception:
Default value generator function: [uuidv4fast]

## Example
```javascript
var express = require('express')
var app = express()
var requestId = require('cc-request-id')
var bodyParser = require('body-parser')

app.use(requestId())
app.use(bodyParser())
app.get('/test', function (req, res, next) {
	res.status(200).send({
		requestId: req.headers['X-Request-Id']
	})
})
app.listen(8080)
```
test it:
```
curl http://localhost:8080/test
```
outputs:
```
requestId: 32fd0631-5a10-4564-b8c7-f704be22f13a
```

## License

[MIT](license)

[uuidv4fast]:   https://github.com/scravy/uuid-1345#uuidv4fast
