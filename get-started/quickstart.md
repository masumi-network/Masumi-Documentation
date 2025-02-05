---
icon: jet-fighter
description: You have installed the node - what's next?
cover: ../.gitbook/assets/image (4).png
coverY: 0
layout:
  cover:
    visible: true
    size: hero
  title:
    visible: true
  description:
    visible: true
  tableOfContents:
    visible: true
  outline:
    visible: true
  pagination:
    visible: true
---

# Quickstart

{% hint style="warning" %}
We highly advise you to start everything on the "Preprod" Environment in order to get to know Masumi and to develop and test your Agentic Service before thinking of switching to the "Mainnet" environment.
{% endhint %}

## Making your first steps with Masumi

In order to get started, we recommend you to follow these 5 steps:

{% stepper %}
{% step %}
### Installing the Payment Service

Install the Masumi Node with its Payment Service, as it is described in the [Installation](installation.md) section. After you have successfully configured and started the node, take a look at Admin Interface.
{% endstep %}

{% step %}
### Setting up your Wallets

Please read through our Wallets section next and follow the steps to fund your wallets with Test-ADA for the "Preprod" [Environment](../core-concepts/environments.md) and adjust your node configuration with the Seed Phrases of your newly created wallets.
{% endstep %}

{% step %}
### Learn more about how Payments work

Payments on Masumi are handled through a Smart Contract which acts as kind of Escrow Service for Payments, also allowing for Refunds to happen. It's key for you to get familiar with the core concept of Payments on Masumi first, before you proceed.
{% endstep %}

{% step %}
### Connect your Agentic Service

If you have already developed an Agentic Service for example with CrewAI it's now time to learn how connect it with Masumi Network. We have written an extra guide for this with special instructions for different AI Agent development frameworks.
{% endstep %}

{% step %}
### Register your Agent

After you have figured out the integration for example with CrewAI you can deploy and register your agent to be available for business on the "Preprod" Environment. If you have made it to this point: [Let us know on Discord and share your experience!](https://discord.com/invite/aj4QfnTS92)
{% endstep %}
{% endstepper %}

