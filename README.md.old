# ethereum-push-notification-system
Protocol for Push notifications for Ethereum (EPNS)

# What are the benefits of having this push notification system on Ethereum?

I see a ton of benefits with the EPNS (Ethereum Push Notification System), both for Ethereum and for third party solidity projects, some of which are:

I am aiming for EPNS to have the ability to differentiate between groups so we can have groups like all ethereum miners, all ethereum active users, custom opt-in groups, etc, etc

## For Ethereum:
- Ethereum can send out notifications to all active addresses in case an important message needs to be delivered or a critical info needs to be broadcasted. For example, when Ethereum 2.0 launches.

- Ethereum can send out notifications to miners whenever a fork takes place.

- Ethereum can send out notifications to exchanges regarding stolen funds so that action against them can be taken (optional protocol method which can be used to block funds if we extend the protocol in that way).

- Since EPNS system will have the feature to send push notifications not only on behalf of Ethereum but also on behalf of third party projects on Ethereum (both of which I will term as apps for information written below). it can also act as a way to monetize the EPNS system when it's used by third party.

- There will be a distinction on what party is sending the message to ensure users are never confused about the authenticity of the message and from which app it has been originated from.

## For Third Party Projects on Ethereum:

- Third Party projects can use EPNS to target either the default groups (Like All Active Users, Miners, etc) or form their own group of addresses (custom opt-in groups) to which they can broadcast their message.

- Example can be when an ICO is conducted or a new cryptocurrency is launched, instead of these projects relying on emails to store and communicate about their updates, they can instead offer EPNS service which is anonymized and doesn't have a central point of failure.

- They can also use it to communicate to users on major events or milestones, if need be.

# Technical Details
The way I see this project is it to have the following major components and phases. Of course, this is just the initial phase so things might require major or minor tweaking moving forward, also some parts might seem crude right now:

The EPNS system works very similar to mobile push notification system. The project owners can communicate with the demography of their users by sending messages out to them.

## EPNS Protocol (Smart Contract):

- I see the EPNS Protocol to be a smart contract as of now, this smart contract will in essence act as a storage for all the messages and other meta, mapping info to be stored which can be retrieved by third party web3 providers to display.

- The Protocol will have the following functions:

	- It allows the apps to send messages to certain groups of their choice, the mapping and tech specs needs to be brainstormed.

	- It allows users (or address owners) to blacklist certain apps if they don't want to receive the messages from them.

	- For the app owners (except for Ethereum), the cost of sending a message should be calculated as gas fees + some fees which goes to Ethereum.

	- It needs to have a function by which the app owners can create or define their own group, this can be a subset of existing group or can be a new group on which the users can give their consent to be included. Kind of like how email addresses are collected for particular projects.

	- This does lead to an issue where in the user might not want to spend gas to give their address to the third party apps, this can be mitigated by cooking logic in the smart contract which requests funds from the third party app itself when they create the group. This can be based on roughly the number of users who they expect to sign up (alternatively, we can have any other criteria that matches the business logic we want to follow). This fund can then be used as meta transaction on behalf of the users who opt in to these groups or want to opt out. Since this is not pure meta transaction in the valid sense, it can be that the user are refunded the gas fees back from the app owner's kitty on their action of subscribe or unsubscribe.

- The EPNS protocol can then be used by the app owners to prepare a message according to the EPNS Message Protocol (outlined below) and then to post it out (or map it out) to the users of a particular group they want to target.

- The EPNS groups are nothing but different demographics, which we will need to brainstorm on as to how to create predefined groups... for example, all ethereum addresses with at least one transaction can be deemed as active but how do we prepare and assign them? Should we create a centralized website to do that job, or a software which a user can download and prepare themself or somewhere in between.

- The EPNS protocol owner would be the official Ethereum address, the messaging when initiated through this adress will ignore the fees portion while the messaging initiated through third party apps will include fees portion.

### Some Pointers:

- The apps (ethereum or third party) will need to register their account in this smart contract, this info can contain a link to their icon, the name of the app among other things... we will however need to vet this information in some way.

- The message needs to be stored and perhaps mapped to all the addresses in the group, this will ensure gas utilization.

- Need to figure out how to map the addresses of the group to the messages in an efficient and optimized way.

## EPNS Message Protocol:

- The EPNS message protocol can store information which is needed to be displayed to the user, such as:

	- The message

	- A Call to Action url

	- Icon can be taken from the app owner meta

	- An ID

	- Other info to be brainstormed on as we further define the feature set

- Any message which needs to be sent should be wrapped in this message protocol structure to ensure standardization

## EPNS API:

- Need to create a Javascript EPNS API to perform functions like registering an app owner, messaging, blacklisting function, how to ensure meta transaction, etc. 

## EPNS Website:

- The purpose of this EPNS website is for the potential app owners to come and register themselves on the smart contract and potentially use the website UI to message their users.

- The website will provide an extremely intuitive UX for app owners to register, create messages and send them (or store them) in the EPNS protocol.

- The website can also serve as a gateway for the users to come and blacklist certain app owners if they don't want to receive the notification from them.

## EPNS Broadcasting:

- This will require third party web3 providers (such as Metamask) to officially tap into our smart contract and read the notifications meant for a wallet address.

- We will also need to roll out a protocol interpretation and documentation guide to tell them how to interpret our protocol and rules which they would need to follow to deliver the message to the user.

- For example, they can maintain the id(or index) of all the messages which the users have read (and dismissed) and can poll the smart contract for messages later than that index and only display those... provided the message app owner is not blacklisted by the user.

## EPNS Protocol Interpretation: 

- This is the set of rules and endpoints which needs to be followed by web3 providers when they incorporate the EPNS system to ensure standardization and unification of user experience.


Also, I do realize some of these pointers will need polishing... I am just conceptualizing all of this and how to make it work well :).

I do see three key pointers which needs more work / brainstorming on:

1. The mapping of address inside each groups - how to do it efficiently.

2. Storing and mapping messages to users of these groups - should a software just sequentially transact on smart contract to write these values or is there a better, more efficient way.

3. The web3 provider framework and how to encourage them to incorporate this once the system is built and is functioning well (or an alternative to it).
