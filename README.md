# @taktikorg/consectetur-quod-dolor <sup>[![Version Badge][npm-version-svg]][package-url]</sup>

[![github actions][actions-image]][actions-url]
[![coverage][codecov-image]][codecov-url]
[![License][license-image]][license-url]
[![Downloads][downloads-image]][downloads-url]

[![npm badge][npm-badge-png]][package-url]

Parse and quote shell commands.

# example

## quote

``` js
var quote = require('@taktikorg/consectetur-quod-dolor/quote');
var s = quote([ 'a', 'b c d', '$f', '"g"' ]);
console.log(s);
```

output

```
a 'b c d' \$f '"g"'
```

## parse

``` js
var parse = require('@taktikorg/consectetur-quod-dolor/parse');
var xs = parse('a "b c" \\$def \'it\\\'s great\'');
console.dir(xs);
```

output

```
[ 'a', 'b c', '\\$def', 'it\'s great' ]
```

## parse with an environment variable

``` js
var parse = require('@taktikorg/consectetur-quod-dolor/parse');
var xs = parse('beep --boop="$PWD"', { PWD: '/home/robot' });
console.dir(xs);
```

output

```
[ 'beep', '--boop=/home/robot' ]
```

## parse with custom escape character

``` js
var parse = require('@taktikorg/consectetur-quod-dolor/parse');
var xs = parse('beep ^--boop="$PWD"', { PWD: '/home/robot' }, { escape: '^' });
console.dir(xs);
```

output

```
[ 'beep --boop=/home/robot' ]
```

## parsing shell operators

``` js
var parse = require('@taktikorg/consectetur-quod-dolor/parse');
var xs = parse('beep || boop > /byte');
console.dir(xs);
```

output:

```
[ 'beep', { op: '||' }, 'boop', { op: '>' }, '/byte' ]
```

## parsing shell comment

``` js
var parse = require('@taktikorg/consectetur-quod-dolor/parse');
var xs = parse('beep > boop # > kaboom');
console.dir(xs);
```

output:

```
[ 'beep', { op: '>' }, 'boop', { comment: '> kaboom' } ]
```

# methods

``` js
var quote = require('@taktikorg/consectetur-quod-dolor/quote');
var parse = require('@taktikorg/consectetur-quod-dolor/parse');
```

## quote(args)

Return a quoted string for the array `args` suitable for using in shell
commands.

## parse(cmd, env={})

Return an array of arguments from the quoted string `cmd`.

Interpolate embedded bash-style `$VARNAME` and `${VARNAME}` variables with
the `env` object which like bash will replace undefined variables with `""`.

`env` is usually an object but it can also be a function to perform lookups.
When `env(key)` returns a string, its result will be output just like `env[key]`
would. When `env(key)` returns an object, it will be inserted into the result
array like the operator objects.

When a bash operator is encountered, the element in the array with be an object
with an `"op"` key set to the operator string. For example:

```
'beep || boop > /byte'
```

parses as:

```
[ 'beep', { op: '||' }, 'boop', { op: '>' }, '/byte' ]
```

# install

With [npm](http://npmjs.org) do:

```
npm install @taktikorg/consectetur-quod-dolor
```

# license

MIT

[package-url]: https://npmjs.org/package/@taktikorg/consectetur-quod-dolor
[npm-version-svg]: https://versionbadg.es/ljharb/@taktikorg/consectetur-quod-dolor.svg
[deps-svg]: https://david-dm.org/ljharb/@taktikorg/consectetur-quod-dolor.svg
[deps-url]: https://david-dm.org/ljharb/@taktikorg/consectetur-quod-dolor
[dev-deps-svg]: https://david-dm.org/ljharb/@taktikorg/consectetur-quod-dolor/dev-status.svg
[dev-deps-url]: https://david-dm.org/ljharb/@taktikorg/consectetur-quod-dolor#info=devDependencies
[npm-badge-png]: https://nodei.co/npm/@taktikorg/consectetur-quod-dolor.png?downloads=true&stars=true
[license-image]: https://img.shields.io/npm/l/@taktikorg/consectetur-quod-dolor.svg
[license-url]: LICENSE
[downloads-image]: https://img.shields.io/npm/dm/@taktikorg/consectetur-quod-dolor.svg
[downloads-url]: https://npm-stat.com/charts.html?package=@taktikorg/consectetur-quod-dolor
[codecov-image]: https://codecov.io/gh/ljharb/@taktikorg/consectetur-quod-dolor/branch/main/graphs/badge.svg
[codecov-url]: https://app.codecov.io/gh/ljharb/@taktikorg/consectetur-quod-dolor/
[actions-image]: https://img.shields.io/endpoint?url=https://github-actions-badge-u3jn4tfpocch.runkit.sh/ljharb/@taktikorg/consectetur-quod-dolor
[actions-url]: https://github.com/taktikorg/consectetur-quod-dolor/actions
