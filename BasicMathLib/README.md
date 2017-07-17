BasicMathLib
=========================

A utility library [provided by Majoolr](https://github.com/Majoolr "Majoolr's Github") to protect math operations from overflow and invalid outputs.

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Library Address](#library-address)
- [How to install](#how-to-install)
  - [Truffle Installation](#truffle-installation)
    - [Manual install:](#manual-install)
    - [Testing the library in truffle](#testing-the-library-in-truffle)
    - [EthPM install:](#ethpm-install)
  - [solc Installation](#solc-installation)
    - [With standard JSON input](#with-standard-json-input)
    - [solc without standard JSON input](#solc-without-standard-json-input)
    - [solc documentation](#solc-documentation)
  - [solc-js Installation](#solc-js-installation)
    - [Solc-js Installation via Linking](#solc-js-installation-via-linking)
    - [Solc-js documentation](#solc-js-documentation)
- [Basic Usage](#basic-usage)
  - [Usage Example](#usage-example)
  - [Usage Note](#usage-note)
- [Functions](#functions)
  - [times(numberOne, numberTwo) constant returns (number)](#timesnumberone-numbertwo-constant-returns-number)
    - [Arguments](#arguments)
    - [Returns](#returns)
  - [dividedBy(numberOne, numberTwo) constant returns (number)](#dividedbynumberone-numbertwo-constant-returns-number)
    - [Arguments](#arguments-1)
    - [Returns](#returns-1)
  - [plus(numberOne, numberTwo) constant returns (number)](#plusnumberone-numbertwo-constant-returns-number)
    - [Arguments](#arguments-2)
    - [Returns](#returns-2)
  - [minus(numberOne, numberTwo) constant returns (number)](#minusnumberone-numbertwo-constant-returns-number)
    - [Arguments](#arguments-3)
    - [Returns](#returns-3)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Library Address

**ENS**: BasicMathLib.majoolr.eth   
**Main Ethereum Network**: 0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e   
**Rinkeby Test Network**: 0x11a69bb2979dbd80ec6f142760c1f7abcad5c9b4   
**Ropsten Test Network**: 0x59580eaaa928a54c58c27cd83b9fa6aa3cdfadfa   

## How to install

### Truffle Installation

**version 3.3.0**

First install truffle via npm using `npm install -g truffle` .

Please [visit Truffle's installation guide](http://truffleframework.com/docs/getting_started/installation "Truffle installation guide") for further information and requirements.

#### Manual install:

This process will allow you to both link your contract to the current on-chain library as well as deploy it in your local environment for development.

1. Place the BasicMathLib.sol file in your truffle `contracts/` directory.
2. Place the BasicMathLib.json file in your truffle `build/contracts/` directory.
3. Amend the deployment .js file in your truffle `migrations/` directory as follows:

```js
var BasicMathLib = artifacts.require("./BasicMathLib.sol");
var OtherLibs = artifacts.require("./OtherLibs.sol");
var YourOtherContract = artifacts.require("./YourOtherContract.sol");
...

module.exports = function(deployer) {
  deployer.deploy(BasicMathLib, {overwrite: false});
  deployer.link(BasicMathLib, YourOtherContract);
  deployer.deploy(YourOtherContract);
};
```

**Note**: The `.link()` function should be called *before* you `.deploy(YourOtherContract)`. Also, be sure to include the `{overwrite: false}` when writing the deployer i.e. `.deploy(BasicMathLib, {overwrite: false})`. This prevents deploying the library onto the main network or Rinkeby test network at your cost and uses the library already on the blockchain. The function should still be called however because it allows you to use it in your development environment. *See below*

#### Testing the library in truffle

The following process will allow you to `truffle test` this library in your project.

1. `git clone --recursive` or download the truffle directory.
   Each folder in the truffle directory correlates to the folders in your truffle installation.
2. Place each file in their respective directory in **your** truffle project.
   **Note**: The `2_deploy_test_contracts.js` file should either be renamed to the next highest number among your migrations files i.e. `3_deploy_test_contracts.js` or you can place the code in your existing deployment migration file. *See Quick Install above.*
3. [Start a testrpc node](https://github.com/ethereumjs/testrpc "testrpc's Github")
4. In your terminal go to your truffle project directory and run `truffle migrate`.
5. After migration run `truffle test`.

#### EthPM install:

We were experiencing errors with EthPM deployment and will update this when those are resolved.

### solc Installation

**version 0.4.11**

For direction and instructions on how the Solidity command line compiler works [see the documentation](https://solidity.readthedocs.io/en/develop/using-the-compiler.html#using-the-commandline-compiler "Solc CLI Doc").

#### With standard JSON input

[The Standard JSON Input](https://solidity.readthedocs.io/en/develop/using-the-compiler.html#input-description "Standard JSON Input") provides an easy interface to include libraries. Include the following as part of your JSON input file:

```json
{
  "language": "Solidity",
  "sources":
  {
    "YourContract.sol": {
      ...
      ...
    },
    "BasicMathLib.sol": {
      "content": "[Contents of BasicMathLib.sol]"
    }
  },
  "settings":
  {
    ...
    "libraries": {
      "YourContract.sol": {
        "BasicMathLib": "0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e"
      }
    }
  }
}
```
**Note**: The library name should match the name used in your contract.

#### solc without standard JSON input

When creating unlinked binary, the compiler currently leaves special substrings in the compiled bytecode in the form of '__LibraryName______' which leaves a 20 byte space for the library's address. In order to include the deployed library in your bytecode add the following flag to your command:

`--libraries "BasicMathLib:0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e"`

Additionally, if you have multiple libraries, you can create a file with one library string per line and inlcude this library as follows:

`"BasicMathLib:0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e"`

then add the following flag to your command:

`--libraries filename`

Finally, if you have an unlinked binary already stored with the '__LibraryName______' placeholder, you can run the compiler with the --link flag and also include the following flag:

`--libraries "BasicMathLib:0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e"`

#### solc documentation

[See the solc documentation for further information](https://solidity.readthedocs.io/en/develop/using-the-compiler.html#using-the-commandline-compiler "Solc CLI Doc").

### solc-js Installation

**version 0.4.11**

Solc-js provides javascript bindings for the Solidity compiler and [can be found here](https://github.com/ethereum/solc-js "Solc-js compiler"). Please refer to their documentation for detailed use.

This version of Solc-js also uses the [standard JSON input](#with-standard-json-input) to compile a contract. The entry function is `compileStandardWrapper()` and you can create a standard JSON object explained under the [solc section](#with-standard-json-input) and incorporate it as follows:

```js
var solc = require('solc');
var fs = require('fs');

var file = fs.readFileSync('/path/to/YourContract.sol','utf8');
var lib = fs.readFileSync('./path/to/BasicMathLib.sol','utf8');

var input = {
  "language": "Solidity",
  "sources":
  {
    "YourContract.sol": {
      "content": file
    },
    "BasicMathLib.sol": {
      "content": lib
    }
  },
  "settings":
  {
    ...
    "libraries": {
      "YourContract.sol": {
        "BasicMathLib": "0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e"
      }
    }
    ...
  }
}

var output = JSON.parse(solc.compileStandardWrapper(JSON.stringify(input)));

//Where the output variable is a standard JSON output object.
```

#### Solc-js Installation via Linking

Solc-js also provides a linking method if you have compiled binary code already with the placeholder. To link this library the call would be:

 ```js
 bytecode = solc.linkBytecode(bytecode, { 'BasicMathLib': '0x3e25cde3fb9c93e4c617fe91c8c0d6720c87d61e' });
 ```

#### Solc-js documentation

[See the Solc-js documentation for further information](https://github.com/ethereum/solc-js "Solc-js compiler").

## Basic Usage

*Disclaimer: While we make every effort to produce professional grade code we can not guarantee the security and performance of these libraries in your smart contracts. Please use good judgement and security practices while developing, we do not take responsibility for any issues you, your customers, or your applications encounter when using these open source resources.

For a detailed explanation on how libraries are used please read the following from the Solidity documentation:

   * [Libraries](http://solidity.readthedocs.io/en/develop/contracts.html#libraries)
   * [Using For](http://solidity.readthedocs.io/en/develop/contracts.html#using-for)

The BasicMathLib library does the four basic math functions for unsigned 256-bit integers and protects for overflow, underflow, and from dividing by 0 (yes, we know Solidity throws when dividing by zero but keep reading.) Each function returns two variables, the first being a boolean variable which indicates `true` if there is an error and `false` if there is no error. Error being an under/overflow condition or dividing by 0. The second variable is the result of the operation or 0 if there is an error.

When there is an error condition, BasicMathLib does not `throw`,`invalid`, or `revert`. This is important to understand for your smart contract workflow. The con to this is that **any state changes your contract has made up to this point will need to be handled by you, no state changes will be reverted by the library if there is an error condition.** The pro is this allows the library to log an error event that describes what happened. Pending EIP140, which we are watching, if your smart contract throws, no events will be triggered and there is no way to describe what happened to the user. This library will return (true, 0) if there is an error, triggers an `Err` event with a string logged such as `plus func overflow`, and leaves you the flexibility to handle it how you want.

The results parallel javascript callback functions such that every return will have (err, result). This allows you to handle returns such as:

```
(err, res) = a.times(b);
if(err)
  //handle the error
else
  //there is no error, use res
```

Note: If you choose to throw when there is an error condition, such as `assert(!err)` , the Err event will not trigger and users will only receive the standard Solidity exception. This gives you the benefit of automatically reverting state changes but will not currently provide a reason to your users, leaving them guessing. On the other hand, you can handle the error without throwing such as reverting yourself, etc, and users will receive the error message. This library gives you the flexibility to decide that tradeoff yourself.

In order to use the BasicMathLib library, import it into your contract and then bind it as follows:

### Usage Example

```
pragma solidity ^0.4.11;

import "./BasicMathLib.sol";

contract YourContract {
  using BasicMathLib for uint256;

  //Then in your function you can call [first argument].function([second argument])
  //Your arguments should be of the same type you bound the library to
  function multiplyTwoNumbers(uint256 a, uint256 b) returns (bool,uint256){
    return a.times(b);
  }

  function divideTwoNumbers(uint256 a, uint256 b) returns (string success){
    bool err;
    uint256 res;
    (err, res) = a.dividedBy(b);
    if(!err)
      success = "I divided a number!"
  }
}
```

Binding the library allows you to call the function in the format [firstParameter].function(secondParameter)
### Usage Note

All of the functions only accept uint256 types.

WORD OF CAUTION! If the function overflows or underflows, ie you subtract below
zero, the function will return 0 as the result. If you operate on a variable
but wish to preserve the value, you need to use a temporary variable to hold
that value until checks pass. Consider the following code:

```
pragma solidity ^0.4.11;

import "./BasicMathLib.sol";

contract YourContract {
  using BasicMathLib for uint256;

  uint256 a; //a is a state variable
  ...
  function badSubtract(uint256 b) returns (bool){
    bool err;
    (err, a) = a.minus(b);
    if(err)
      return false;
    //You have changed your state variable to zero
  }

  function goodSubtract(uint256 b) returns (bool){
    bool err;
    uint256 temp;
    (err, temp) = a.minus(b);
    if(err)
      return false;
    //Checks then effects
    a = temp;
  }
  ...
}
```
While it may seem complicated rather than just asserting and throwing an error,
being able to send an error message, when feasible, to your users is much better
than sending them `invalid opcode` and leaving them guessing.

## Functions

The following is the list of functions available to use in your smart contract.

   ### times(numberOne, numberTwo) constant returns (number)
   *(BasicMathLib.sol, line 39)*

   Multiply two numbers. Checks for overflow.

   #### Arguments
   numberOne *uint256*
   numberTwo *uint256*

   #### Returns
   number *uint256*

   ### dividedBy(numberOne, numberTwo) constant returns (number)
   *(BasicMathLib.sol, line 57)*

   Divide two numbers. Checks for 0 divisor.

   #### Arguments
   numberOne *uint256*
   numberTwo *uint256*

   #### Returns
   number *uint256*

   ### plus(numberOne, numberTwo) constant returns (number)
   *(BasicMathLib.sol, line 75)*

   Add two numbers. Checks for overflow.

   #### Arguments
   numberOne *uint256*
   numberTwo *uint256*

   #### Returns
   number *uint256*

   ### minus(numberOne, numberTwo) constant returns (number)
   *(BasicMathLib.sol, line 93)*

   Subtract two numbers. Checks for underflow.

   #### Arguments
   numberOne *uint256*
   numberTwo *uint256*

   #### Returns
   number *uint256*