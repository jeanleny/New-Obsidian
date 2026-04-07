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
1. The name of the decorator
2. The value passed in the decorator
3. The dependency (the actual logic)

This will add the utility function on the fastify instance object as a method.
```js
fastify.register((instance, opts, done) => {
  instance.decorate('util', (a, b) => a + b)
  console.log(instance.util('Nom de merde serieux ', 'Autant lappeler silo a grain, papier peint, range rover d lespace'))

  done()
})
```
Like registering plugins Decorate functions with the instance scope.

We can also put whole function return in the dependencies to keep code clean.
