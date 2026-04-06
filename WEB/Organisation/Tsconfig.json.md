Same as [[Package.json]] this config file is used for type script purpose.

To use the typescript transpiller install the typescript dependencies

```bash
npm install typescript
```

Then init it with the tsc command

```bash
tsc --init
```

This will generate a tsconfig.json

This config file should be placed at the root of your typescript project aswell so that the files location can be set easier.

Here its a tsconfig.json
```json
{
	"compilerOptions": {
		"target": "ES2020",	//Javascript version
		"module": "NodeNext", //Module manager 
		"moduleResolution": "NodeNext", //How ts finds files with import
		"outDir": "./object", //transpiled scripts location
		"rootDir": "./src", //typescripts files location
		"strict": true, //like wall werror wextra
		"esModuleInterop": true, //compatibility between JS and ecmascript
		"skipLibCheck": true//skip type check
	},
	"include": ["src/**/*"],//which files to compile
  	//"exclude": ["node_modules", "dist"]//which folder to ignore
}
```
