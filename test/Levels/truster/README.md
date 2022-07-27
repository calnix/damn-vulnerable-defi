# Challenge #3 - Truster

More and more lending pools are offering flash loans. In this case, a new pool has launched that is offering flash loans of DVT tokens for free.

Currently the pool has 1 million DVT tokens in balance. And you have nothing.

But don't worry, you might be able to take them all from the pool. In a single transaction.

[See the contracts](https://github.com/nicolasgarcia214/damn-vulnerable-defi-foundry/tree/master/src/Contracts/truster)
<br/>
[Complete the challenge](https://github.com/nicolasgarcia214/damn-vulnerable-defi-foundry/blob/master/test/Levels/truster/Truster.t.sol)

# Solution

- target.functionCall(data) is your opening
- pass target = address(dvt)
- functionCall is a method in Address.sol
- functionCall returns functionCallWithValue() [line 128 - 139]
- abi.encodeWithSignature("approve(address,uint256)", attacker, TOKENS_IN_POOL);
- cannot do transfer within functionCall as there is FlashLoanHasNotBeenPaidBack() check at the end of flashLoan().
