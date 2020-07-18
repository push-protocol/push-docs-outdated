---
description: This page is outdated and in development
---

# Ethereum Push Notification Service

{% hint style="info" %}
This page is outdated and in development
{% endhint %}

## EPNS \(Ethereum Push Notification Service\)

The EPNS protocol is the first of its kind decentralized defi notification protocol which enables users \(wallet addresses\) to receive notifications.

Using the protocol, any dApp, service or smart contract can send notifications to users\(wallet addresses\) in a platform agnostic way \(mobile, tablet, web, fav. wallets, etc\). _**The DeFi aspect of the protocol also ensures that the user receives and earns from those notifications.**_

Slides: [https://docs.google.com/presentation/d/1hweNz4QSDLdCVWKa3T8lw-ZwmhhDuPnhim-bgeUsIks/edit\#slide=id.g85c3ec45e5\_1\_38](https://docs.google.com/presentation/d/1hweNz4QSDLdCVWKa3T8lw-ZwmhhDuPnhim-bgeUsIks/edit#slide=id.g85c3ec45e5_1_38)

Teaser: [https://www.youtube.com/watch?v=kwwnlmUpRsk](https://www.youtube.com/watch?v=kwwnlmUpRsk)

Live Demo: [https://www.youtube.com/watch?v=uI-YhyUyMgw](https://www.youtube.com/watch?v=uI-YhyUyMgw)

## What are the benefits of having EPNS?

Idea behind EPNS is to expand on and integrate existing ways by which a user can be reached out to by different dApp owners, smart contracts, etc. The EPNS service can be used in a variety of ways:

* It can be used to relay important loan liquidation, funds running out, debt positions notifies to a specific user in \#DeFi
* It can be used to inform users of important upcoming events, notifications, etc of specific dApps \(via App Owners\)
* It can be further enhanced to convey push notifications that act as security mechanisms \(for example: a Trusted App Owner group is subscribed by all exchanges, the addresses relayed by this app owner in specific format can automatically blacklist those addresses out\)
* It can potentially be used by Ethereum itself for major announcements like launching of Ethereum 2.0, notifications to miners for any upcoming fork, etc
* It can potentially replace the way new projects gather user's sensitive information. For Example, when an ICO is conducted or a new cryptocurrency is launched, instead of these projects relying on emails to store and communicate about their updates, they can instead offer EPNS service which is anonymized and doesn't have a central point of failure.

## Technical Details

Following definitions are used in the rest of the spec to refer to a particular category or demography of the users of the protocol.

### Definitions

| Term | Description |
| :--- | :--- |
| Contract Owner | The owner of the contract, specifically the address by which the contract is deployed |
| App Owner | The third party projects, dApps or smart contract, specifically the address which forms their identity as well as the custom opt-in group which the subscribed users will recieve message from |
| Users | All the users who don't fall in either of the above category |
| App Owner Group | The group which contains subscribed users of a particular App Owner |
| Subscribed Users | The users who have subscribed to a specific App Owner Group |

For the purpose of explaining above EPNS terms, let's take the example of Youtube and the various associated roles.

| Term | Description |
| :--- | :--- |
| Youtube | Contract Owner |
| Channels | App Owner Groups |
| Channel Owners | App Owners |
| Users | Users |
| Subscribed Users | Users subscribed to a specific App owner group |

### Game Theory

Inorder to ensure the proper participation of all players, following game theory is proposed, features marked with indentation will mostly be excluded from MVP:

* The **contract owner** doesn't have any ability to send message on behalf of **app owners**
* > The **app owners** might spoof other trusted apps and thus will have to be verified or a spam system developed so that users can mark them as spoof or a similar mechanism
* The **app owners** need explicit permission from the **users** before messages can be sent to them
* The **app owners** need to stake some minimum DAI to ensure spam free environment, this is going to be minimal but good enough to ascertain good behavior \(for example: 50 DAI\)
* The **users** need to transact on blockchain to specifically subscribe or unsubscribe to an **app owner group**, this leads to an incentive issue, ie: why would a user spend gas in most cases?
* To counter this, The staked DAI from **app owners** can in turn be used as a incentive for **users** to subscribe to the specific **app owner** group
* This can be done by using service like [**AAVE**](https://app.aave.com/deposit/DAI) to accure interest on the said DAI and distribute it to the subscribed **users** group
* This incentivizes the **users** to spend gas to perform transaction operation of subscribe
* The **app owners** can stake more DAI if they want to, since the **users** are incentivized to subscribe
* > The **app owner** can blacklist a certain **user** from their group if they want to
* The **app owners** can reclaim this DAI back, reclaiming this DAI will also destroy the **app owner group**, a fees of 10 DAI will also be held back for the **contract owner**, the fees is small enough for serious players to not worry about but will act as a further deterrent for bad players

### Features

EPNS should be able to:

* Provide function for dApp or Smart Contract to register itself as **app owner**
* The **app owner** needs to upload their profile in a json format to IPFS, this will contain their name and icon at the beginning, this json file hash is stored on-chain and fetched and shown along with the message they send
* The **users** can subscribe to multiple **app owner group** through their own action
* The **subscribed users** can unsubscribe from an **app owner group** through their own action
* The **app owner** can send messages to their **subscribed users**
* The messages sent from **app owner** can also indicate if they want to use push notification service of [epns.io](https://epns.io).
* A small fee will be charged for using the service for push notification
* To ensure that push notification service usage is done after paying the fee, the message will be emitted with a flag
* The **app owner** can send unencrypted message to their **app owner group** in which case the message will reach every **subscribed users**
* The **app owner** can also send encrypted message to specific **subscribed user** in which case the message will be encrypted with the specific user's public key
* In the encrypted message scenario, the user private key will be used to decrypt the message, this means that the mobile app needs to store the private key of the user wallet which will be done in a safe and secure way. The private key in any case will never leave the user's device
* The web3 provider can also use a similar mechanism to display notifications to the users in the future
* The **app owner** message is to be stored in the JSON file on [ipfs](https://ipfs.io/) and the hash of that will be mapped. this will be interpreted by the server handling push notifications and also by any web3 providers who wants to use the service
* > The JSON file will carry msg type ids which can ensure that the system can be extended beyond the ecosystem, ie: for having a trusted **app owner** with exchanges and **subscribed users** that can monitor and lock down blacklisted wallets automatically in the future.

### Proposed Structure

**Proposed App Owner JSON File Format**

| Name | Type | Description |
| :--- | :--- | :--- |
| name | _string_ | The name of the app to be displayed |
| icon | _base64_ | 128x128 icon to be associated with the app |

**Proposed message JSON File Format**

| Name | Type | Description |
| :--- | :--- | :--- |
| type | _Integer_ | The message type, currently will be 1 indicating normal message |
| payload | _json_ | The Payload of the message |

**Payload Type 1 - Normal Push Notification**

| Name | Type | Description |
| :--- | :--- | :--- |
| title | _String_ | The title of the message |
| message | _String_ | The message |
| cta | _String \(Url\) \(Optional\)_ | The link to perform call to action if any |
| image | _String \(Url\) \(Optional\)_ | To make the notification rich |
| encrypted | _Bool_ | message is encrpted or not |

**Note:** The push notification icon will be taken from the App Owner Json Icon and will be displayed on the right side of the notification area for mobile.

### Tech Spec

EPNS system needs to deal with the following to allow **specific, user permissioned messaging from different custom opt-in groups created by app owners**:

* Creation of App Owners \(dApp Owners, Smart Contracts, etc that want to send message\)
* Storage of Message
* User Subscription to Groups
* Broadcasting of Message

  -- Via EPNS Push Notification Mobile App

  -- Via Web3 Provider

### TBA

