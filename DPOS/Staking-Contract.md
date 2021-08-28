## Contract Address

abeychain staking contract is deployed at address:

```
0x000000000000000000747275657374616b696E67
```

## Contract json ABI

Refer to [Staking ABI](https://github.com/abeychain/go-abey/wiki/Staking-ABI)

## Interact with contract interface

### deposit

One node can participate as a validator to proposal new blocks with `deposit` function. To
create your validator, you need to `deposit` some `abey` coin and register you validator 
public key.  Delegators can bond their coin to the validator account and shares block reward
by their portion. Validator can charge for additional `fee` rate from the delegators reward.

The feeRate calculation:

```
feeRate = fee / 10000
```

After deposit, the node becomes a validator candidate. Only if the deposit balance > 20000(abey),
the validator can be selected as a candidate.

| parameter | type    | comment                                                      |
| --------- | ------- | ------------------------------------------------------------ |
| pubkey    | bytes   | BFT public key of 65 bytes                                   |
| fee       | uint256 | percent of reward charged for delegate, the rate = fee / 10000 |
| value     | wei     | `abey` token to deposit |


### cancel

Validator can cancel a portion of the deposit from staking balance. With the `cancel` transaction executed, the cancelled portion is locked in the contract for about 2 weeks. 
After the period, validator can withdraw the canceled coins.

| parameter | type    | comment                                        |
| :-------- | ------- | ---------------------------------------------- |
| value     | uint256 | unlock a portion of deposit, the unit is `wei` |

### append

Validator can deposit extra `abey` token to the deposit contract by `append` function.

| parameter | type | comment                                         |
| --------- | ---- | ----------------------------------------------- |
| value     | wei  | amout of coin staked by the deposit account |

### withdraw

Validator can withdraw the unlocked token after a locking period of 2 weeks. All the deposit balance can be retrived by `getDeposit` function.

| parameter | type         | comment                                 |
| --------- | ------------ | --------------------------------------- |
| value     | uint256(wei) | amount of value withdrawed to the owner |

### getDeposit

Validator can query deposit balance by `getDeposit` function. there are 3 states for the
deposit: `staked`, `locked`, `unlocked`

* staked: token which validator bond to stake contract and may receive block reward
* locked: token which were canceld but are still locked in the deposit util 2 weeks.
* unlocked: valdator use withdraw token of unlocked state

| parameter | type    | comment                      |
| --------- | ------- | ---------------------------- |
| owner     | address | address of deposit validator |

`getDeposit` function outputs  `uint256` tuple of 3 items:(staked, locked, unlocked)

| parameter | type    | comment                                               |
| --------- | ------- | ----------------------------------------------------- |
| staked    | uint256 | amount which is staked in deposit                     |
| locked    | uint256 | amount which is cancelled but still is in lock period |
| unlocked  | uint256 | amount which validator can withdraw                   |

### delegate

People who do not want to run a validator full node can deposit their token to a certern
validator to gain staking reward.

If the holder's own deposit is less than 20000 abey, delegtor can not receive any reward as the
validator would't be elected as a candidate.

| parameter | type    | comment                                           |
| --------- | ------- | ------------------------------------------------- |
| holder    | address | address of a particular validator account                         |
| value     | wei     | amout of coin deposit to the delegator account |


### undelegate

Delegator can cancel a portion of the deposit from a certern validator holder.
With the `undelegate` transaction, the cancelled portion is locked in the contract for
about 2 weeks. After the period, delegator can withdraw the canceled token.

| parameter | type    | comment                            |
| --------- | ------- | ---------------------------------- |
| holder    | address | address of the delegator           |
| value     | uint256 | unlock a portion of delegated coin |

### withdrawDelegate

Delegator can withdraw the unlocked token from a validtor. All the delegation balance can be retrived by `getDelegate` function.

| parameter | type    | comment                                |
| --------- | ------- | -------------------------------------- |
| holder    | address | address of the delegator               |
| value     | uint256 | amount of coin withdrawed to the owner |

### getDelegate

`getDelegate` return the balance state of a delegator. The state of token balance is similar to `getDeposit`

| parameter | type    | comment                             |
| --------- | ------- | ----------------------------------- |
| owner     | address | owner address of the delegated coin |
| holder    | address | address of the delegator            |

`getDelegate` function outputs  `uint256` tuple of 3 items: (staked, locked, unlocked)

| parameter | type    | comment                                               |
| --------- | ------- | ----------------------------------------------------- |
| staked    | uint256 | amount which is staked in deposit                     |
| locked    | uint256 | amount which is cancelled but still is in lock period |
| unlocked  | uint256 | amount which coin owner can withdraw                  |
