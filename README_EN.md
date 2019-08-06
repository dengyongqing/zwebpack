# xwebpack
No webpack config.

> This project is just a wrapper on webpack.

[中文文档](README.md)

## Install

```bash
npm i xwebpack --save-dev
```

It can work globally, but not recommend.

## Overview

package.json

```json
{
  "scripts": {
    "build": "xwebpack -e src"
  }
}
```

**No more config, absolutely automatic**

## Cli

This is the output when you command `xwebpack --help`.

```bash
  Usage: xwebpack [options]

  Options:

    -V, --version                    output the version number
    --root [root]                    root context relative to process.cwd()
    --ay, --analyze                  Visualize size of webpack output files with an interactive zoomable treemap.
    --mv, --modifyVars [modifyVars]  Enables run-time modification of Less variables.
    --bp, --babelPolyfill            Use babel-polyfill to polyfill your code.
    --pfx, --prefix [prefix]         Add prefix to output filename. (default: )
    -c, --xConfig [xConfig]          config file of xwebpack
    -e, --entry [entry]              The entry of xwebpack (default: ./src/index.js)
    -p, --path [path]                The output path of xwebpack (default: ./dist)
    -j, --jsx                        Entry extension is .jsx
    -m, --mode [mode]                production or development. (default: production)
    -a, --alias <alias>              Alias for webpack resolve. (A json file | name=path,name=path)
    -s, --splitChunks                https://webpack.js.org/plugins/split-chunks-plugin/
    -w, --watch                      Turn on watch mode.
    -h, --help                       output usage information
```

## Commands

```bash
xwebpack [options]
```

#### -V, --version

Output the xwebpack's version.

#### -c, --config

Use config file.

```javascript
/**
 * use config file.
 * 
 * @mode
 * @entry
 * @output
 * @watch
 * @modifyVars
 * @analyze
 * @jsx
 * @babelPolyfill
 */
module.exports = {
  entry: 'src/index.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'bundle.js'
  },
  jsx: true,
  modifyVars: path.resolve(__dirname, 'theme', 'index.less'),
  alias: {
    'dengyongqing': path.resolve(__dirname, 'alias/dengyongqing.js')
  }
}
```

#### --root

webpack.resolve.modules, root context relative to process.cwd().

```bash
xwebpack --root ..
```

means

```javascript
{
  resolve: {
    modules: [path.resolve(process.cwd(), '..'), 'node_modules']
  }
}
```

#### --ay, --analyze

Visualize size of webpack output files with an interactive zoomable treemap. 
https://github.com/webpack-contrib/webpack-bundle-analyzer

#### --mv, --modifyVars [filePath]

Enables run-time modification of Less variables (Less).
the [filePath] can be a json or less file.

eg.

```bash
xwebpack -e list --mv ./theme/index.less
# or
xwebpack -e list --mv ./theme/theme.json
```

#### --bp, --babelPolyfill

Use babel-polyfill to polyfill your code. It probably be used when you write react app.

#### --pfx, --prefix [value]

Add prefix to output filename. (default: '')

```bash
# prefix: zh-CN

# production mode
[hash:6].zh-CN.min.js

# development mode
zh-CN.min.js
```

#### -e, --entry [filename | directory | mixed]

Specify the entry of xwebpack. (default: 'bundle=./src/index.js')

bundle need a name, so you need format it like this `name=filename`.

* filename

  ```bash
  xwebpack -e home=entry/index.js
  ```
* directory

  You can specify a directory, and xwebpack will find the index automatically.

  eg.
  ```
  my-app
  ├── node_modules
  ├── package.json
  └── entry
      └── index.js
  ```
  ```bash
  xwebpack -e bundle=entry
  ```

  eg.
  ```
  my-app
  ├── README.md
  ├── node_modules
  ├── package.json
  └── applications
      ├── about
      │   └── index.js
      └── home
          └── index.js
  ```
  When the directory like this, you do not need specify the name of bundle, the `about` and `home` will be name.
  ```bash
  xwebpack -e applications
  ```
* Mixed

  ```bash
  xwebpack -e home=src/index.js,applications
  ```

#### -p, --path [value]

`Default: './dist'`

Specify the output directory of xwebpack.

#### -j, --jsx

Specify entry's extension `.jsx`.

#### -m, --mode [mode] (production | development)

`Defalut: production`

* production -- uglify code.
* development -- not uglify code

#### -a, --alias [alias]

Webpack resolve alias, [alias] is a json file like this.

```json
{
  "moment": "client/lib/monent.js"
}
```

```bash
xwebpack -e applications -a alias.json
```

or just use like this:

```bash
xwebpack -e src -a moment=client/moment.js
```

#### -s, --splitChunks

When specify, webpack will split chunks into split files.
https://webpack.js.org/configuration/optimization/#optimization-splitchunks

#### -w, --watch

Open the watch mode.

#### -h, --help

Show usage help.

## LICENSE

[MIT](./LICENSE) © dengyongqing
