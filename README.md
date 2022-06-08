# @rexxars/babel-plugin-inline-json-import

A babel plugin that inlines all imports of JSON files straight into your
JavaScript files.

## Example

Given the following JSON file:

```json
{
  "foo": "bar"
}
```

The plugin will transform the following statement:

```js
import json from './path/to/file.json'
```

or

```js
const json = require('./path/to/file.json')
```

to:

```js
const json = {foo: 'bar'}
```

Simple as that! Both `require` and `import` are supported.

Not only that, but it also supports destructuring:

```js
const {foo} = require('./path/to/file.json')
// =>
const foo = 'bar'
```

## Installation

Install the plugin through `npm`, you will also need `babel` installed for
obvious reasons:

```sh
$ npm install --save-dev @rexxars/babel-plugin-inline-json-import
```

Add `@rexxars/babel-plugin-inline-json-import` to the list of plugins. If you are using a `.babelrc` file, the file should have an entry that looks like this:

```json
{
  "plugins": ["@rexxars/inline-json-import"]
}
```

## Usage

This should work straight out of the box. You can configure a `RegExp` pattern you want to match on, should you only wish it to apply to certain JSON files:

```json
{
  "plugins": [
    [
      "@rexxars/inline-json-import",
      {
        "match": "/package.json$",
        "matchFlags": "i"
      }
    ]
  ]
}
```

## Contributing

1. Fork it!
2. Create your feature branch: `git checkout -b my-new-feature`
3. Commit your changes: `git commit -am 'Add some feature'`
4. Push to the branch: `git push origin my-new-feature`
5. Submit a pull request =)

## Fork modifications

This module was originally made by [Bryan Yap](https://github.com/yggie), and has been forked in order to provide the following improvements:

- Inlining of only destructured items where possible
- Rewritten imports now correctly appear _after_ other imports
- Configurable RegExp for specifying which files to inline
- Handles certain "exotic" import styles without crashing
- Handles loading of JSON files from `node_modules`

All modifications were [contributed upstream](https://github.com/yggie/babel-plugin-inline-json-import/pull/17) and is awaiting review at the time of writing.

## License

This project is licensed under the MIT License - see the [LICENSE](/LICENSE)
file for details
