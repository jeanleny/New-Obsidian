Decorators are function utilities that only has to be declared once in a fastify instance.

If you want to declare a small utility you declare like this :
```js
// your-awesome-utility.js
module.exports = function (a, b) {
  return a + b
}
```
Then you call register to keep it in an object:
```js
const util = require('./your-awesome-utility')
console.log(util('Decorators ?', 'serieusement ?'))
```

And now we will import this utility in every file we need it in. So we have to call import each time.

Decorators are the elegant way to do this.
```js
fastify.decorate('util', (a, b) => a + b)
```
This function takes three parameters.
