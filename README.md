# React + NextJS + Webpacking
Example of computing proofs for the [zkp-merkle-airdrop-contracts](https://github.com/a16z/zkp-merkle-airdrop-contracts) sample repo in the browser. The majority of the work is done by the [zkp-merkle-airdrop-lib](https://github.com/a16z/zkp-merkle-airdrop-lib) which in turn uses the work of the iden3 team's circom libraries. In this repo it's installed as a submodule in `zkp-merkle-airdrop-lib`.

Proof computation takes 20-60s in the browser depending on the machine.

![Fe-ex-picture](FE-EX.png)

## Install 
- `gh repo clone a16z/zkp-merkle-airdrop-fe-ex -- --recurse-submodules`
- Install: `npm i`
- Run local: `npm run dev`

## Notes
This example front-end depends on the following locally served files:
- `mt_8192.txt` – Sample merkle tree from `zkp-merkle-airdrop-contracts/test/temp/mt_8192.txt`
- `circuit_final.zkey` – ZKey used by proof generation
- `circuit.wasm` – Circom wasm used to generate circuit proof by snarkjs

The library includes imports for server-side only libraries. Because this usage is browser based, this repo ignores them during webpacking in `next.config.js`.

# Testing locally
### Setup
- clone the [zkp-merkle-airdrop-contracts](https://github.com/a16z/zkp-merkle-airdrop-contracts) repo: `gh repo clone a16z/zkp-merkle-airdrop-contracts -- --recurse-submodules`
- install: `cd zkp-merkle-airdrop-contracts && npm i && npx hardhat compile` 
- start a local Hardhat node: `npx hardhat node`
- open a new terminal window, navigate back to the `zkp-merkle-airdrop-contracts` directory and deploy: `npx hardhat run --network localhost ./scripts/deploy.ts` 
- note the deploy locations of the ERC20 contract and the PrivateAirdrop contract logged to the console
---
- open a new terminal, clone this repo: `gh repo clone a16z/zkp-merkle-airdrop-fe-ex -- --recurse-submodules`
- install: `cd zkp-merkle-airdrop-fe-ex && npm i`
- launch the front end: `npm run dev`
- navigate to `localhost:3000` a browser 
- point browser wallet at `localhost:8545` (see "Adding Hardhat local..." below)

### UI
- Collect some ETH: Transfer 1 ETH from the default Hardhat signer to the browser's wallet address
- Query Balances: Check the current ERC20 balance for the provided address
- Calculate proof and collect airdrop:
    - Enter a `key` and a `secret` (samples below) and hit "Calculate Proof". This is a 20-60s operation.
    - Once the proof is displayed in the "Proof" section, you can enter a "PrivateAirdrop Contract Address" and hit "Collect Drop". 
    - Querying for the ERC20 balance to confirm receipt.
    - Rinse and repeat.

### Sample keys and secrets 
| key | secret |
| --- | --- |
| 0x0049a9ef3d7fd63b5db0a70c83721ca7e53e092e3edb54de90b07e3e069258fc | 0x003dbe3ecc58da8d8f530d24733846a794fc1047d58ab81fe2dfb240bbc2e994 |
| 0x00818a031d8fae48b4685fad60bfb880451bdb0718181b224e45b27b9cd21dd6 | 0x002966f64f1829eaefa9971f07294364c9ec106b4381ab373356e6ae16897c61 |
| 0x0076f5375cb69a8b00cacb2dfbbf2f9f521ece9bc37676968e403e3aa42d283c | 0x00284cddbdb17bca11bd55822cda81e28d91f8c0fc021fb1d82d32ca93b2488b |
| 0x00372045d58eff4521feba2696634c589c522c26b8252440fdc05588b36b0b9d | 0x00d5940fd9784bbfd8e69760cd8d7f469f685e1acddc1156d8d9910a8a5fd72c |

*[source](https://github.com/a16z/zkp-merkle-airdrop-contracts/blob/master/test/temp/mt_keys_8192.csv)*

### Adding Hardhat local dev chain to Metamask
- Click the "Networks" drop down and then click "Add Network"
- Fill out with the following settings:
![local-metamask-settings](local-metamask-settings.png)

## Disclaimer
_These smart contracts are being provided as is. No guarantee, representation or warranty is being made, express or implied, as to the safety or correctness of the user interface or the smart contracts. They have not been audited and as such there can be no assurance they will work as intended, and users may experience delays, failures, errors, omissions or loss of transmitted information. In addition, any airdrop using these smart contracts should be conducted in accordance with applicable law. Nothing in this repo should be construed as investment advice or legal advice for any particular facts or circumstances and is not meant to replace competent counsel. It is strongly advised for you to contact a reputable attorney in your jurisdiction for any questions or concerns with respect thereto.  a16z is not liable for any use of the foregoing and users should proceed with caution and use at their own risk. See a16z.com/disclosure for more info._
