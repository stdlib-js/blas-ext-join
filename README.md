<!--

@license Apache-2.0

Copyright (c) 2025 The Stdlib Authors.

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.

-->


<details>
  <summary>
    About stdlib...
  </summary>
  <p>We believe in a future in which the web is a preferred environment for numerical computation. To help realize this future, we've built stdlib. stdlib is a standard library, with an emphasis on numerical and scientific computation, written in JavaScript (and C) for execution in browsers and in Node.js.</p>
  <p>The library is fully decomposable, being architected in such a way that you can swap out and mix and match APIs and functionality to cater to your exact preferences and use cases.</p>
  <p>When you use stdlib, you can be absolutely certain that you are using the most thorough, rigorous, well-written, studied, documented, tested, measured, and high-quality code out there.</p>
  <p>To join us in bringing numerical computing to the web, get started by checking us out on <a href="https://github.com/stdlib-js/stdlib">GitHub</a>, and please consider <a href="https://opencollective.com/stdlib">financially supporting stdlib</a>. We greatly appreciate your continued support!</p>
</details>

# join

[![NPM version][npm-image]][npm-url] [![Build Status][test-image]][test-url] [![Coverage Status][coverage-image]][coverage-url] <!-- [![dependencies][dependencies-image]][dependencies-url] -->

> Return an [ndarray][@stdlib/ndarray/ctor] created by joining elements using a separator along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.



<section class="usage">

## Usage

To use in Observable,

```javascript
join = require( 'https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-join@umd/browser.js' )
```

To vendor stdlib functionality and avoid installing dependency trees for Node.js, you can use the UMD server build:

```javascript
var join = require( 'path/to/vendor/umd/blas-ext-join/index.js' )
```

To include the bundle in a webpage,

```html
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-join@umd/browser.js"></script>
```

If no recognized module system is present, access bundle contents via the global scope:

```html
<script type="text/javascript">
(function () {
    window.join;
})();
</script>
```

#### join( x\[, options] )

Returns an [ndarray][@stdlib/ndarray/ctor] created by joining elements using a separator along one or more [ndarray][@stdlib/ndarray/ctor] dimensions.

```javascript
var array = require( '@stdlib/ndarray-array' );

// Create an input ndarray:
var x = array( [ 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 ] );
// returns <ndarray>

// Perform operation:
var out = join( x );
// returns <ndarray>[ '1,2,3,4,5,6' ]
```

The function has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The function accepts the following options:

-   **sep**: separator. May be either a scalar value or an [ndarray][@stdlib/ndarray/ctor] having a "generic" [data type][@stdlib/ndarray/dtypes]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, an [ndarray][@stdlib/ndarray/ctor] separator value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], an [ndarray][@stdlib/ndarray/ctor] separator value must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor]. Default: `,`.
-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].
-   **keepdims**: boolean indicating whether the reduced dimensions should be included in the returned [ndarray][@stdlib/ndarray/ctor] as singleton dimensions. Default: `false`.

By default, the function joins [ndarray][@stdlib/ndarray/ctor] elements by using `,` as a separator. To perform the operation with a different separator, provide a `sep` option.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ 1.0, 2.0, 3.0, 4.0, 5.0, 6.0 ] );

var out = join( x, {
    'sep': '|'
});
// returns <ndarray>[ '1|2|3|4|5|6' ]
```

By default, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor]. To perform the operation over specific dimensions, provide a `dims` option.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ] );

var out = join( x, {
    'dims': [ 0 ]
});
// returns <ndarray>[ '1,3', '2,4' ]

out = join( x, {
    'dims': [ 1 ]
});
// returns <ndarray>[ '1,2', '3,4' ]

out = join( x, {
    'dims': [ 0, 1 ]
});
// returns <ndarray>[ '1,2,3,4' ]
```

By default, the function excludes reduced dimensions from the output [ndarray][@stdlib/ndarray/ctor]. To include the reduced dimensions as singleton dimensions, set the `keepdims` option to `true`.

```javascript
var array = require( '@stdlib/ndarray-array' );

var x = array( [ [ 1.0, 2.0 ], [ 3.0, 4.0 ] ] );

var opts = {
    'dims': [ 0 ],
    'keepdims': true
};

var out = join( x, opts );
// returns <ndarray>[ [ '1,3', '2,4' ] ]
```

#### join.assign( x, out\[, options] )

Joins elements of an input [ndarray][@stdlib/ndarray/ctor] using a separator along one or more [ndarray][@stdlib/ndarray/ctor] dimensions and assigns results to a provided output [ndarray][@stdlib/ndarray/ctor].

```javascript
var array = require( '@stdlib/ndarray-array' );
var scalar2ndarray = require( '@stdlib/ndarray-from-scalar' );

var x = array( [ 1.0, 2.0, 3.0, 4.0 ] );
var y = scalar2ndarray( '', {
    'dtype': 'generic'
});

var out = join.assign( x, y );
// returns <ndarray>[ '1,2,3,4' ]

var bool = ( out === y );
// returns true
```

The method has the following parameters:

-   **x**: input [ndarray][@stdlib/ndarray/ctor].
-   **out**: output [ndarray][@stdlib/ndarray/ctor].
-   **options**: function options (_optional_).

The method accepts the following options:

-   **sep**: separator. May be either a scalar value or an [ndarray][@stdlib/ndarray/ctor] having a "generic" [data type][@stdlib/ndarray/dtypes]. If provided an [ndarray][@stdlib/ndarray/ctor], the value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the complement of the shape defined by `options.dims`. For example, given the input shape `[2, 3, 4]` and `options.dims=[0]`, an [ndarray][@stdlib/ndarray/ctor] separator value must have a shape which is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with the shape `[3, 4]`. Similarly, when performing the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor], an [ndarray][@stdlib/ndarray/ctor] separator value must be a zero-dimensional [ndarray][@stdlib/ndarray/ctor]. Default: `,`.
-   **dims**: list of dimensions over which to perform operation. If not provided, the function performs the operation over all elements in a provided input [ndarray][@stdlib/ndarray/ctor].

</section>

<!-- /.usage -->

<section class="notes">

## Notes

-   Setting the `keepdims` option to `true` can be useful when wanting to ensure that the output [ndarray][@stdlib/ndarray/ctor] is [broadcast-compatible][@stdlib/ndarray/base/broadcast-shapes] with ndarrays having the same shape as the input [ndarray][@stdlib/ndarray/ctor].

</section>

<!-- /.notes -->

<section class="examples">

## Examples

<!-- eslint no-undef: "error" -->

```html
<!DOCTYPE html>
<html lang="en">
<body>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/random-array-discrete-uniform@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-to-array@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/ndarray-ctor@umd/browser.js"></script>
<script type="text/javascript" src="https://cdn.jsdelivr.net/gh/stdlib-js/blas-ext-join@umd/browser.js"></script>
<script type="text/javascript">
(function () {

// Generate an array of random numbers:
var xbuf = discreteUniform( 10, 0, 20, {
    'dtype': 'float64'
});

// Wrap in an ndarray:
var x = new ndarray( 'float64', xbuf, [ 5, 2 ], [ 2, 1 ], 0, 'row-major' );
console.log( ndarray2array( x ) );

// Perform operation:
var out = join( x, {
    'dims': [ -1 ]
});

// Print the results:
console.log( ndarray2array( out ) );

})();
</script>
</body>
</html>
```

</section>

<!-- /.examples -->

<!-- Section for related `stdlib` packages. Do not manually edit this section, as it is automatically populated. -->

<section class="related">

</section>

<!-- /.related -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->


<section class="main-repo" >

* * *

## Notice

This package is part of [stdlib][stdlib], a standard library for JavaScript and Node.js, with an emphasis on numerical and scientific computing. The library provides a collection of robust, high performance libraries for mathematics, statistics, streams, utilities, and more.

For more information on the project, filing bug reports and feature requests, and guidance on how to develop [stdlib][stdlib], see the main project [repository][stdlib].

#### Community

[![Chat][chat-image]][chat-url]

---

## License

See [LICENSE][stdlib-license].


## Copyright

Copyright &copy; 2016-2026. The Stdlib [Authors][stdlib-authors].

</section>

<!-- /.stdlib -->

<!-- Section for all links. Make sure to keep an empty line after the `section` element and another before the `/section` close. -->

<section class="links">

[npm-image]: http://img.shields.io/npm/v/@stdlib/blas-ext-join.svg
[npm-url]: https://npmjs.org/package/@stdlib/blas-ext-join

[test-image]: https://github.com/stdlib-js/blas-ext-join/actions/workflows/test.yml/badge.svg?branch=v0.1.0
[test-url]: https://github.com/stdlib-js/blas-ext-join/actions/workflows/test.yml?query=branch:v0.1.0

[coverage-image]: https://img.shields.io/codecov/c/github/stdlib-js/blas-ext-join/main.svg
[coverage-url]: https://codecov.io/github/stdlib-js/blas-ext-join?branch=main

<!--

[dependencies-image]: https://img.shields.io/david/stdlib-js/blas-ext-join.svg
[dependencies-url]: https://david-dm.org/stdlib-js/blas-ext-join/main

-->

[chat-image]: https://img.shields.io/badge/zulip-join_chat-brightgreen.svg
[chat-url]: https://stdlib.zulipchat.com

[stdlib]: https://github.com/stdlib-js/stdlib

[stdlib-authors]: https://github.com/stdlib-js/stdlib/graphs/contributors

[umd]: https://github.com/umdjs/umd
[es-module]: https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide/Modules

[deno-url]: https://github.com/stdlib-js/blas-ext-join/tree/deno
[deno-readme]: https://github.com/stdlib-js/blas-ext-join/blob/deno/README.md
[umd-url]: https://github.com/stdlib-js/blas-ext-join/tree/umd
[umd-readme]: https://github.com/stdlib-js/blas-ext-join/blob/umd/README.md
[esm-url]: https://github.com/stdlib-js/blas-ext-join/tree/esm
[esm-readme]: https://github.com/stdlib-js/blas-ext-join/blob/esm/README.md
[branches-url]: https://github.com/stdlib-js/blas-ext-join/blob/main/branches.md

[stdlib-license]: https://raw.githubusercontent.com/stdlib-js/blas-ext-join/main/LICENSE

[@stdlib/ndarray/ctor]: https://github.com/stdlib-js/ndarray-ctor/tree/umd

[@stdlib/ndarray/dtypes]: https://github.com/stdlib-js/ndarray-dtypes/tree/umd

[@stdlib/ndarray/base/broadcast-shapes]: https://github.com/stdlib-js/ndarray-base-broadcast-shapes/tree/umd

</section>

<!-- /.links -->
