<a name="introduction"/></a>

# EigenLayer

EigenLayer is a set of smart contracts deployed on Ethereum that enable restaking of assets to secure new services. This repo contains the EigenLayer core contracts, whose currently-supported assets include beacon chain ETH and several liquid staking tokens (LSTs). Users use these contracts to deposit and withdraw these assets, as well as delegate them to operators providing services to AVSs.

## Getting Started

* [Documentation](#documentation)
* [Building and Running Tests](#building-and-running-tests)
* [Deployments](#deployments)

## Documentation

### Basics

To get a basic understanding of EigenLayer, check out [You Could've Invented EigenLayer](https://www.blog.eigenlayer.xyz/ycie/). Note that some of the document's content describes features that do not exist yet (like the Slasher). To understand more about how restakers and operators interact with EigenLayer, check out these guides:
* [Restaking User Guide](https://docs.eigenlayer.xyz/restaking-guides/restaking-user-guide)
* [Operator Guide](https://docs.eigenlayer.xyz/operator-guides/operator-introduction)

### Deep Dive

The most up-to-date and technical documentation can be found in [/docs](/docs). If you're a shadowy super coder, this is a great place to get an overview of the contracts before diving into the code.

To get an idea of how users interact with these contracts, check out our integration tests: [/src/test/integration](./src/test/integration/).

## Building and Running Tests

This repository uses Foundry. See the [Foundry docs](https://book.getfoundry.sh/) for more info on installation and usage. If you already have foundry, you can build this project and run tests with these commands:

```
foundryup

forge build
forge test
```

### Running Fork Tests

We have a few fork tests against ETH mainnet. Passing these requires the environment variable `RPC_MAINNET` to be set. See `.env.example` for an example. Once you've set up your environment, `forge test` should show these fork tests passing.

Additionally, to run all tests in a forked environment, [install yq](https://mikefarah.gitbook.io/yq/v/v3.x/). Then, set up your environment using this script to read from `config.yml`:

`source source-env.sh [goerli|local]`

Then run the tests:

`forge test --fork-url [RPC_URL]`

### Running Static Analysis

1. Install [solhint](https://github.com/protofire/solhint), then run:

`solhint 'src/contracts/**/*.sol'`

2. Install [slither](https://github.com/crytic/slither), then run:

`slither .`

### Generate Inheritance and Control-Flow Graphs

1. Install [surya](https://github.com/ConsenSys/surya/) and graphviz:

```
npm i -g surya

apt install graphviz
```

2. Then, run:

```
surya inheritance ./src/contracts/**/*.sol | dot -Tpng > InheritanceGraph.png

surya mdreport surya_report.md ./src/contracts/**/*.sol
```

## Deployments

### Current Mainnet Deployment

The current mainnet deployment is our M1 release, and is from a much older version of this repo. You can view the deployed contract addresses in [Current Mainnet Deployment](#current-mainnet-deployment) below, or check out the [`init-mainnet-deployment`](https://github.com/Layr-Labs/eigenlayer-contracts/tree/mainnet-deployment) branch in "Releases".

| Name | Solidity | Proxy | Implementation | Notes |
| -------- | -------- | -------- | -------- | -------- | 
| StrategyManager | [`StrategyManager`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/core/StrategyManager.sol) | [`0x8586...075A`](https://etherscan.io/address/0x858646372CC42E1A627fcE94aa7A7033e7CF075A) | [`0x5d25...42Fb`](https://etherscan.io/address/0x5d25EEf8CfEdaA47d31fE2346726dE1c21e342Fb) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: cbETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x5494...56bc`](https://etherscan.io/address/0x54945180dB7943c0ed0FEE7EdaB2Bd24620256bc) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: stETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x93c4...564D`](https://etherscan.io/address/0x93c4b944D05dfe6df7645A86cd2206016c51564D) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: rETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x1BeE...dCD2`](https://etherscan.io/address/0x1BeE69b7dFFfA4E2d53C2a2Df135C388AD25dCD2) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: ETHx | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x9d7e...011d`](https://etherscan.io/address/0x9d7eD45EE2E8FC5482fa2428f15C971e6369011d) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: ankrETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x1376...58ff`](https://etherscan.io/address/0x13760F50a9d7377e4F20CB8CF9e4c26586c658ff) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: OETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0xa4C6...d059`](https://etherscan.io/address/0xa4C637e0F704745D182e4D38cAb7E7485321d059) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: osETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x57ba...4c02`](https://etherscan.io/address/0x57ba429517c3473B6d34CA9aCd56c0e735b94c02) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: swETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x0Fe4...96d6`](https://etherscan.io/address/0x0Fe4F44beE93503346A3Ac9EE5A26b130a5796d6) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: wBETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x7CA9...2184`](https://etherscan.io/address/0x7CA911E83dabf90C90dD3De5411a10F1A6112184) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: sfrxETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x8CA7...28b6`](https://etherscan.io/address/0x8CA7A5d6f3acd3A7A8bC468a8CD0FB14B6BD28b6) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: lsETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0xAe60...4473`](https://etherscan.io/address/0xAe60d8180437b5C34bB956822ac2710972584473) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: mETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x298a...6dd2`](https://etherscan.io/address/0x298aFB19A105D59E74658C4C334Ff360BadE6dd2) | [`0xdfdA...46d3`](https://etherscan.io/address/0xdfdA04f980bE6A64E3607c95Ca26012Ab9aA46d3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| EigenPodManager | [`EigenPodManager`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/pods/EigenPodManager.sol) | [`0x91E6...A338`](https://etherscan.io/address/0x91E677b07F7AF907ec9a428aafA9fc14a0d3A338) | [`0xEB86...e111`](https://etherscan.io/address/0xEB86a5c40FdE917E6feC440aBbCDc80E3862e111) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| EigenPod (beacon) | [`EigenPod`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/pods/EigenPod.sol) | [`0x5a2a...9073`](https://etherscan.io/address/0x5a2a4F2F3C18f09179B6703e63D9eDD165909073) | [`0x5c86...9dA7`](https://etherscan.io/address/0x5c86e9609fbBc1B754D0FD5a4963Fdf0F5b99dA7) | - Beacon: [OpenZeppelin BeaconProxy@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/beacon/BeaconProxy.sol) <br />- Deployed pods use [UpgradableBeacon@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/beacon/UpgradeableBeacon.sol) |
| DelayedWithdrawalRouter | [`DelayedWithdrawalRouter`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/pods/DelayedWithdrawalRouter.sol) | [`0x7Fe7...23D8`](https://etherscan.io/address/0x7Fe7E9CC0F274d2435AD5d56D5fa73E47F6A23D8) | [`0x44Bc...E2AF`](https://etherscan.io/address/0x44Bcb0E01CD0C5060D4Bb1A07b42580EF983E2AF) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| DelegationManager | [`DelegationManager`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/core/DelegationManager.sol) | [`0x3905...f37A`](https://etherscan.io/address/0x39053D51B77DC0d36036Fc1fCc8Cb819df8Ef37A) | [`0xf97E...75e4`](https://etherscan.io/address/0xf97E97649Da958d290e84E6D571c32F4b7F475e4) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Slasher | [`Slasher`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/core/Slasher.sol) | [`0xD921...c3Cd`](https://etherscan.io/address/0xD92145c07f8Ed1D392c1B88017934E301CC1c3Cd) | [`0xef31...d6d8`](https://etherscan.io/address/0xef31c292801f24f16479DD83197F1E6AeBb8d6d8) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| PauserRegistry | [`PauserRegistry`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/0139d6213927c0a7812578899ddd3dda58051928/src/contracts/permissions/PauserRegistry.sol) | - | [`0x0c43...7060`](https://etherscan.io/address/0x0c431C66F4dE941d089625E5B423D00707977060) | |
| Pauser Multisig | [`GnosisSafe@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/GnosisSafe.sol) | [`0x5050…2390`](https://etherscan.io/address/0x5050389572f2d220ad927CcbeA0D406831012390) | [`0xd9db...9552`](https://etherscan.io/address/0xd9db270c1b5e3bd161e8c8503c55ceabee709552) | Proxy: [`GnosisSafeProxy@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/proxies/GnosisSafeProxy.sol) |
| Community Multisig | [`GnosisSafe@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/GnosisSafe.sol) | [`0xFEA4...c598`](https://etherscan.io/address/0xFEA47018D632A77bA579846c840d5706705Dc598) | [`0xd9db...9552`](https://etherscan.io/address/0xd9db270c1b5e3bd161e8c8503c55ceabee709552) | Proxy: [`GnosisSafeProxy@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/proxies/GnosisSafeProxy.sol) |
| Executor Multisig | [`GnosisSafe@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/GnosisSafe.sol) | [`0x369e...9111`](https://etherscan.io/address/0x369e6F597e22EaB55fFb173C6d9cD234BD699111) | [`0xd9db...9552`](https://etherscan.io/address/0xd9db270c1b5e3bd161e8c8503c55ceabee709552) | Proxy: [`GnosisSafeProxy@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/proxies/GnosisSafeProxy.sol) |
| Operations Multisig | [`GnosisSafe@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/GnosisSafe.sol) | [`0xBE16...3e90`](https://etherscan.io/address/0xBE1685C81aA44FF9FB319dD389addd9374383e90) | [`0xd9db...9552`](https://etherscan.io/address/0xd9db270c1b5e3bd161e8c8503c55ceabee709552) | Proxy: [`GnosisSafeProxy@1.3.0`](https://github.com/safe-global/safe-contracts/blob/v1.3.0/contracts/proxies/GnosisSafeProxy.sol) |
| Timelock | [Compound: `Timelock.sol`](https://github.com/compound-finance/compound-protocol/blob/a3214f67b73310d547e00fc578e8355911c9d376/contracts/Timelock.sol) | - | [`0xA6Db...0EAF`](https://etherscan.io/address/0xA6Db1A8C5a981d1536266D2a393c5F8dDb210EAF) | |
| Proxy Admin | [OpenZeppelin ProxyAdmin@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/ProxyAdmin.sol) | - | [`0x8b95...2444`](https://etherscan.io/address/0x8b9566AdA63B64d1E1dcF1418b43fd1433b72444) | |

### Current Testnet Deployment

The current testnet deployment is from our Goerli v2 release. You can view the deployed contract addresses in [Current Testnet Deployment](#current-testnet-deployment), or check out the [`v0.2.1-goerli-m2`](https://github.com/Layr-Labs/eigenlayer-contracts/tree/v0.2.1-goerli-m2) branch in "Releases".

| Name | Solidity | Proxy | Implementation | Notes |
| -------- | -------- | -------- | -------- | -------- | 
| StrategyManager | [`StrategyManager`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/v0.2.1-goerli-m2/src/contracts/core/StrategyManager.sol) | [`0x779d...E907`](https://goerli.etherscan.io/address/0x779d1b5315df083e3F9E94cB495983500bA8E907) | [`0x506C...40E4`](https://goerli.etherscan.io/address/0x506C21f43e81D9d231d8A13831b42A2a2B5540E4) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: stETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0xB613...14da`](https://goerli.etherscan.io/address/0xb613e78e2068d7489bb66419fb1cfa11275d14da) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: rETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x8799...70b5`](https://goerli.etherscan.io/address/0x879944A8cB437a5f8061361f82A6d4EED59070b5) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: ETHx | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x5d1E...7C14`](https://goerli.etherscan.io/address/0x5d1E9DC056C906CBfe06205a39B0D965A6Df7C14) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: ankrETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x98b4...dB8E`](https://goerli.etherscan.io/address/0x98b47798B68b734af53c930495595729E96cdB8E) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: lsETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0xa9DC...37A9`](https://goerli.etherscan.io/address/0xa9DC3c93ae59B8d26AF17Ae63c96Be78793537A9) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: mETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0x1755...9b14`](https://goerli.etherscan.io/address/0x1755d34476BB4DaEd726ee4a81E8132dF00F9b14) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Strategy: wBETH | [`StrategyBaseTVLLimits`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/strategies/StrategyBaseTVLLimits.sol) | [`0xD89d...E164`](https://goerli.etherscan.io/address/0xD89dc4C40d901D4622C203Fb8808e6e7C7fcE164) | [`0x81E9...8ebA`](https://goerli.etherscan.io/address/0x81E94e16949AC397d508B5C2557a272faD2F8ebA) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| EigenPodManager | [`EigenPodManager`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/v0.2.1-goerli-m2/src/contracts/pods/EigenPodManager.sol) | [`0xa286...df41`](https://goerli.etherscan.io/address/0xa286b84C96aF280a49Fe1F40B9627C2A2827df41) | [`0xDA9B...189f`](https://goerli.etherscan.io/address/0xDA9B60D3dC7adD40C0e35c628561Ff71C13a189f) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| EigenLayerBeaconOracle | [`succinctlabs/EigenLayerBeaconOracle.sol`](https://github.com/succinctlabs/telepathy-contracts/blob/main/external/integrations/eigenlayer/EigenLayerBeaconOracle.sol) | [`0x40B1...9f2c`](https://goerli.etherscan.io/address/0x40B10ddD29a2cfF33DBC420AE5bbDa0649049f2c) | [`0x0a6e...db01`](https://goerli.etherscan.io/address/0x0a6e235c30658dbdb53147fbb199878a4e34db01) | OpenZeppelin UUPS |
| EigenPod (beacon) | [`EigenPod`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/v0.2.1-goerli-m2/src/contracts/pods/EigenPod.sol) | [`0x3093...C9a5`](https://goerli.etherscan.io/address/0x3093F3B560352F896F0e9567019902C9Aff8C9a5) | [`0x16a0...a426`](https://goerli.etherscan.io/address/0x16a0d8aD2A2b12f3f47d0e8F5929F9840e29a426) | - Beacon: [OpenZeppelin BeaconProxy@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/beacon/BeaconProxy.sol) <br />- Deployed pods use [UpgradableBeacon@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/beacon/UpgradeableBeacon.sol) |
| DelayedWithdrawalRouter | [`DelayedWithdrawalRouter`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/v0.2.1-goerli-m2/src/contracts/pods/DelayedWithdrawalRouter.sol) | [`0x8958...388f`](https://goerli.etherscan.io/address/0x89581561f1F98584F88b0d57c2180fb89225388f) | [`0xE576...2878`](https://goerli.etherscan.io/address/0xE576731194EC3d8Ba92E7c2B578ea74238772878) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| DelegationManager | [`DelegationManager`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/v0.2.1-goerli-m2/src/contracts/core/DelegationManager.sol) | [`0x1b7b...b0a8`](https://goerli.etherscan.io/address/0x1b7b8F6b258f95Cf9596EabB9aa18B62940Eb0a8) | [`0x5665...e58C`](https://goerli.etherscan.io/address/0x56652542926444Ebce46Fd97aFd80824ed51e58C) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| AVSDirectory | [`AVSDirectory`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/v0.2.1-goerli-m2/src/contracts/core/AVSDirectory.sol) | [`0x0AC9...f935`](https://goerli.etherscan.io/address/0x0AC9694c271eFbA6059e9783769e515E8731f935) | [`0x871c...8cb3`](https://goerli.etherscan.io/address/0x871cD8f6CFec8b2EB1ac64d58F6D9e1D36a88cb3) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| Slasher | [`Slasher`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/core/Slasher.sol) | [`0xD11d...0C22`](https://goerli.etherscan.io/address/0xD11d60b669Ecf7bE10329726043B3ac07B380C22) | [`0x89C5...D262`](https://goerli.etherscan.io/address/0x89C5e6e98f79be658e830Ec66b61ED3EE910D262) | Proxy: [OpenZeppelin TUP@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/TransparentUpgradeableProxy.sol) |
| PauserRegistry | [`PauserRegistry`](https://github.com/Layr-Labs/eigenlayer-contracts/blob/goerli-m2-deployment/src/contracts/permissions/PauserRegistry.sol) | - | [`0x2588...0010`](https://goerli.etherscan.io/address/0x2588f9299871a519883D92dcd5092B4A0Cf70010) | |
| Timelock | [Compound: `Timelock.sol`](https://github.com/compound-finance/compound-protocol/blob/a3214f67b73310d547e00fc578e8355911c9d376/contracts/Timelock.sol) | - | [`0xa7e7...796e`](https://goerli.etherscan.io/address/0xa7e72a0564ebf25fa082fc27020225edeaf1796e) | |
| Proxy Admin | [OpenZeppelin ProxyAdmin@4.7.1](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/v4.7.1/contracts/proxy/transparent/ProxyAdmin.sol) | - | [`0x28ce...02e2`](https://goerli.etherscan.io/address/0x28ceac2ff82B2E00166e46636e2A4818C29902e2) | |

