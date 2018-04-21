# how to develop middleware


## middleware template
```js
/* ./middleware/logger-async.js */
function log( ctx ) {
  console.log( ctx.method, ctx.header.host + ctx.url )
}

module.exports = function () {
  return async function ( ctx, next ) {
    log(ctx);
    await next();
  }
}
```


## how to use:
```js
const Koa = require('koa'); // koa v2
const loggerAsync  = require('./middleware/logger-async');
const app = new Koa();

app.use(loggerAsync());

app.use(( ctx ) => {
    ctx.body = 'hello world!'
});

app.listen(3000);
console.log('the server is starting at port 3000');
```
