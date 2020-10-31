# express-json-router

Express router wrapper to send json response

## Installation

```sh
$ npm install express-json-router
```

## Usage

```js
const express = require('express');
const JsonRouter = require('express-json-router');
const router = new JsonRouter();
const clientErrors = JsonRouter.clientErrors;
const app = express();

router.all('/all-route', () => 'all-route');
router.get('/get-route', () => 'get-route');
router.post('/post-route', () => 'post-route');
router.put('/put-route', () => 'put-route');
router.delete('/delete-route', () => 'delete-route');

router
  .route('/route-route')
  .all((req, res, next) => next())
  .get(() => 'route-get-route')
  .post(() => 'route-post-route')
  .put(() => 'route-put-route')
  .delete(() => 'route-delete-route');

router.get(
  '/next',
  (req, res, next) => next(),
  () => 'next-test'
);

router.get('/unauthorized-error', () => {
  throw new clientErrors.UnauthorizedError();
});

app.use('/', router.original).listen();
```

### [MIT Licensed](LICENSE)
