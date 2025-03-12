# Generate genesis file

The purpose of this document is to explain how to generate a genesis.json file for the blockchain and its ancilliary files.

In order to do so, we rely on the script `generate-genesis.js` located in the `scripts` folder.


## How to generate the files

First of all, we install the dependencies of the project:

```bash
yarn
```

After that, we should run the following command that will generate all the files:

```bash
node scripts/generate-genesis.js
```

We will be prompted to provide the values to be included in the files. These are the default ones:

```
✔ Enter the gas limit for the genesis block … 40000000
✔ Enter the extra data for the genesis block … My Custom Genesis Block
✔ Enter the block number for the VIP191 fork … 0
✔ Enter the block number for the ETH_CONST fork … 0
✔ Enter the block number for the BLOCKLIST fork … 0
✔ Enter the block number for the ETH_IST fork … 0
✔ Enter the block number for the VIP214 fork … 0
✔ Enter the block number for the FINALITY fork … 0
✔ Enter the block number for the GALACTICA fork … 0
✔ Enter the amount (Millions) of VET and VTHO to allocate to the genesis accounts … 1000
✔ Enter the number of genesis accounts … 10
✔ Enter the amount of Authority nodes to allocate to the genesis block … 3
✔ Enter the amount (Millions) of VET and VTHO to allocate to each Authority node … 1000
✔ Enter the output directory … ./custom-net
```


The expected output files are (within the `custom-net` folder, following the value provided above):
- `authority-keys.json`: Address and private key pair for the authority nodes
- `endorsor-keys.json`: Address and private key pair for the endorsors (same number as authority)
- `executor-keys.json`: Address and private key pair for the executors
- `genesis-keys.json`: Address and private key pair to be included in the genesis block
- `genesis-mnemonic.txt`: Mnemonic to generate the accounts from
- `genesis.json`: Final genesis file relying on the data provided by the above files

## How to run a node with the genesis file

In this document we will be providing a way to run a node using the generated file. We are assuming that:
1. The folder name is `custom-net`, please change it accordingly if you have provided a different one.
2. You have built the binary [as described here](https://github.com/vechain/thor/blob/master/docs/build.md) under the `thor` submodule.
3. You are running everything from the root of the repository.

The same can be done by providing an URL instead with the location of the genesis file, like the one in [this example](https://raw.githubusercontent.com/vechain/thor/master/genesis/example.json).

### Solo

```bash
./thor/bin/thor --genesis custom-net/genesis.json
```

### Custom network

```bash
./thor/bin/thor --network custom-net/genesis.json
```