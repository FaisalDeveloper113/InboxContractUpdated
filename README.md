# InboxContractUpdated
Due to expected dependency conflicts with old installed versions, it would be best to create a brand new project.

In your terminal of choice, run the following:

mkdir inbox-updated
cd inbox-updated
npm init -y
npm install solc@0.8.9 web3 mocha ganache-cli @truffle/hdwallet-provider
Update your test script in the package.json file to be "test": "mocha"

Outline of changes:

Update the pragma version at the top of the contract file to ^0.8.9
Refactor the Inbox constructor to use the new constructor keyword - Source.
Specify the data location of the variables to be memory - Source.
Remove the public keyword from the constructor - Source.
Add an SPDX identifier to the top of the contract (will address compilation warnings) - Source.


Outline of changes:

Add the expected JSON formatted input, specifying the language, sources, and outputSelection - Source.
Update the export to provide the expected JSON formatted output - Source
Note - the output is structured differently so the accessors have changed slightly. If you have a doubt you can add a console.log to view this structure:
console.log(JSON.parse(solc.compile(JSON.stringify(input))).contracts);

Update the import to destructure the abi (formerly the interface) and the evm (bytecode)
const { abi, evm } = require('../compile');

Pass the abi to the contract object
  inbox = await new web3.eth.Contract(abi)

Assign the bytecode to the data property of the deploy method:

    .deploy({
      data: evm.bytecode.object, 
deploy.js

const HDWalletProvider = require('@truffle/hdwallet-provider');
const Web3 = require('web3');
 
const { abi, evm } = require('./compile');
 
provider = new HDWalletProvider(
  'YOUR_MNEMONIC',
  'YOUR_INFURA_URL'
);
 
