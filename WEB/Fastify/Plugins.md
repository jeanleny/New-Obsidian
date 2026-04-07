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

