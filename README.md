Flow.io
==========

Collection of Node.js streams.


## Installation

``` bash
$ npm install flow.io
```

## Usage

To use flow,

``` javascript
var flow = require( 'flow.io' );
```

The flow module is comprised of several smaller modules. If you want to roll your own flow, follow the links and import the individual modules.


## API

The flow module includes the following stream factories...

### Files

#### [flow.read()](https://github.com/flow-io/flow-read)

File readStream factory.

``` javascript
var stream = flow.read()
	.path( 'path/to/file' )
	.stream( clbk );

stream.pipe( process.stdout );
```


#### [flow.write()](https://github.com/flow-io/flow-write)

File writeStream factory.

``` javascript
var stream = flow.write()
	.path( 'path/to/destination' )
	.stream( clbk );

readStream.pipe( stream );
```


### JSON

#### [flow.parse()](https://github.com/flow-io/flow-parse)

Transform stream factory to parse JSON. Wraps JSONStream's [parse](https://github.com/dominictarr/JSONStream) stream.

``` javascript
var rStream = flow.read()
	.path( 'path/to/file.json' )
	.stream();

var pStream = flow.parse().stream();

rStream.pipe( pStream );
```


#### [flow.stringify()](https://github.com/flow-io/flow-stringify)

Transform stream factory to stringify JSON. Wraps JSONStream's [stringify](https://github.com/dominictarr/JSONStream) stream.

``` javascript
var rStream = flow.read()
	.path( 'path/to/file.json' )
	.stream();

var pStream = flow.parse().stream();

var sStream = flow.stringify().stream();

var wStream = flow.write()
	.path( 'path/to/destination.json' )
	.stream();

rStream
	.pipe( pStream )
	.pipe( sStream )
	.pipe( wStream );
```


### Arrays

#### [flow.array()](https://github.com/flow-io/flow-array)

Transform stream factory to convert an array into an element-by-element readable stream. Similar to event-stream [readArray](https://github.com/dominictarr/event-stream#readarray-array), except a transform stream. Useful when using a sink stream which generates an array and where downstream streams in a stream pipeline require individual data elements. 




### Map

#### [flow.map()](https://github.com/flow-io/flow-map)

Transform stream factory to map a data value to another data value via a transformation function. Wraps event-stream's [map](https://github.com/dominictarr/event-stream#map-asyncfunction) stream.


### Reduce

#### [flow.reduce()](https://github.com/flow-io/flow-reduce)

Transform stream factory to perform a data reduction.



### Mathematics

#### [flow.abs()](https://github.com/flow-io/flow-abs)

Transform stream factory to map numeric data stream values to their absolute values.

``` javascript
var readArray = require( 'event-stream' ).readArray;

var readStream = readArray( [ -1, -1, 0, 1, 1 ] );

var stream = flow.abs().stream();

readStream
	.pipe( stream )
	.pipe( /* writable stream */ );
```


#### [flow.pow()](https://github.com/flow-io/flow-pow)

Transform stream factory to exponentiate numeric data stream values according to a specified power.

``` javascript
var readArray = require( 'event-stream' ).readArray;

var readStream = readArray( [ 2, 4, 3, 5, 7 ] );

var stream = flow.pow()
	.exponent( 3 )
	.stream();

readStream
	.pipe( stream )
	.pipe( /* writable stream */ );
```


#### [flow.exp()](https://github.com/flow-io/flow-exp)

Transform stream factory to evaluate an exponential function for each numeric data value.

``` javascript
var readArray = require( 'event-stream' ).readArray;

var readStream = readArray( [ 1.453, 0, 9.504, 102.2, 1 ] );

var stream = flow.exp().stream();

readStream
	.pipe( stream )
	.pipe( /* writable stream */ );
```


### Statistics

#### [flow.count()](https://github.com/flow-io/flow-count)

Reduce stream factory to count the number of streamed data elements and stream the result.


#### [flow.min()](https://github.com/flow-io/flow-min)

Reduce stream factory to find a numeric data stream's minimum value.


#### [flow.mmin()](https://github.com/flow-io/flow-mmin)

Transform stream factory to find sliding-window minimum values (moving min) over a numeric data stream.

``` javascript
var readArray = require( 'event-stream' ).readArray;

var readStream = readArray( [1,0,5,2,3,6,8,1,0] );

var stream = flow.mmin()
	.window( 3 )
	.stream();

readStream
	.pipe( stream )
	.pipe( /* writable stream*/ );
```


#### [flow.max()](https://github.com/flow-io/flow-max)

Reduce stream factory to find a numeric data stream's maximum value.


#### [flow.mmax()](https://github.com/flow-io/flow-mmax)

Transform stream factory to find sliding-window maximum values (moving max) over a numeric data stream.

``` javascript
var readArray = require( 'event-stream' ).readArray;

var readStream = readArray( [1,0,5,2,3,6,8,1,0] );

var stream = flow.mmax()
	.window( 3 )
	.stream();

readStream
	.pipe( stream )
	.pipe( /* writable stream*/ );
```


#### [flow.sum()](https://github.com/flow-io/flow-sum)

Reduce stream factory to calculate a numeric data stream's sum.


#### [flow.msum()](https://github.com/flow-io/flow-msum)

Transform stream factory to compute a sliding-window sum over a numeric data stream.


#### [flow.csum()](https://github.com/flow-io/flow-csum)

Transform stream factory to compute the cumulative sum over a numeric data stream.


#### [flow.median()](https://github.com/flow-io/flow-median)

Reduce stream factory to find a numeric data stream's median value.


#### [flow.quantiles()](https://github.com/flow-io/flow-quantiles)

Reduce stream factory to compute quantiles from a numeric data stream.


#### [flow.iqr()](https://github.com/flow-io/flow-iqr)

Reduce stream factory to compute the inter-quartile range from a numeric data.


#### [flow.histc()](https://github.com/flow-io/flow-histc)

Reduce stream factory to compute a histogram over a numeric data stream.


#### [flow.mean()](https://github.com/flow-io/flow-mean)

Reduce stream factory to calculate a numeric data stream's mean.


#### [flow.mmean()](https://github.com/flow-io/flow-mmean)

Transform stream factory to compute a sliding-window average over a numeric data stream.


#### [flow.variance()](https://github.com/flow-io/flow-variance)

Reduce stream factory to calculate a numeric data stream's variance.


#### [flow.covariance()](https://github.com/flow-io/flow-covariance)

Reduce stream factory to calculate the covariance between data elements in a numeric data stream.


#### [flow.pcc()](https://github.com/flow-io/flow-pcc)

Reduce stream factory to compute the Pearson product-moment correlation coefficient between data elements in a numeric data stream.



### Filters

#### [flow.find()](https://github.com/flow-io/flow-find)

Filter stream factory which finds stream values matching user-defined critiera.


#### [flow.nans()](https://github.com/flow-io/flow-nans)

Filter stream factory which removes any stream values which are not numeric.



---
## Tests

Unit tests use the [Mocha](http://visionmedia.github.io/mocha) test framework with [Chai](http://chaijs.com) assertions.

Assuming you have installed Mocha, execute the following command in the top-level application directory to run the tests:

``` bash
$ mocha
```

All new feature development should have corresponding unit tests to validate correct functionality.


---
## License

[MIT license](http://opensource.org/licenses/MIT). 


---
## Copyright

Copyright &copy; 2014. Athan Reines.
