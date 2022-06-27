---
description: >-
  Commerce Layer changelog for software updates, new features, and general
  improvements.
---

# Changelog

#### :calendar\_spiral: June 23, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Introduced price volume and shipping weight tiers

Commerce Layer now supports tiered [pricing](https://commercelayer.io/docs/data-model/price-lists-and-currencies) strategies based on volume. These tiers can be used to enable specialized pricing when customers order in quantity, like offering a unit discount when a customer orders 10 of an SKU instead of 1.

We’ve introduced two new resources — [price tiers](https://docs.commercelayer.io/developers/v/api-reference/price-tiers) and [price volume tiers](https://docs.commercelayer.io/developers/v/api-reference/price-volume-tiers) — enabling you to create up to 5 tiers for each price. The price of the associated SKU will then be set by the tier the total quantity of items falls within. Price tiers can be [imported](https://docs.commercelayer.io/developers/importing-resources#importing-a-list-of-prices-with-price-tiers) together with their related prices.

The [shipping methods](https://docs.commercelayer.io/developers/v/api-reference/shipping\_methods) availability management has been improved:

* The relationships with the shipping zone and the shipping category has been relaxed (they're now both optional when [creating a shipping method](https://docs.commercelayer.io/developers/v/api-reference/shipping\_methods/create)).
* A new optional relationship with a stock location has been added so that the shipping method will only be available if the items are shipped from that specific stock location.
* A new optional weight-based constraint on the shipping method availability has been added. Now you can define a minimum and/or a maximum weight threshold and make the shipping method available only if the total weight of the items in the shipment falls within the threshold.

The shipping methods cost management has also been updated. Now you can select one of two schemes:

* _Flat_ — the shipping method has a fixed cost.
* _Weight-tiered_ — the [shipping method](https://commercelayer.io/docs/data-model/shipping-zones-and-methods)'s price is tiered based on the total weight of the items in the shipment. Two new resources have been introduced ([shipping method tiers](https://docs.commercelayer.io/developers/v/api-reference/shipping-method-tiers) and [shipping weight tiers](https://docs.commercelayer.io/developers/v/api-reference/shipping-weight-tiers)) so that you can create up to 5 price tiers for each shipping method.

A new [events](https://docs.commercelayer.io/developers/v/api-reference/events) endpoint has been exposed (which can be used to improve [webhooks](https://docs.commercelayer.io/developers/v/api-reference/webhooks) management and monitoring). Events can be included when fetching the resources that support them in order to inspect each recorded action.

![](.gitbook/assets/changelog-separator\_full-width.png)

#### :calendar\_spiral: June 20, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Introduced idempotency for payments

[Order](https://docs.commercelayer.io/developers/v/api-reference/orders) status changes are now idempotent. This means order and payment statuses stay consistent with multiple updates, which can limit the effect of transaction errors. For example, it's now possible to place or cancel an order more than once without worrying about duplicated transactions (or other unintended effects). Because of this, order status-related actions such as webhook events and stock item updates are only executed once.

[Adyen gateway](https://docs.commercelayer.io/developers/v/how-tos/payments/adyen) authorizations via 3DS now generate just one transaction.

![](.gitbook/assets/changelog-separator\_full-width.png)

#### ​:calendar\_spiral: June 7, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Improved bundle support for promotions

[Free gift](https://docs.commercelayer.io/developers/v/api-reference/free\_gift\_promotions) and [fixed price](https://docs.commercelayer.io/developers/v/api-reference/fixed\_price\_promotions) promotions can now apply to bundles (as long as they [share the same SKU list](https://docs.commercelayer.io/developers/v/api-reference/sku\_list\_promotion\_rules)). Both can now combine with other promotion types (but cannot overlap with each other or with other promotions of the same type). Two new relationships have also been added to the [order object](https://docs.commercelayer.io/developers/v/api-reference/orders/object) (`available_free_skus` and `available_free_bundles`), which is useful when presenting the customer with a list of possible free gifts during checkout.

![](.gitbook/assets/changelog-separator\_full-width.png)

#### :calendar\_spiral: May 3, 2022

[`Hosted checkout`](https://github.com/commercelayer/commercelayer-react-checkout)

### Checkout.com integration and error improvements in `v1.7.0`

Hosted checkout `v1.7.0` now supports [Checkout.com](https://docs.commercelayer.io/developers/v/how-tos/payments/checkout.com) out-of-the-box (in addition to all other [payment gateway integrations](https://docs.commercelayer.io/developers/v/how-tos/payments)). A new error handling process for _out-of-stock_ and _no shipping zone_ errors is now available.

![](.gitbook/assets/changelog-separator\_full-width.png)

#### :calendar\_spiral: May 2, 2022

[`React components`](https://github.com/commercelayer/commercelayer-react)

### Updated stock transfer components in `v3.11.1`

React components `v3.11.1` comes with valuable improvements regarding the stock transfer components. Now developers can customize [stock transfers](https://commercelayer.io/docs/data-model/users-and-organizations) alongside line items in a rapid and efficient way.

![](.gitbook/assets/changelog-separator\_full-width.png)

#### ​:calendar\_spiral: April 20, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### New token info endpoint

A new OAuth endpoint has been exposed. You can now unpack the JWT token information by sending a GET request to `oauth/tokeninfo`. The response will contain some useful info such as the application type, the owner, and the associated roles, permissions, and scopes.

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### ​:calendar\_spiral: April 14, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Avalara integration update (AvaTax)

[AvaTax](https://developer.avalara.com/avatax/dev-guide/transactions/document-types/) is a full-service engine for calculating transactional taxes, including sales, use, VAT, and many other tax types. If you're using [Avalara](https://docs.commercelayer.io/developers/v/api-reference/avalara\_accounts) as the tax calculator associated with one (or more) of your markets, you can now register tax computation on their systems (`SalesInvoice`). This is useful for tax returns in the US.

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### :calendar\_spiral: April 12, 2022

[`React components`](https://github.com/commercelayer/commercelayer-react)

### Klarna and Checkout.com integration in `v3.10.0`

React components `v3.10.0` now supports [Klarna](https://docs.commercelayer.io/developers/v/how-tos/payments/klarna) and [Checkout.com](https://docs.commercelayer.io/developers/v/how-tos/payments/checkout.com) out-of-the-box (in addition to all the other [payment gateway integrations](https://docs.commercelayer.io/developers/v/how-tos/payments)).

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### :calendar\_spiral: April 4, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Checkout.com integration and updates to importable resources

Commerce Layer API now supports [Checkout.com](https://docs.commercelayer.io/developers/v/how-tos/payments/checkout.com) out-of-the-box (in addition to all the other [payment gateway integrations](https://docs.commercelayer.io/developers/v/how-tos/payments)). [Bundles](https://docs.commercelayer.io/developers/importing-resources#importing-a-list-of-bundles) and [SKU options](https://docs.commercelayer.io/developers/importing-resources#importing-a-list-of-sku-options) have been added to the list of importable resources.

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### :calendar\_spiral: March 17, 2022

[`Hosted checkout`](https://github.com/commercelayer/commercelayer-react-checkout)

### Improved flow in `v1.5.0`

Hosted checkout `v1.5.0` features robust improvements on how the application state is managed, which translates into a speed boost and offers a way to hook on each user action. The checkout flow has also been streamlined by introducing auto-selection of the shipping method when the shipment only has a single shipping method available.

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### :calendar\_spiral: March 16, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Stripe integration optimizations

In order to prevent errors in some edge cases where an order can be placed after the authorization was created by the Stripe webhook, a large set of optimizations has been implemented on our [Stripe integration](https://docs.commercelayer.io/developers/v/how-tos/payments/stripe). Among them:

* A [control on order placement](https://docs.commercelayer.io/developers/v/how-tos/payments/stripe/adding-the-payment-source#authorization-check-on-order-placement) to check if the payment has been authorized has been introduced.
* Previously created Stripe's payment sources are now [nullified](https://docs.commercelayer.io/developers/v/how-tos/payments/stripe/adding-the-payment-source#payment-source-nullification) in case of order edit/refresh. The related authorizations are voided.
* The `_nullify_payment_source` trigger attribute has been added to the [order object](https://docs.commercelayer.io/developers/v/api-reference/orders/object) in case you want to force the payment source nullification.

On top of that, a [payment source](https://docs.commercelayer.io/developers/v/how-tos/checkout/adding-a-payment-source) nullification automation has been introduced for all _intent-based_ payments (e.g. Stripe, [Klarna](https://docs.commercelayer.io/developers/v/how-tos/payments/klarna/adding-the-payment-source#payment-source-nullification), [PayPal](https://docs.commercelayer.io/developers/v/how-tos/payments/paypal/adding-the-payment-source#payment-source-nullification)).

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### ​:calendar\_spiral: February 9, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### PayPal integration updates

Our [PayPal integration](https://docs.commercelayer.io/developers/v/how-tos/payments/paypal) has been updated and now uses the most recent PayPal [V2](./#klarna-integration-in-v3.10.0-1-1-2) libraries (no changes to the developer experience and integration functionalities).

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### ​:calendar\_spiral: January 19, 2022

[`Core API`](https://docs.commercelayer.io/developers/v/api-reference/)

### Klarna integration

Commerce Layer API now supports [Klarna](https://docs.commercelayer.io/developers/v/how-tos/payments/klarna) out-of-the-box (in addition to all the other [payment gateway integrations](https://docs.commercelayer.io/developers/v/how-tos/payments)).

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### :calendar\_spiral: January 18, 2022

​[`Hosted checkout`](https://github.com/commercelayer/commercelayer-react-checkout)

### Bundles management in `v1.1.0`

Hosted checkout `v1.1.0` now supports [bundles](https://commercelayer.io/docs/data-model/bundles), showing them in the order summary as a single line item and unpacking them in terms of single SKUs inside each shipment.

![](<.gitbook/assets/changelog-separator\_full-width (1).png>)

#### ​:calendar\_spiral: November 23, 2021

[`React components`](https://github.com/commercelayer/commercelayer-react)

### Switched to the new SDK in `v2.47.0`

React components `v2.47.0` start using our [new SDK](https://github.com/commercelayer/commercelayer-sdk) (the [previous one](https://github.com/commercelayer/commercelayer-js-sdk) is now deprecated, so make sure to update your code ASAP if you're still using it). This comes with improved performance, stability, and a lot of other new features.
