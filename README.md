fantasy-auction
===============

Web app that helps conduct a single instance of a fantasy sports auction draft.

There are 3 consumers of the hosted application:

1) Admin - conducts the draft and nominates the current player to draft.  This is typically your commissioner.
2) Managers - the players in the draft.  They will be FB Oauth'd with permissions to participate in bids.
3) General - everyone else with read-only privileges.

### Admin

The admin must be authenticated through some means (basic auth?) and accesses the /admin portion of the site.  There, a list of player names is displayed with the ability to nominate a player.  This player is then pushed on all devices:

1) Admin logs into /admin
2) List of players is displayed
3) Admin picks a player to nominate (client -> server through web sockets)
4) Server pushes the player's details to all clients: player name, current bid, current owner

### Manager

The managers go to the /manager portion of the site.  They have the ability to see the details of the current nominated player and can make bids provided they still have a balance.  This portion of the site is meant to be displayed on a small screen - design will be minimal:

1) Manager logs into /manager
2) Current player, player owner, player price, your bid price, bid button, bump bid button, current balance.
3) Manager bumps the bid until its greater than the current price and hits bid button
4) If transaction goes through, the server deducts from player balance, sets the new price on the player and pushes the new details to clients: player name, current bid, current owner
5) If the transaction falls through, bid fails and the manager is notified

Transactions can fall through for a number of reasons.  Perhaps another manager made the bid first or the bidding manager doesn't have a sufficient balance for the bid.  The bid could also have not been made in the allotted time.

### General

The general audience can view some information about the current auction: The current player details (name, current bid, current owner).  This view is meant to be displayed on a big screen (perhaps via Chromecast).  It is meant to incite players to bid and to glorify the current player on display.


### Future considerations
* Ability to see other manager balances
* Ability to see other manager rosters
* 
