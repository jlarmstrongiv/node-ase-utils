# Fork
I just needed to merge pull requests from the fragmented libraries.  To install this version, `npm install https://github.com/jlarmstrongiv/node-ase-utils` or `yarn add https://github.com/jlarmstrongiv/node-ase-utils`.

## Merged Pull Requests
- https://github.com/hughsk/adobe-swatch-exchange/pull/6
- https://github.com/DominikGuzei/node-ase-utils/pull/3

## Additional Documentation

### Groups

```json
{
  "version": "1.0",
  "groups": [{
    "name": "Sample Group",
    "colors": [{
      "name": "RGB Red",
      "model": "RGB",
      "color": [1, 0, 0],
      "type": "global"
    }, {
      "name": "RGB Yellow",
      "model": "RGB",
      "color": [1, 1, 0],
      "type": "global"
    }]
  }],
  "colors": []
}
```

### Color Modes
Exporting HSB and WebSafeRGB from Adobe Illustrator both convert to RGB.

Types include `global`, `spot`, and `normal`.  Global allows the color to be synced so that changing the swatch changes all instances.  Spot is also global, but maintains the color models.

Color modes include:
```json
{
  "model": "Gray",
  "color": [
    "0.12345678"
  ]
}

{
  "model": "CMYK",
  "color": [
    "0.12345678",
    "0.12345678",
    "0.12345678",
    "0.12345678"
  ]
}

{
  "model": "RBG",
  "color": [
    "0.12345678",
    "0.12345678",
    "0.12345678"
  ]
}

{
  "model": "LAB",
  "color": [
    "0.12345678",
    "-0.12345678",
    "0.12345678"
  ]
}
```
Note that all colors also have the keys `name` and `type`.

# ase-utils
Encode/decode color palettes in Adobe's `.ase` format.

Liberally taken and modified from https://github.com/hughsk/adobe-swatch-exchange Because Meteor.js does not support loading github forks of npm packages.

## Usage ##
`npm install ase-utils`

### Decoding ASE Files ###
Just read in a `.ase` file and hand it over to the `decode` method:

```javascript
var ase = require('ase-utils');
var fs = require('fs');

var buffer = fs.readFileSync('./test.ase');
var output = require('./test.json');
test.deepEqual(ase.decode(buffer), output);
test.end();
```

`ase.decode` returns a JSON object representing the contents of the `.ase` file, for example:

``` json
{
  "version": "1.0",
  "groups": [],
  "colors": [{
    "name": "RGB Red",
    "model": "RGB",
    "color": [1, 0, 0],
    "type": "global"
  }, {
    "name": "RGB Yellow",
    "model": "RGB",
    "color": [1, 1, 0],
    "type": "global"
  }]
}
```

### Ecoding ASE Files ###

By providing a JSON object (see above) to the `encode` method you get a binary buffer back that represents the .ase format.

```javascript
var ase = require('ase-utils');
var fs = require('fs');

var buffer = fs.readFileSync('./test.ase');
var input = require('./test.json');
test.deepEqual(ase.encode(input), buffer);
test.end();
```

## License ##

MIT. See [LICENSE.md](http://github.com/CodeAdventure/ase-utils/blob/master/LICENSE.md) for details.
