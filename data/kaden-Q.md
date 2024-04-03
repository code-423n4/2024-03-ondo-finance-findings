## OUSG/rOUSG instant redemptions are blocked when BUIDL is paused

It's possible for the BUIDL contract to be paused and redemptions in ousgInstantManager will revert if BUIDL needs to be redeemed if the BUIDL contract is paused.

## BUIDL centralization risks

The BUIDL contract contains the ability for an admin to burn or transfer arbitrary user balances.

## OUSG price-dependent functions still proceed in rOUSG when the price is considered invalid by ousgInstantManager

In ousgInstantManager.getOUSGPrice, if the retrieved price is not greater than MINIMUM_OUSG_PRICE, we revert because the price is "unexpectedly low". However, in rOUSG.getOUSGPrice, we accept the price as being valid even if it's less than MINIMUM_OUSG_PRICE.