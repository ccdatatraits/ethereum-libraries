Array Utility Libraries
=========================

[![Build Status](https://travis-ci.org/Majoolr/ethereum-libraries.svg?branch=master)](https://travis-ci.org/Majoolr/ethereum-libraries)
[![Join the chat at https://gitter.im/Majoolr/EthereumLibraries](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/Majoolr/EthereumLibraries?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)    

An array utility library [provided by Majoolr](https://github.com/Majoolr "Majoolr's Github") .   

*Note: Each uint array type now has its own library thanks to Joshua Hannan's help. If your storage array contains uint16[] types, for instance, then you would link to the Array16Lib.sol library. This README uses the Array256Lib for all examples.*

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->


- [Library Addresses](#library-addresses)
  - [Array256Lib](#array256lib)
  - [Array128Lib](#array128lib)
  - [Array64Lib](#array64lib)
  - [Array32Lib](#array32lib)
  - [Array16Lib](#array16lib)
  - [Array8Lib](#array8lib)
- [License and Warranty](#license-and-warranty)
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
  - [getMin(uint256[] storage self) constant returns(uint256 minValue)](#getminuint256-storage-self-constant-returnsuint256-minvalue)
    - [Arguments](#arguments-2)
    - [Returns](#returns-2)
  - [indexOf(uint256[] storage self, uint256 value, bool isSorted) constant](#indexofuint256-storage-self-uint256-value-bool-issorted-constant)
    - [Arguments](#arguments-3)
    - [Returns](#returns-3)
  - [heapSort(uint256[] storage self)](#heapsortuint256-storage-self)
    - [Arguments](#arguments-4)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Library Addresses

### Array256Lib   
**ENS**: Array256Lib.majoolr.eth   
**Main Ethereum Network**: 0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247   
**Rinkeby Test Network**: 0xbc3216a0a455a66acdfb5bb3394499ce91f922a0   
**Ropsten Test Network**: 0x7424a30199a76d085277c58e38b5b5375fb9bff8    

### Array128Lib   
**ENS**: Array128Lib.majoolr.eth   
**Main Ethereum Network**: 0xc78c0c443c84518ec6a14e63a994b329ac19024d   
**Rinkeby Test Network**: 0x3992e42d28f407e0447fc072d61a18d985f9d7f6   
**Ropsten Test Network**: 0xcb4092d7c9e942511b9f4ec508ffccc5018775a5    

### Array64Lib   
**ENS**: Array64Lib.majoolr.eth   
**Main Ethereum Network**: 0x5aceb3732891236fa650f6ac0fc54ad6a62721d7   
**Rinkeby Test Network**: 0x76eaa211356fccfb7d4145655871ba7e9ea09d18   
**Ropsten Test Network**: 0x5cc626a7beee0ab35ebdf3a5b03f0b0a996aa981    

### Array32Lib   
**ENS**: Array32Lib.majoolr.eth   
**Main Ethereum Network**: 0xd013b100aa17fbc70be8ced563a49feaacc5fd1d   
**Rinkeby Test Network**: 0x60b46cf2b2f4eab3bc62b2a1bf32f2e0bddd026e   
**Ropsten Test Network**: 0x1252909f34f6d947f065f43c2cdd562c94ce876c    

### Array16Lib   
**ENS**: Array16Lib.majoolr.eth   
**Main Ethereum Network**: 0x2c61c117b2fb8a481a6936ad7015717b6a9c6ba1   
**Rinkeby Test Network**: 0xe883e1ce1ca062d81697a10f9bb1b880c3e5563c   
**Ropsten Test Network**: 0xfb82af7c5c72a412990ed3cff53fa3b3fdc68db5    

### Array8Lib   
**ENS**: Array8Lib.majoolr.eth   
**Main Ethereum Network**: 0xf1da7827c3bb76e9cddfa2d6077695e550f121d7   
**Rinkeby Test Network**: 0xb01497c19cfcae1b30e7dbcd820f9e278eb9a639   
**Ropsten Test Network**: 0xb16d12469c89aaccaea09bc28160ab80674d575a    

## License and Warranty

Be advised that while we strive to provide professional grade, tested code we cannot
guarantee its fitness for your application. This is released under [The MIT License (MIT)](https://github.com/Majoolr/ethereum-libraries/blob/master/LICENSE "MIT License")
and as such we will not be held liable for lost funds, etc. Please use your best
judgment and note the following:   

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED,
INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A
PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT
HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION
OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.

## How to install

### Truffle Installation

**version 3.4.6**

First install truffle via npm using `npm install -g truffle` .

Please [visit Truffle's installation guide](http://truffleframework.com/docs/getting_started/installation "Truffle installation guide") for further information and requirements.

#### Manual install:

This process will allow you to both link your contract to the current on-chain library as well as deploy it in your local environment for development.

1. Place the Array256Lib.sol file in your truffle `contracts/` directory.
2. Place the Array256Lib.json file in your truffle `build/contracts/` directory.
3. Amend the deployment .js file in your truffle `migrations/` directory as follows:

```js
var Array256Lib = artifacts.require("./Array256Lib.sol");
var OtherLibs = artifacts.require("./OtherLibs.sol");
var YourOtherContract = artifacts.require("./YourOtherContract.sol");
...

module.exports = function(deployer) {
  deployer.deploy(Array256Lib, {overwrite: false});
  deployer.link(Array256Lib, YourOtherContract);
  deployer.deploy(YourOtherContract);
};
```

**Note**: The `.link()` function should be called *before* you `.deploy(YourOtherContract)`. Also, be sure to include the `{overwrite: false}` when writing the deployer i.e. `.deploy(Array256Lib, {overwrite: false})`. This prevents deploying the library onto the main network or Rinkeby test network at your cost and uses the library already on the blockchain. The function should still be called however because it allows you to use it in your development environment. *See below*

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

**version 0.4.13**

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
    "Array256Lib.sol": {
      "content": "[Contents of Array256Lib.sol]"
    }
  },
  "settings":
  {
    ...
    "libraries": {
      "YourContract.sol": {
        "Array256Lib": "0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247"
      }
    }
  }
}
```
**Note**: The library name should match the name used in your contract.

#### solc without standard JSON input

When creating unlinked binary, the compiler currently leaves special substrings in the compiled bytecode in the form of '__LibraryName______' which leaves a 20 byte space for the library's address. In order to include the deployed library in your bytecode add the following flag to your command:

`--libraries "Array256Lib:0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247"`

Additionally, if you have multiple libraries, you can create a file with one library string per line and include this library as follows:

`"Array256Lib:0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247"`

then add the following flag to your command:

`--libraries filename`

Finally, if you have an unlinked binary already stored with the '__LibraryName______' placeholder, you can run the compiler with the --link flag and also include the following flag:

`--libraries "Array256Lib:0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247"`

#### solc documentation

[See the solc documentation for further information](https://solidity.readthedocs.io/en/develop/using-the-compiler.html#using-the-commandline-compiler "Solc CLI Doc").

### solc-js Installation

**version 0.4.13**

Solc-js provides javascript bindings for the Solidity compiler and [can be found here](https://github.com/ethereum/solc-js "Solc-js compiler"). Please refer to their documentation for detailed use.

This version of Solc-js also uses the [standard JSON input](#with-standard-json-input) to compile a contract. The entry function is `compileStandardWrapper()` and you can create a standard JSON object explained under the [solc section](#with-standard-json-input) and incorporate it as follows:

```js
var solc = require('solc');
var fs = require('fs');

var file = fs.readFileSync('/path/to/YourContract.sol','utf8');
var lib = fs.readFileSync('./path/to/Array256Lib.sol','utf8');

var input = {
  "language": "Solidity",
  "sources":
  {
    "YourContract.sol": {
      "content": file
    },
    "Array256Lib.sol": {
      "content": lib
    }
  },
  "settings":
  {
    ...
    "libraries": {
      "YourContract.sol": {
        "Array256Lib": "0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247"
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
 bytecode = solc.linkBytecode(bytecode, { 'Array256Lib': '0xcbe717fb2923f4226271cc4c1d5ef2c076fb3247' });
 ```

#### Solc-js documentation

[See the Solc-js documentation for further information](https://github.com/ethereum/solc-js "Solc-js compiler").

## Basic Usage

*Disclaimer: While we make every effort to produce professional grade code we can not guarantee the security and performance of these libraries in your smart contracts. Please use good judgement and security practices while developing, we do not take responsibility for any issues you, your customers, or your applications encounter when using these open source resources.

For a detailed explanation on how libraries are used please read the following from the Solidity documentation:

   * [Libraries](http://solidity.readthedocs.io/en/develop/contracts.html#libraries)
   * [Using For](http://solidity.readthedocs.io/en/develop/contracts.html#using-for)

The Array Utility libraries provide several utility functions for contracts that contain storage arrays. Each library handles the specified uint type and either returns the uint value or, in the case of heapSort, sorts the given array in place which helps to reduce gas costs because of low memory usage.   

When using the `indexOf` function be sure to provide a return tuple and check to ensure the value was found in the array. The function will return 0 as the index if the value was not found. See the usage example below.

### Usage Example

```
pragma solidity ^0.4.13;

import "./Array256Lib.sol";

contract YourContract {
  using Array256Lib for uint256[];

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
   *(Array256Lib.sol, line 34)*

   Returns the sum of the array elements

   #### Arguments
   *uint256[] storage variable* self   

   #### Returns
   *uint256* sum    

   ### getMax(uint256[] storage self) constant returns(uint256 maxValue)
   *(Array256Lib.sol, line 47)*

   Returns the maximum value in the given array.

   #### Arguments
   *uint256[] storage variable* self   

   #### Returns
   *uint256* maxValue   

   ### getMin(uint256[] storage self) constant returns(uint256 minValue)
   *(Array256Lib.sol, line 64)*

   Returns the minimum value in the given array.

   #### Arguments
   *uint256[] storage variable* self   

   #### Returns
   *uint256* minValue    

   ### indexOf(uint256[] storage self, uint256 value, bool isSorted) constant
       returns(bool found, uint256 index)
   *(Array256Lib.sol, line 84)*

   Returns true and the index of the given value if found or false and 0 otherwise

   #### Arguments
   *uint256[] storage variable* self   
   *uint256* value   
   *bool* isSorted    

   #### Returns
   *bool* found    
   *uint256* index    

   ### heapSort(uint256[] storage self)
   *(ArrayUtilsLib.sol, line 144)*

   Sorts the given array.

   #### Arguments
   *uint256[] storage variable* self   
