---
content_title: How to build eosio.token
link_text: How to build eosio.token
---

## Preconditions
Ensure an appropriate version of `eosio.cdt` is installed. Installing `eosio.cdt` from binaries is sufficient, follow the [`eosio.cdt` installation instructions steps](https://developers.eos.io/manuals/eosio.cdt/latest/installation) to install it. To verify if you have `eosio.cdt` installed and its version run the following command

```sh
eosio-cpp -v
```

### Build contracts manually

To build the `eosio.token` execute the following commands.

On all platforms except macOS:
```sh
cd you_local_path_to/eosio.token/
rm -fr build
mkdir build
cd build
cmake ..
make -j$( nproc )
cd ..
```

For macOS:
```sh
cd you_local_path_to/eosio.token/
rm -fr build
mkdir build
cd build
cmake ..
make -j$(sysctl -n hw.ncpu)
cd ..
```

#### To build the contract and unit tests
1. Ensure an appropriate version of `eosio` has been built from source and installed. Installing `eosio` from binaries `is not` sufficient. You can find instructions on how to do it in section [Building from Sources](https://developers.eos.io/manuals/eos/latest/install/build-from-source).
2. Run the below command to build all the contracts and the unit tests for these contracts.
```
rm -fr build
mkdir build
cd build
cmake -DBUILD_TESTS=true ..
make
```

### After build:
* If the build was configured to also build unit tests, the unit tests executable is placed in the _build/tests_ folder and is named __unit_test__.
* The contracts (both `.wasm` and `.abi` files) are built into their corresponding _build/contracts/\<contract name\>_ folder.
* Finally, simply use __cleos__ to _set contract_ by pointing to the previously mentioned directory for the specific contract.

# How to deploy the eosio.token

## To deploy eosio.token contract execute the following command:
Let's assume your account name to which you want to deploy the contract is `testertoken`
```
cleos set contract testertoken you_local_path_to/eosio.token/build/contracts/eosio.token/ -p testertoken
```
