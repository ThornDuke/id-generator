# kinoid

<!--
![npms.io](https://img.shields.io/npms-io/maintenance-score/kinoid?style=plastic&logo=npm&label=maintenance)
![npms.io](https://img.shields.io/npms-io/quality-score/kinoid?style=plastic&logo=npm&label=quality)
![npms.io](https://img.shields.io/npms-io/popularity-score/kinoid?style=plastic&logo=npm&label=popularity)
![Node Current](https://img.shields.io/node/v/kinoid?style=plastic&logo=nodedotjs&logoColor=white&logoSize=auto)
-->

[![NPM Version](https://img.shields.io/npm/v/kinoid?style=plastic&logo=npm&label=version)](https://www.npmjs.com/package/kinoid)
[![NPM Downloads](https://img.shields.io/npm/d18m/kinoid?style=plastic&logo=npm)](https://www.npmjs.com/package/kinoid)
[![NPM License](https://img.shields.io/npm/l/kinoid?style=plastic&logo=MIT)](https://opensource.org/license/mit)
![npm bundle size](https://img.shields.io/bundlephobia/min/kinoid?style=plastic&logo=webpack)

A JavaScript library for generating unique IDs.

## Overview

The **Kinoid** library generates unique IDs as strings made up of numbers and the 26 lowercase
characters of the english alphabet; every string generated by kinoid can be considered as a
[base36 number](https://en.wikipedia.org/wiki/Base36).

The generated IDs are _unique_ because, no matter how many IDs are generated, no ID will ever be the
same as one generated previously, nor as any ID that will be generated subsequently, nor as any ID
generated _simultaneously_ in any other process running on the same machine.

### Features

Each ID is composed of a timestamp (representing milliseconds since the UNIX epoch), a number that
identifies the process in which the program runs, and a final number which can be said a
_serialization value_ or a _singularity factor_ that guarantees the uniqueness of the ID.

IDs are sortable by time, because they are based on the time they were created. Additionally, the
time an ID was created can be calculated from the ID itself thanks to the `decodeId()` utility which
returns an object containing, among other things, the date on which that ID was generated.

### Warning

**IDs are not passwords**. Kinoid ensures that each generated ID is _unique_, but not _necessarily
unpredictable_.

This depends on a limit that affects _all_ libraries: an algorithm that produces unpredictable
strings cannot guarantee their uniqueness and, vice versa, an algorithm that produces unique strings
cannot guarantee their unpredictability.

If you need a library for creating cryptographically secure passwords, consider
[crypto-pwd-generator](https://www.npmjs.com/package/crypto-pwd-generator)

## Installation

```bash
# with npm
npm install kinoid

# with yarn
yarn add kinoid
```

## How to use

### `import`

```javascript
import kinoid from "kinoid";
const { newId, decodeId } = kinoid();

const id = newId();

console.log(id);
// cohb4z87mvoyf1zjy

console.log(`The id '${id}' was generated on ${decodeId(id).date.toDateString()}`);
// The id 'cohb4z87mvoyf1zjy' was generated on Tue Nov 19 2024

console.log(decodeId(id));
// {
//   id: 'cohb4z87mvoyf1zjy',
//   date: 2024-11-19T16:52:19.962Z,
//   singularity: 1144,
//   pid: 5438
// }
```

### `require`

```javascript
const { newId } = require("kinoid")();

const newBook = {
  title: "Love at the time of the inquisition",
  author: "John White",
  publisher: "Hypercubes",
  id: newId(),
};

db.add(newBook);
```

## Contributing

Contributions to this project are welcomed!

Whether you have

- questions, concerns, or suggestions for improving this library
- want to report a bug
- submit a fix
- propose new features

please don't hesitate to reach out to me on GitHub and
[open an issue](https://github.com/ThornDuke/kinoid/issues).

## Disclaimer

Permission is hereby granted, free of charge, to any person obtaining a copy of this software and
associated documentation files (the “Software”), to deal in the Software without restriction,
including without limitation the rights to use, copy, modify, merge, publish, distribute,
sublicense, and/or sell copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial
portions of the Software.

THE SOFTWARE IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT
NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND
NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES
OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
