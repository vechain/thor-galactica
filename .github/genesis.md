# Genesis Instructions

This document explains how to generate a `genesis.json` file for the blockchain and its ancillary files. It also provides a guide on how to use these files with the `thor` binary.

To generate the genesis files, we use the `generate-genesis.js` script located in the `scripts` folder.

## How to Generate the Files

First, install the project dependencies:

```bash
yarn
```

Next, run the following command to generate all the files:

```bash
node scripts/generate-genesis.js
```

You will be prompted to provide values to be included in the files. These are the default ones:

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

The expected output files are located within the `custom-net` folder (or the directory you specified):

- `authority-keys.json`: Address and private key pair for the authority nodes
- `endorsor-keys.json`: Address and private key pair for the endorsors (same number as authority)
- `executor-keys.json`: Address and private key pair for the executors
- `genesis-keys.json`: Address and private key pair to be included in the genesis block
- `genesis-mnemonic.txt`: Mnemonic to generate the accounts from
- `genesis.json`: Final genesis file relying on the data provided by the above files

## How to Run a Node with the Genesis File

This section provides instructions on how to run a node using the generated file. We assume that the folder name is `custom-net`. Please change it accordingly if you provided a different one.

### Binary
- Clone the [Thor](https://github.com/vechain/thor) repo
- Compile the binaries [as described here](https://github.com/vechain/thor/blob/master/docs/build.md)
- Run for:
    - solo: `./thor/bin/thor solo --genesis custom-net/genesis.json`
    - custom network: `./thor/bin/thor --network custom-net/genesis.json`

### Docker
- Pull the image `docker pull ghcr.io/vechain/thor:release-galactica-latest`
- Run for:
    - solo: 
    ```bash
    docker run -d \
        -v /path/to/custom-net:/custom-net \
        -p 8669:8669 \
        -p 11235:11235 \
        ghcr.io/vechain/thor:release-galactica-latest solo --genesis /custom-net/genesis.json
    ```
    - custom network:
    ```bash
    docker run -d \
        -v /path/to/custom-net:/custom-net \
        -p 8669:8669 \
        -p 11235:11235 \
        ghcr.io/vechain/thor:release-galactica-latest --network /custom-net/genesis.json
    ```

You can also provide a URL with the location of the genesis file, like the one in [this example](https://raw.githubusercontent.com/vechain/thor/master/genesis/example.json).
