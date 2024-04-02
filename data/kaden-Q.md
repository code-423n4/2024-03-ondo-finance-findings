## OUSG/rOUSG instant redemptions are blocked when BUIDL is paused

It's possible for the BUIDL contract to be paused and redemptions in ousgInstantManager will revert if BUIDL needs to be redeemed if the BUIDL contract is paused.

## BUIDL centralization risks

The BUIDL contract contains the ability for an admin to burn or transfer arbitrary user balances.