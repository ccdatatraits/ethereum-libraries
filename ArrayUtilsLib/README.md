ArrayUtilsLib
=========================

An array utility library [provided by Majoolr](https://github.com/Majoolr "Majoolr's Github") .

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
  - [sumElements(uint256[] storage self) constant returns(uint256 sum)](#sumelementsuint256-storage-self-constant-returnsuint256-sum)
    - [Arguments](#arguments)
    - [Returns](#returns)
  - [getMax(uint256[] storage self) constant returns(uint256 maxValue)](#getmaxuint256-storage-self-constant-returnsuint256-maxvalue)
    - [Arguments](#arguments-1)
    - [Returns](#returns-1)
  - [indexOf(uint256[] storage self, uint256 value, bool isSorted) constant](#indexofuint256-storage-self-uint256-value-bool-issorted-constant)
    - [Arguments](#arguments-2)
    - [Returns](#returns-2)
  - [heapSort(uint256[] storage self)](#heapsortuint256-storage-self)
    - [Arguments](#arguments-3)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Library Address

**ENS**: ArrayUtilsLib.majoolr.eth
**Main Ethereum Network**: 0xf44ab905eba847774848c43735c8ec7d0530956f
**Rinkeby Test Network**: 0xbe3eeaf48f204501db5de4be6181808680b58979
**Ropsten Test Network**: 0x7BCfD8844D248db1ce5C4114b06Bf36762553962

## How to install

### Truffle Installation

**version 3.3.0**

First install truffle via npm using `npm install -g truffle` .

Please [visit Truffle's installation guide](http://truffleframework.com/docs/getting_started/installation "Truffle installation guide") for further information and requirements.

#### Manual install:

This process will allow you to both link your contract to the current on-chain library as well as deploy it in your local environment for development.

1. Place the ArrayUtilsLib.sol file in your truffle `contracts/` directory.
2. Place the ArrayUtilsLib.json file in your truffle `build/contracts/` directory.
3. Amend the deployment .js file in your truffle `migrations/` directory as follows:

```js
var ArrayUtilsLib = artifacts.require("./ArrayUtilsLib.sol");
var OtherLibs = artifacts.require("./OtherLibs.sol");
var YourOtherContract = artifacts.require("./YourOtherContract.sol");
...

module.exports = function(deployer) {
  deployer.deploy(ArrayUtilsLib, {overwrite: false});
  deployer.link(ArrayUtilsLib, YourOtherContract);
  deployer.deploy(YourOtherContract);
};
```

**Note**: The `.link()` function should be called *before* you `.deploy(YourOtherContract)`. Also, be sure to include the `{overwrite: false}` when writing the deployer i.e. `.deploy(ArrayUtilsLib, {overwrite: false})`. This prevents deploying the library onto the main network or Rinkeby test network at your cost and uses the library already on the blockchain. The function should still be called however because it allows you to use it in your development environment. *See below*

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
    "ArrayUtilsLib.sol": {
      "content": "[Contents of ArrayUtilsLib.sol]"
    }
  },
  "settings":
  {
    ...
    "libraries": {
      "YourContract.sol": {
        "ArrayUtilsLib": "0xf44ab905eba847774848c43735c8ec7d0530956f"
      }
    }
  }
}
```
**Note**: The library name should match the name used in your contract.

#### solc without standard JSON input

When creating unlinked binary, the compiler currently leaves special substrings in the compiled bytecode in the form of '__LibraryName______' which leaves a 20 byte space for the library's address. In order to include the deployed library in your bytecode add the following flag to your command:

`--libraries "ArrayUtilsLib:0xf44ab905eba847774848c43735c8ec7d0530956f"`

Additionally, if you have multiple libraries, you can create a file with one library string per line and inlcude this library as follows:

`"ArrayUtilsLib:0xf44ab905eba847774848c43735c8ec7d0530956f"`

then add the following flag to your command:

`--libraries filename`

Finally, if you have an unlinked binary already stored with the '__LibraryName______' placeholder, you can run the compiler with the --link flag and also include the following flag:

`--libraries "ArrayUtilsLib:0xf44ab905eba847774848c43735c8ec7d0530956f"`

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
var lib = fs.readFileSync('./path/to/ArrayUtilsLib.sol','utf8');

var input = {
  "language": "Solidity",
  "sources":
  {
    "ArrayUtilsLib.sol": {
      "content": file
    },
    "ArrayUtilsLib.sol": {
      "content": lib
    }
  },
  "settings":
  {
    ...
    "libraries": {
      "YourContract.sol": {
        "ArrayUtilsLib": "0xf44ab905eba847774848c43735c8ec7d0530956f"
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
 bytecode = solc.linkBytecode(bytecode, { 'ArrayUtilsLib': '0xf44ab905eba847774848c43735c8ec7d0530956f' });
 ```

#### Solc-js documentation

[See the Solc-js documentation for further information](https://github.com/ethereum/solc-js "Solc-js compiler").

## Basic Usage

*Disclaimer: While we make every effort to produce professional grade code we can not guarantee the security and performance of these libraries in your smart contracts. Please use good judgement and security practices while developing, we do not take responsibility for any issues you, your customers, or your applications encounter when using these open source resources.

For a detailed explanation on how libraries are used please read the following from the Solidity documentation:

   * [Libraries](http://solidity.readthedocs.io/en/develop/contracts.html#libraries)
   * [Using For](http://solidity.readthedocs.io/en/develop/contracts.html#using-for)

The ArrayUtilsLib library provides several utility functions for contracts that contain storage arrays. All of the functions only accept a storage array of uint256 types and either returns a uint256 value or, in the case of heapSort, sorts the given array in place which helps to reduce gas costs because of low memory usage. The library uses inline Assembly for most functions which gives a slight improvement in performance and helps us build competency in the lower level language.

When using the `indexOf` function be sure to provide a return tuple and check to ensure the value was found in the array. The function will return 0 as the index if the value was not found. See the usage example below.

### Usage Example

```
pragma solidity ^0.4.11;

import "./ArrayUtilsLib.sol";

contract YourContract {
  using ArrayUtilsLib for uint256[];

  uint256[] array;

  //Then in your function you can call array.function([second argument])
  //Your arguments should be of the same type you bound the library to
  function getSortedIndexOf() returns (bool,uint256){
    bool found;
    uint256 index;
    //The first value in the arguments is the value we're searching for and true
    //indicates the array is sorted
    (found,index) = array.indexOf(7,true);

    //found will now be true if 7 is in the array and index will be the index of 7
  }

  function sortMyStorageArray(){
    array.heapSort();

    //Your array is now sorted
  }
}
```

Binding the library allows you to call the function in the format array.function(otherParameter)

### Usage Note

All of the functions only accept storage arrays containing uint256 types.

## Functions

The following is the list of functions available to use in your smart contract.

   ### sumElements(uint256[] storage self) constant returns(uint256 sum)
   *(ArrayUtilsLib.sol, line 34)*

   Returns the sum of the array elements

   #### Arguments
   self *uint256[] storage variable*

   #### Returns
   sum *uint256*

   ### getMax(uint256[] storage self) constant returns(uint256 maxValue)
   *(ArrayUtilsLib.sol, line 47)*

   Returns the maximum value in the given array.

   #### Arguments
   self *uint256[] storage variable*

   #### Returns
   maxValue *uint256*

   ### indexOf(uint256[] storage self, uint256 value, bool isSorted) constant
       returns(bool found, uint256 index)
   *(ArrayUtilsLib.sol, line 66)*

   Returns true and the index of the given value if found or false and 0 otherwise

   #### Arguments
   self *uint256[] storage variable*
   value *uint256*
   isSorted *bool*

   #### Returns
   found *bool*
   index *uint256*

   ### heapSort(uint256[] storage self)
   *(ArrayUtilsLib.sol, line 118)*

   Sorts the given array.

   #### Arguments
   self *uint256[] storage variable*