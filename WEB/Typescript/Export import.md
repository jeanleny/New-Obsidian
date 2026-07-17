In type script, to export function use the export keyword beside the function to import it in other files :

```ts
export function bla () 
{
	return "the result";
}
```
And call them in your interested file.
```ts
import  {bla} from "../route/linker.js"

const result = bla();

console.log(result);
```
NOTICE : the function imported has the same name.
