# Parport.JS

Parport.js is a Node.JS addon you can use to **access,
control and communicate with parallel ports**.  
It uses the C++/Java library [Parallel-Port](http://parallel-port.googlecode.com) to
provide a **high-level** and **cross-platform**[<sup>✝</sup>](#compatibility) interface.

    npm install parport

## License

As Parallel-Port is distributed under the GPL, I'm forced to do the
same (which I perfectly agree). So, Parport.JS is distributed under
the [GPLv3](http://www.gnu.org/licenses).

## Usage

```javascript
var par = require('parport');

var port = new par.Port();
port.writeControl(241);
console.log('Data:', port.readData());
console.log('Status:', port.readStatus());
```

You can pass an ID to pick which port to open (useful if you have more than one):

```javascript
var port = new par.Port(1);
port.writeData(110);
```

And remember:

> Exceptions may be thrown  
> if something goes wrong.

Full documentation can be found under `doc/`.  
More examples can be found under `examples/`.

## API

**Read**

```javascript
port.readData(); // Reads 1 byte from the DATA pins.
port.readStatus(); // Reads 1 byte from the STATUS pins.
port.readControl(); // Reads 1 byte from CONTROL pins.
```

**Write**

```javascript
port.writeData( 255 ); // Set the DATA pins to the byte provided.
port.writeControl( 255 ); // Set the CONTROL pins to the byte provided.
port.setDataDirection( 0 ); // Set direction of DATA pins. In: 255, Out: 0
```

## Compatibility

**Important:** these are only the bindings to Node.JS. The common interface
to the platform-dependent functions is in Parallel-Port.

Parallel-Port currently works on the following platforms:

 * **Linux**: through the [parport driver](http://cyberelk.net/tim/parport/parport.html) (usually comes with kernel, see `/dev/parport0`).

 * **Windows**: through the [Inpout32](http://logix4u.net/component/content/article/14-parallel-port/16-inpout32dll-for-windows-982000ntxp) library (free for non-commercial use only).  
   It seems it doesn't work on 64-bit Windows, though.

Platforms with no (but planned) support:

 * **Darwin** (that is, Mac OSX and iOS) not supported.
