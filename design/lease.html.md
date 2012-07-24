---
layout: design
---
Deal to Lease refactoring
=========================

Currently the Deal class is overloaded with a lot of responsibilites:

* Handling client feedback
* Handling robot feedback
* Handling provider feedback
* Managing a Deal lifecycle

This is unsustainable so we're rebuilding the feedback workflow. This document describes the new design.

### ClientDealFeedback

When a client reports back in the client will fill out a form that will create
an instance of a ClientDealFeedback object in the database. This object has
just the responsibility of storing this feedback.

### ProviderDeal

Based on a ClientDealFeedback the admin may choose to forward it to a provider
for approval. This is done from the admin interface by creating a ProviderDeal
object. The only change made to the ClientDealFeedback is setting the state to
processed.

ProviderDeals are presented to the provider in the provider interface. From
here the provider may choose to confirm or deny the ProviderDeal. If the
provider chooses to confirm the provider is lead to the Lease form where the
provider must enter client, the location, the rent, the move-in date, and the
area.

### Lease

The Lease is a replacement for the current Deal. The important thing about the
Lease is that it is not created until a provider or an admin have confirmed,
that there is an agreement between a tenant and a provider.

### RewardPick

If the client has the option to pick a reward the choice of reward is stored
as a RewardPick object. This object is created alongside the
ClientDealFeedback when the client submits the feedback.

### MatchedOrder

Matched orders are some what equivalent to ClientDealFeedback except that they
are created by the various matcher programs instead of by a client. When a
MatchedOrder object is created the admin has the option to create a new
ProviderDeal based on the MatchedOrder, just like a ClientDealFeedback.