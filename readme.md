# Http Exception Handler

## Description

Handles express.js app http exceptions.

## Install

```bash
$ npm install httpexceptions
```

## Example

```javascript
const HttpExceptions = require('httpexceptions');
const express        = require('express');

/* create express app */
const app = express();

/* define an app endpoint */
app.get('/', (req, res) => {
    throw new HttpExceptions.NotImplementedHttpException('This method is not implemented yet');
});

/* handle exceptions */
app.use((err, req, res, next) => {
    /* http exceptions handling */
    if (err instanceof HttpExceptions.HttpException) {
        return res.status(err.getStatusCode()).json(err.getMessage() ? {message: err.getMessage()} : {});
    }

    /* other errors */
    res.sandStatus(500);
});
```

OR

```javascript
const HttpExceptions = require('httpexceptions');
const express        = require('express');

/* create express router  */
const router = new express.Router();

/* define an endpoint */
router.get('/', (req, res, next) => {
    return next(new HttpExceptions.NotImplementedHttpException('This method is not implemented yet'));
});

/* create express app */
const app = express();

/* use router */
app.use(router);

/* handle exceptions */
app.use((err, req, res, next) => {
    /* http exceptions handling */
    if (err instanceof HttpExceptions.HttpException) {
        return res.status(err.getStatusCode()).json(err.getMessage() ? {message: err.getMessage()} : {});
    }

    /* other errors */
    res.sandStatus(500);
});
```