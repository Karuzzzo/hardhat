[![npm](https://img.shields.io/npm/v/@nomiclabs/hardhat-ethers.svg)](https://www.npmjs.com/package/@nomiclabs/hardhat-ethers)
[![hardhat](https://usehardhat.com/hardhat-plugin-badge.svg?1)](https://usehardhat.com)

# hardhat-ethers

[Hardhat](http://gethardhat.com) plugin for integration with [ethers.js](https://github.com/ethers-io/ethers.js/).

## What

This plugin brings to Hardhat the Ethereum library `ethers.js`, which allows you to interact with the Ethereum blockchain in a simple way.

## Installation

```bash
npm install --save-dev @nomiclabs/hardhat-ethers 'ethers@^5.0.0'
```

And add the following statement to your `hardhat.config.js`:

```js
usePlugin("@nomiclabs/hardhat-ethers");
```

## Tasks

This plugin creates no additional tasks.

## Environment extensions

This plugins adds an `ethers` object to the Hardhat Runtime Environment.

This object has the same API than `ethers.js`, with some extra Hardhat-specific
functionality.

### Provider object

A `provider` field is added to `ethers`, which is an `ethers.providers.Provider`
automatically connected to the selected network.

### Helpers

These helpers are added to the `ethers` object:

```typescript
function getContractFactory(name: string, signer?: ethers.Signer): Promise<ethers.ContractFactory>;


function getContractAt(nameOrAbi: string | any[], address: string, signer?: ethers.Signer): Promise<ethers.Contract>;

function getSigners() => Promise<ethers.Signer[]>;
```

The `Contract`s and `ContractFactory`s returned by these helpers are connected to the first signer returned by `getSigners` be default.

## Usage

There are no additional steps you need to take for this plugin to work.

Install it and access ethers through the Hardhat Runtime Environment anywhere you need it (tasks, scripts, tests, etc). For example, in your `hardhat.config.js`:

```js
usePlugin("@nomiclabs/hardhat-ethers");

// task action function receives the Hardhat Runtime Environment as second argument
task(
  "blockNumber",
  "Prints the current block number",
  async (_, { ethers }) => {
    await ethers.provider.getBlockNumber().then((blockNumber) => {
      console.log("Current block number: " + blockNumber);
    });
  }
);

module.exports = {};
```

And then run `npx hardhat blockNumber` to try it.

Read the documentation on the [Hardhat Runtime Environment](https://usehardhat.com/advanced/hardhat-runtime-environment.html) to learn how to access the HRE in different ways to use ethers.js from anywhere the HRE is accessible.

## TypeScript support

If your project uses TypeScript, you need to create a `hardhat-env.d.ts` file like this:

``` typescript
/// <reference types="@nomiclabs/hardhat-ethers" />
```

If you already have this file, just add that line to it.


Then you have to include that file in the `files` array of your `tsconfig.json`:

```json
{
  ...
  "files": [..., "hardhat-env.d.ts"]
}
```

using the relative path from the `tsconfig.json` to your `hardhat-env.d.ts`.