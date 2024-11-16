# kinoid

<!--
![npms.io](https://img.shields.io/npms-io/maintenance-score/crypto-pwd-generator?style=plastic&logo=npm&label=maintenance)
![npms.io](https://img.shields.io/npms-io/quality-score/crypto-pwd-generator?style=plastic&logo=npm&label=quality)
![npms.io](https://img.shields.io/npms-io/popularity-score/crypto-pwd-generator?style=plastic&logo=npm&label=popularity)

[![NPM Version](https://img.shields.io/npm/v/crypto-pwd-generator?style=plastic&logo=npm&label=version)](https://www.npmjs.com/package/crypto-pwd-generator)
[![NPM Downloads](https://img.shields.io/npm/d18m/crypto-pwd-generator?style=plastic&logo=npm)](https://www.npmjs.com/package/crypto-pwd-generator)
[![NPM License](https://img.shields.io/npm/l/crypto-pwd-generator?style=plastic&logo=GNU)](https://www.gnu.org/licenses/gpl-3.0.html)
[![Crypto](https://img.shields.io/badge/enabled-crypto?style=plastic&logo=alienware&logoColor=white&label=crypto&labelColor=black&color=green)](https://nodejs.org/api/crypto.html)
![Node Current](https://img.shields.io/node/v/crypto-pwd-generator?style=plastic&logo=nodedotjs&logoColor=white&logoSize=auto)
![npm bundle size](https://img.shields.io/bundlephobia/min/crypto-pwd-generator?style=plastic&logo=webpack)
-->

A simple, configurable library for generating rock-solid passwords.

## Overview

**crypto-pwd-generator** allows you to generate password lists or single passwords of any length and
composed of any group of characters. The mechanism is as simple as calling a single function even
without any parameters. It can be used in Node.js CLI applications, WEB applications or VSCode
extensions.

The randomization engine is based on the [Crypto](https://nodejs.org/api/crypto.html) library, which
is
[considered cryptographically secure](https://nodejs.org/api/crypto.html#crypto:~:text=The%20node%3Acrypto%20module%20provides%20cryptographic%20functionality%20that%20includes%20a%20set%20of%20wrappers%20for%20OpenSSL%27s%20hash%2C%20HMAC%2C%20cipher%2C%20decipher%2C%20sign%2C%20and%20verify%20functions.)
and ensures a level of security suitable for industrial or military applications.

Thanks to the use of the `crypto` library and an effective shuffling algorithm, the passwords
produced are aesthetically beautiful and expressive of a high level of entropy.

## Features

The generator, by default, produces a password or a list of 10 passwords, each of them 12 characters
long and containing at least one uppercase character, at least one lowercase character, at least one
number and at least one special character. It is possible to pass to the generator a list of
parameters with which every aspect of the password list structure can be configured.

## Requirements

`Node` version 8 or later.

## Installation

```bash
npm install crypto-pwd-generator
```

## How to use

```javascript
const pwds = require("crypto-pwd-generator");

//////
// Generate a list of passwords with default parameters
const pwdsList = pwds.generate();
pwdsList.forEach((pw) => console.log("default", pw));

// ... or just a single password
const pw = pwds.password();
console.log("one default", pw);

//////
// Generate 20 passwords 32 characters long in the
// format of hexadecimal numbers
const params = {
  quantity: 20,
  pwLength: 32,
  uppercases: "abcdef0123456789",
  lowercases: "abcdef0123456789",
  symbols: "abcdef0123456789",
  digits: "abcdef0123456789",
};

const hexPwList = pwds.generate(params);
hexPwList.forEach((pw) => console.log("hexadecimal", pw));

// one password with the same requirements
const custPw = pwds.password(params);
console.log("one hexadecimal", custPw);

//////
// Generate 10 passwords 8 characters long without
// uppercase characters or symbols; only numbers
// and lowercase characters.
params = {
  pwLength: 8,
  uppercases: "abcdefghijklmnopqrstuvwxyz",
  symbols: "1234567890",
};

const noUpCasePwList = pwds.generate(params);
noUpCasePwList.forEach((pw) => console.log("no uppercases", pw));

// one password with the same requirements
const noUpCasePw = pwds.password(params);
console.log("one no uppercases", noUpCasePw);
```

## Managing settings

The generators can be invoked without any parameters (in this case the default parameters are used)
or with a parameter consisting of an object containing one or more of the following values:

```javascript
const pwds = require("crypto-pwd-generator");

const pwdsList = pwds.generate({
  //////
  // the length of every generated password;
  // type: number; min: 8 chars; max: 128 chars; default: 12 chars;
  pwLength: 12,
  //////
  // the length of the generated list;
  // type: number; min: 1; max: 100; default: 10;
  quantity: 10,
  //////
  // A string containing the uppercase characters used to construct the passwords;
  // type: string; minLength: 4; maxLength: 128; default: 'ABCDEFGHIJKLMNOPQRSTUVWXYZ';
  uppercases: "ABCDEFGHIJKLMNOPQRSTUVWXYZ",
  //////
  // Minimum amount of uppercase characters contained in each password;
  // type: number; min: 1; max: 2; default: 1;
  uppercasesQty: 1,
  //////
  // A string containing the lowercase characters used to construct the passwords;
  // type: string; minLength: 4; maxLength: 128; default: 'abcdefghijklmnopqrstuvwxyz';
  lowercases: "abcdefghijklmnopqrstuvwxyz",
  //////
  // Minimum amount of lowercase characters contained in each password;
  // type: number; min: 1; max: 2; default: 1;
  lowercasesQty: 1,
  //////
  // A string containing the numbers used to construct the passwords;
  // type: string; minLength: 4; maxLength: 128; default: '0123456789';
  digits: "0123456789",
  //////
  // Minimum amount of digits contained in each password;
  // type: number; min: 1; max: 2; default: 1;
  digitsQty: 1,
  //////
  // A string containing the symbols used to construct the passwords;
  // type: string; minLength: 4; maxLength: 128; default: '£$%&+*/-@#';
  symbols: "£$%&+*/-@#",
  //////
  // Minimum amount of special characters contained in each password;
  // type: number; min: 1; max: 2; default: 1;
  symbolsQty: 1,
});
```

<!-- Da qui in poi è sistemato. Rivedere sopra -->

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
