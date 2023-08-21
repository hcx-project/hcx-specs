---
description: Guidelines on strategy for operating charges by the operators
---

# Guidelines for Operating charges

### Operating charges/Pricing

Like with any infrastructural offering, offerings of the operating entity (based on the ecosystem needs with the infrastructure) will evolve over time. Therefore the model pricing strategy needs to be flexible to provide for evolution of needs as the ecosystem evolves. E.g. in the beginning the objective may be higher integration and adoption rates, as time progresses need may be to provide new value added use cases/service, and it may further evolve to provide tighter (real time/near real time) SLAs.

Operators may charge fees from participants in any of the methods commonly used by exchanges, depositories (for example, stock exchanges, commodity exchanges,stock depositories etc.). The methods could be the following or a combination thereof :

1. Listing and subscription
2. Fixed fee per claim or subscription slabs based on number of claims
3. Transaction/Claim specific fee based on special needs of a claim, say additional quantum of data exchanged, or number of times data is exchanged to settle a claim

The pricing and choice of pricing models can be modified by the operator from time to time, reacting to competitive pressures and also to enhance the value delivered to its participants (customers)

It may help to unbundle different aspects of the pricing strategy to allow needed flexibility in the strategy. The following categorisation of offerings gives a costing basis as also a justification basis for the adopted pricing. However, it is recommended that the pricing models be kept very simple and focused on just a few key, well understood drivers -

**What (offerings) may be charged**

1. Registry maintenance and access, e.g.
   1. Subscription to change notifications
2. Facilitating the claim submission process&#x20;
   1. Basic process - Simple cycle
   2. Advance process facilitation, e.g.
      1. Enabling forward/redirects for multi party processing facilitation
      2. Auto status check and reporting to providers/ISNPs
      3. In process communication for preauth/claims cycle etc.
3. Facilitating compliance reporting of the claims data, e.g.&#x20;
   1. Operating entity may run and maintain schedules against which it can search the data from the payors and forward to IIB, thereby easing the process for the payor)
4. Open data streams on the agreed data (data in protocol/domain headers)
5. Other innovating offerings&#x20;

**Who may get charged for each of these offerings**

Here is the [list of key roles](https://docs.swasth.app/v1.1-draft/hcx-domain-specifications/healthcare-operations-policies/access-control-roles) envisioned in the current version of the HCXS specifications. While the list includes many roles, they can be high level categorized in following personas:

1. Claim Sender - providers
2. Claim Receiver - payors/sponsors
3. Processing helpers - TPAs, TSPs, ISNPs, other HCX instance
4. Observers - regulators, Sponsors, ISNPs, researchers

In the current scenario, claim processing expenses are mostly borne by the payors, however, based on the nature of key offerings on HCX there may be a potential to levy charges to other persona/roles also.

**What could be the Basis and Quantum of charges**

One way to think about it could be that actual pricing of an offering from an operator would be a function of many operational choices and best derived by the operator. There can be many models that may emerge - flat claim fee, flat transaction fee, or flat monthly fee, or mixed slabs etc. However the key aspect here would be that the pricing plan strategy is formulated using a robust governance process and transparently published in the public domain.

RBI has also prescribed a guideline for a similar construct (Account Aggregator) in the financial domain ([Section 13, Account Aggregator master directive](https://rbi.org.in/Scripts/BS\_ViewMasDirections.aspx?id=10598)).

It is generally felt that a transaction/claim value based pricing may not be justifiable for an infrastructure business in a high volume, evolved market.

An infrastructure service may choose to estimate infrastructure costs and per transaction costs and translate that into a pricing model. Translating per transaction costing into a pricing model could include one or more of the following:

1. Listing and storage pricing per day/month/year - by estimating average transaction volumes and storage needs
2. Per transaction price, can also be aggregated into transaction volume slabs
3. Per claim price, where transactions per claim can be estimated/averaged out and aggregated into claim volume slabs
4. A subscription charge based on estimated transaction volumes
5. Other factors that may evolve with ecosystem usage&#x20;
