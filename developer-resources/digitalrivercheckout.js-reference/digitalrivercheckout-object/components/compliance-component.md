---
description: Learn how to remain compliant in a components checkout
---

# Compliance component

The compliance component displays localized hypertext that links customers to the terms and disclosures of the designated [selling entity](../../../../integration-options/checkouts/creating-checkouts/selling-entities.md).&#x20;

![](<../../../../.gitbook/assets/compliance element.png>)

To access Digital River's [merchant of record](https://www.digitalriver.com/merchant-of-record/) model, you'll need to design your experience so that this component is visible (mostly likely in the footer of the page) throughout every stage of the checkout process.&#x20;

{% hint style="success" %}
The only exception is the [payment component](payment-component.md). Digital River automatically embeds its disclosures within that component.&#x20;
{% endhint %}

## Creating the compliance component

To create an instance of the compliance component, pass `'compliance'` to [`createComponent()`](./#createcomponent-componenttype).

```javascript
let complianceComponent;
...
complianceComponent = components.createComponent('compliance');
...
```

## Mounting the compliance component

To attach the compliance component to your DOM, pass the `id` of its container to [`mount()`](./#mount-elementid).&#x20;

```javascript
<div id="compliance-container" style="display: block">
...
complianceComponent.mount('compliance-container');
...
```
