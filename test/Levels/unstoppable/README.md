# Challenge #1 - Unstoppable

There's a lending pool with a million DVT tokens in balance, offering flash loans for free.

If only there was a way to attack and stop the pool from offering flash loans ...

You start with 100 DVT tokens in balance.

[See the contracts](https://github.com/nicolasgarcia214/damn-vulnerable-defi-foundry/tree/master/src/Contracts/unstoppable)
<br/>
[Complete the challenge](https://github.com/nicolasgarcia214/damn-vulnerable-defi-foundry/blob/master/test/Levels/unstoppable/Unstoppable.t.sol)

# Solution:

OBJ: attack and stop the pool from offering flash loans
In flashloan function, `poolBalance != balanceBefore`

- poolBalance is a storage variable that is updated when tokens are deposited.
- it will not reflect tokens sent directly to the contract via 'transfer' method.
- but balanceBefore is updated from token.balanceOf(address(this))
- by sending tokens directly, we can force poolBalance to be unequal to balanceBefore.
