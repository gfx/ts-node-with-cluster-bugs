As of ts-node v3.0.6, the following command crashes:

```console
$ ts-node --project tsconfig.universal.json cluster.ts
Master 55522 is running
/Users/gfx/repo/ts-node-fork/cluster.ts:1
(function (exports, require, module, __filename, __dirname) { import * as cluster from 'cluster';
                                                              ^^^^^^

SyntaxError: Unexpected token import
    at createScript (vm.js:74:10)
    at Object.runInThisContext (vm.js:116:10)
    at Module._compile (module.js:533:28)
    at Module.m._compile (/opt/brew/lib/node_modules/ts-node/src/index.ts:385:23)
    at Module._extensions..js (module.js:580:10)
    at Object.require.extensions.(anonymous function) [as .ts] (/opt/brew/lib/node_modules/ts-node/src/index.ts:388:12)
    at Module.load (module.js:503:32)
    at tryModuleLoad (module.js:466:12)
    at Function.Module._load (module.js:458:3)
    at Function.Module.runMain (module.js:605:10)
worker 55528 died
/Users/gfx/repo/ts-node-fork/cluster.ts:1
(function (exports, require, module, __filename, __dirname) { import * as cluster from 'cluster';
                                                              ^^^^^^

SyntaxError: Unexpected token import
    at createScript (vm.js:74:10)
    at Object.runInThisContext (vm.js:116:10)
    at Module._compile (module.js:533:28)
    at Module.m._compile (/opt/brew/lib/node_modules/ts-node/src/index.ts:385:23)
    at Module._extensions..js (module.js:580:10)
    at Object.require.extensions.(anonymous function) [as .ts] (/opt/brew/lib/node_modules/ts-node/src/index.ts:388:12)
    at Module.load (module.js:503:32)
    at tryModuleLoad (module.js:466:12)
    at Function.Module._load (module.js:458:3)
    at Function.Module.runMain (module.js:605:10)
worker 55529 died
```

This is because the worker uses the default `tsconfig.json`, not `tsconfig.universal.json` as specified. `tsconfig.json` compiles `import` as is, while `tsconfig.json` compiles `import` to commonjs style `require`.

## env

* ts-node 3.0.6
* tsc 2.3.4
* node 8.1.2
