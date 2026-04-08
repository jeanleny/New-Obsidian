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

BUT WAIT,
Fastify has a type script support but you need to know a few things before.
Since you have to type everything, you'll need to declare it as a variable that is equal to to the content of the plugin.
like so :
```ts
const linker: FastifyPluginAsync = async (fastify, opts) => {
	fastify.decorate('bla', (str:string) =>
	{
		console.log(str);
		return (str);
	})
}
```
The FastifyPluginAsync is the type and is equal to a decorator called bla.
NOTE : since you typed the argument, the decorator will need to return a variable with the same type.

THERES MORE :
You declare the type, but the fastify instance doesn't know that your plugins contents are typed and what type they are.
So you have to specify it.
```ts
declare module 'fastify' {
  interface FastifyInstance {
    bla: (str: string) => string;
  }
}
```
The interface will contains each decorators of your program.
The best use is to create a types.ts where you put all the plugins interfaces.
But you have to set it in your tsconfig.json, otherwise the typescript won't recognize them.
```json
{
  "compilerOptions": {
    "...": "existing options"
  },
  "include": ["src/**/*", "types/**/*"] //the type folder where to put the types
}
```