---
description: >-
  Describes how notifications can be sent out by a dApp, service or a smart
  contract by interacting with our protocol.
---

# Sending Notifications

## High Level Application Flow

{% hint style="info" %}
Sending notification from your service requires **a one time process** of staking fees for creating a channel. Creating channel is extremely simple and can be done via [our dApp](https://app.epns.io) or can be automated on server or smart contract.
{% endhint %}

EPNS uses the following application flow to ensure storage, broadcasting and sending the notifications out from.

![High Level Application Flow](../.gitbook/assets/highlevel.jpg)

{% hint style="info" %}
 Abstracting the data layer on chain \(directly or indirectly\) ensures notifications are platform agnostic. In the future, we might even support other centralized services apart from Mobile, Tablet, Chrome, Firefox, favorite user wallets, etc.
{% endhint %}

