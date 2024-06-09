
First we deployed the contract Ballot.sol
https://sepolia.etherscan.io/address/0x9f6a51a83242bb5d6909c2016431fecc776255fa
![image](https://github.com/dutragustavo/Encode-Club-Solidity-Bootcamp-Week2/assets/31355296/a13ed882-636d-403c-87d6-dd6c3bbe1b6b)

CastVote
https://sepolia.etherscan.io/tx/0xa6342467204b8fea1c957a2e779fdb677740f3ef9d560b95ed7a4b4d32228496
![image](https://github.com/dutragustavo/Encode-Club-Solidity-Bootcamp-Week2/assets/31355296/de23dbb4-c486-4c50-b0c5-ca6c8b1bed43)

Worked properly

so now we developed and tested the DelegateVote.ts

```solidity
npx ts-node --files ./scripts/DelegateVote.ts 0x9f6a51A83242bB5D6909C2016431FECc776255Fa 895960eeb2b92269383d152622244f22f291a59d35aeda865798065db490a4aa
```

Failed because we already voted.

`shortMessage: 'Execution reverted with reason: You already voted..',`

So we developed the GiveVoteRights.ts, deployed a new contract 
NewContract > **0xe4a3dd5a5750010ee34064faac7828802b160d5f**

And then we give rigth to vote to a new address 

```solidity
npx ts-node --files ./scripts/GiveVoteRights.ts 0xe4a3dd5a5750010ee34064faac7828802b160d5f 0x41cff881c9c8db0D053A678b0d7aeBDD05754944
```

https://sepolia.etherscan.io/tx/0x7422dd96d84313b323523b4490b65fd01a647f34aaad028146a7e5414d1f8262
![image](https://github.com/dutragustavo/Encode-Club-Solidity-Bootcamp-Week2/assets/31355296/486b4d08-cb05-451e-9a7f-1b3c761b2a37)

Now lets try to delegate the vote back again.

```solidity
npx ts-node --files ./scripts/DelegateVote.ts 0xe4a3dd5a5750010ee34064faac7828802b160d5f 0x3B340ad8Aa7aa2331a8aBB17A2298d8B50EF2b6D
```

`TransactionExecutionError: Execution reverted with reason: Self-delegation is disallowed..`

We are trying to delegate back to the chairperson, but using the chairperson private key, that would be self-delegation so it failed. 
Lets try delegate using another PK
```solidity
npx ts-node --files ./scripts/DelegateVote.ts 0xe4a3dd5a5750010ee34064faac7828802b160d5f 0x3B340ad8Aa7aa2331a8aBB17A2298d8B50EF2b6D
```
https://sepolia.etherscan.io/tx/0x1afd19a97df19b3c9e94a9f6520fb09b132393a52d98d78d84d4150e796c8a44
![image](https://github.com/dutragustavo/Encode-Club-Solidity-Bootcamp-Week2/assets/31355296/52144e7b-3c53-4765-8903-94b116d4688c)

Now we vote, and two votes should be computed
```solidity
npx ts-node --files ./scripts/CastVote.ts 0xe4a3dd5a5750010ee34064faac7828802b160d5f 0
```
https://sepolia.etherscan.io/tx/0xe4208746e3a0e759f30b707286d6215317e9cd9a49fca95605f588036873a30b
![image](https://github.com/dutragustavo/Encode-Club-Solidity-Bootcamp-Week2/assets/31355296/4535831b-275c-4933-8c66-e9477bb69aec)

```
Waiting for confirmations...
Transaction confirmed
Vote count:  2
```

Now let's try get the winner proposal from the contract, it should be the one with index: 0
```solidity
npx ts-node --files ./scripts/getWinnerProposal.ts 0xe4a3dd5a5750010ee34064faac7828802b160d5f
```
``
