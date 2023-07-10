# Syscoin Masternode EVM Registry

Webapp enables Syscoin masternode owners to provably associate an EVM address to their masternode through a Syscoin UTXO blockchain transaction. Built using Next.js framework.

The production version of this app runs at [registry.syscoin.org](https://registry.syscoin.org).

## Why it's useful

A broader horizon for masternode owners!

Registration makes possible various kinds of participation on EVM blockchains on the basis of provable masternode ownership and/or other masternode-related conditions. Technical possibilities include airdrops of EVM tokens to Syscoin masternode owners, etc. Also, it becomes more technically viable for Syscoin's governance participants (normally siloed to Syscoin's native UTXO chain) to participate in other external governance structures. In other words, this registry puts masternodes one step closer to providing on-tap decentralized governance to projects built on Rollux, Ethereum, or other EVMs.

## How it works

This is a passive application. Registering requires direct involvement of a masternode's owner. 

1. You provide your collateral txid, collateral index, and EVM address.
1. The application provides you with a registration RPC command which you execute via `send` in a Syscoin Core console that is connected to your collateral wallet.

This is the best and safest way to provide a registry because it...
1. proves you own the masternode via a signature  
1. gives the safety of a change address which helps keep your collateral address clean
1. avoids any risk of exposing your collateral key as all signing stays within Syscoin Core
1. keeps your collateral intact


## User FAQ

Q. **Will the `send` command spend my masternode collateral?  How is the funding UTXO selected?**  
A. No! Your unspent collateral UTXO is identified and excluded from the selection. The UTXO selected is the oldest one (*other than* your collateral) that happens to have sufficient value to fund the registry transaction. Even so, we recommend that you always validate commands before executing them, including this one!

Q. **How much SYS will it cost to register?**  
A. 0.00001 SYS plus network fee.

Q. **Can I update my registration to a different EVM address?**  
A. This is possible, yes. You simply submit the same registration but with your new EVM address. Although all registrations remain onchain permanently, only the most recent one is considered.

Q. **Does this mean my masternode block rewards will go to the EVM address?**  
A. No. Your rewards will continue to go where they are currently going. Your registration is passive; it does not change how Syscoin Core provides block rewards, nor does it trigger any kind of automated bridge functionality. 

Q. **Can anyone register, even if they don't own a masternode?**  
A. No. This application is specifically intended for masternode owners. It also validates that registrations originate from masternode collateral wallets. If not, the registration attempt is ignored.

Q. **Will I still get a benefit/airdrop/etc if my collateral moves, is sold, or my masternode goes offline before or after I register?**  
A. Ultimately that is decided by the individual project as they make the qualification rules for their particular offering. As a general rule, you will want to make sure to keep your masternode online and its collateral stationary. We tend to assume most projects will disqualify offline or `POSE_BANNED` masternodes.
