Binary String
===
[![NPM version][npm-image]][npm-url] [![Build Status][build-image]][build-url] [![Coverage Status][coverage-image]][coverage-url] [![Dependencies][dependencies-image]][dependencies-url]

> Returns a string giving the literal bit representation of a [single-precision floating-point number][ieee754].


## Installation

``` bash
$ npm install math-float32-to-binary-string
```


## Usage

``` javascript
var binaryString = require( 'math-float32-to-binary-string' );
```

#### binaryString( x )

Returns a `string` giving the literal bit representation of a [single-precision floating-point number][ieee754].

``` javascript
var toFloat32 = require( 'float64-to-float32' );

var str = binaryString( toFloat32( 4 ) );
// returns '01000000100000000000000000000000'

str = binaryString( toFloat32( Math.PI ) );
// returns '01000000010010010000111111011011'

str = binaryString( toFloat32( -1e38 ) );
// returns '11111110100101100111011010011001'
```

The `function` handles [subnormals][subnormals].

``` javascript
str = binaryString( toFloat32( -3.14e-39 ) );
// returns '10000000001000100011000100001011'

str = binaryString( toFloat32( 1.4e-45 ) );
// returns '00000000000000000000000000000001'
```

The `function` handles special values.

``` javascript
var pinf = require( 'const-pinf-float32' );
var ninf = require( 'const-ninf-float32' );

str = binaryString( 0 );
// returns '00000000000000000000000000000000'

str = binaryString( -0 );
// returns '10000000000000000000000000000000'

str = binaryString( NaN );
// returns '01111111110000000000000000000000'

str = binaryString( pinf );
// returns '01111111100000000000000000000000'

str = binaryString( ninf );
// returns '11111111100000000000000000000000'
```


## Examples

``` javascript
var round = require( 'math-round' );
var pow = require( 'math-power' );
var float64ToFloat32 = require( 'float64-to-float32' );
var binaryString = require( 'math-float32-to-binary-string' );

var frac;
var sign;
var exp;
var b;
var x;
var i;

// Convert random numbers to literal bit representations...
for ( i = 0; i < 100; i++ ) {
	if ( Math.random() < 0.5 ) {
		sign = -1;
	} else {
		sign = 1;
	}
	frac = Math.random() * 10;
	exp = round( Math.random()*100 );
	if ( Math.random() < 0.5 ) {
		exp = -exp;
	}
	x = sign * frac * pow( 2, exp );
	x = float64ToFloat32( x );
	b = binaryString( x );
	console.log( b );
}
```

To run the example code from the top-level application directory,

``` bash
$ node ./examples/index.js
```


---
## Tests

### Unit

This repository uses [tape][tape] for unit tests. To run the tests, execute the following command in the top-level application directory:

``` bash
$ make test
```

All new feature development should have corresponding unit tests to validate correct functionality.


### Test Coverage

This repository uses [Istanbul][istanbul] as its code coverage tool. To generate a test coverage report, execute the following command in the top-level application directory:

``` bash
$ make test-cov
```

Istanbul creates a `./reports/coverage` directory. To access an HTML version of the report,

``` bash
$ make view-cov
```


### Browser Support

This repository uses [Testling][testling] for browser testing. To run the tests in a (headless) local web browser, execute the following command in the top-level application directory:

``` bash
$ make test-browsers
```

To view the tests in a local web browser,

``` bash
$ make view-browser-tests
```

<!-- [![browser support][browsers-image]][browsers-url] -->


---
## License

[MIT license](http://opensource.org/licenses/MIT).


## Copyright

Copyright &copy; 2016. The [Compute.io][compute-io] Authors.


[npm-image]: http://img.shields.io/npm/v/math-float32-to-binary-string.svg
[npm-url]: https://npmjs.org/package/math-float32-to-binary-string

[build-image]: http://img.shields.io/travis/math-io/float32-to-binary-string/master.svg
[build-url]: https://travis-ci.org/math-io/float32-to-binary-string

[coverage-image]: https://img.shields.io/codecov/c/github/math-io/float32-to-binary-string/master.svg
[coverage-url]: https://codecov.io/github/math-io/float32-to-binary-string?branch=master

[dependencies-image]: http://img.shields.io/david/math-io/float32-to-binary-string.svg
[dependencies-url]: https://david-dm.org/math-io/float32-to-binary-string

[dev-dependencies-image]: http://img.shields.io/david/dev/math-io/float32-to-binary-string.svg
[dev-dependencies-url]: https://david-dm.org/dev/math-io/float32-to-binary-string

[github-issues-image]: http://img.shields.io/github/issues/math-io/float32-to-binary-string.svg
[github-issues-url]: https://github.com/math-io/float32-to-binary-string/issues

[tape]: https://github.com/substack/tape
[istanbul]: https://github.com/gotwarlost/istanbul
[testling]: https://ci.testling.com

[compute-io]: https://github.com/compute-io/
[ieee754]: https://en.wikipedia.org/wiki/IEEE_754-2008
[subnormals]: https://en.wikipedia.org/wiki/Denormal_number
