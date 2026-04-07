In Fastify, everything is a plugin.
Routes, hooks, decorators, middleware. A plugin is just a **function with this signature**.
```js
async function myPlugin(fastify, options) {
  console.log("franchement le web au secours envie de démarrer un maximum de scooter 50 CC débridés pour taper des rétros")
}
```

Then you register it with the register function
```js
fastify.register(myPlugin, { someOption: 'value' })
```

When you register a plugin, Fastify creates a new fastify context.
Anything declared in this context stays in it. You cant use things delcare in this context, **unless you explicitly expose it** .

You can do this by using the **'fastify-plugin'** wrappers.
It breaks encapsulation and makes things global.
```ts
import Fastify from 'fastify'
import fp from 'fastify-plugin' //dont forget to install fastify plugin with npm

fastify.register(fp(async (scope) => { //the fp near async wraps the plugins at the root of the fastify instance and makes it global
  scope.decorate('bla', (str: string) => { 
    console.log(str)
  })
}))
```
