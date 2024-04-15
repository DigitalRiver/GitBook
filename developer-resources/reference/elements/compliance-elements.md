---
description: >-
  Gain a better understanding of what the compliance element does and how to use
  it.
---

# Compliance element

The compliance element displays the [selling entity](../../../integration-options/checkouts/creating-checkouts/selling-entities.md) facilitating a transaction and renders links to applicable disclosures, such as terms of sale, cookie policies, and cancellation rights.

<figure><img src="../../../.gitbook/assets/Compliance element (1).png" alt=""><figcaption></figcaption></figure>

On this page, you'll find information on how to [create](compliance-elements.md#creating-a-compliance-element), [mount](compliance-elements.md#mount), [unmount](compliance-elements.md#unmount), [destroy](compliance-elements.md#destroy), [update](compliance-elements.md#update), and [configure](compliance-elements.md#compliance-element-configuration-object) the element.

{% hint style="info" %}
For details on using the element in checkout flows, refer to [Displaying compliance disclosures](../../../integration-options/checkouts/creating-checkouts/#displaying-compliance-disclosures) on the [Building checkouts](../../../integration-options/checkouts/creating-checkouts/) page.&#x20;
{% endhint %}

## Creating a compliance element

To create a compliance element, pass `'compliance'` and its [configuration object](compliance-elements.md#compliance-element-configuration-object) to `createElement()`, which is exposed by the [`DigitalRiver` object](../../../payments/payment-integrations-1/digitalriver.js/reference/digitalriver-object.md#creating-a-digitalriver-object).

```javascript
var compliance = digitalRiver.createElement('compliance', complianceOptions);
```

## `mount()`

Call this function to place the created compliance element on your page.

```javascript
<div id="compliance"></div>

compliance.mount('compliance');
```

## `unmount()`

Call this function to remove the compliance element from your page. The element may be re-added to your page by calling [`mount()`](compliance-elements.md#mount).

```javascript
compliance.unmount();
```

## `destroy()`

Call this function to remove both the compliance element and its functionality from your page. You cannot re-add a destroyed element to your page via [`mount()`](compliance-elements.md#mount).

```javascript
compliance.destroy();
```

## `update()`

To refresh the compliance element, pass its [configuration object](compliance-elements.md#compliance-element-configuration-object) to `update()`.

```javascript
let complianceOptions = {
  compliance: {
    entity: 'DR_JAPAN-ENTITY'
  }
}
compliance.update(complianceOptions);
```

## Compliance element configuration object

The compliance element's configuration object contains a nested [`classes`](compliance-elements.md#classes) and [`compliance`](compliance-elements.md#compliance). &#x20;

### `classes`&#x20;

To stylize the compliance element, define the optional `classes`. For details, refer to [Custom classes](./#custom-classes).

```javascript
var complianceOptions = {
    classes: {
      base: 'DRElement'
    },
    ...
}
var compliance = digitalRiver.createElement('compliance', complianceOptions);
```

### `compliance`

The `compliance` object consists of a [`language`](compliance-elements.md#language), [`country`](compliance-elements.md#country), and [`entity`](compliance-elements.md#entity), all of which are required to make the element behave properly. Giving Digital River this data increases the probability that customers are shown accurately translated disclosures that apply to their shopping country.

For example, the following configuration results in the compliance element displaying the required disclosures, translated into Spanish, when customers are shopping in Germany, and [Digital River Ireland Ltd.](../../../integration-options/checkouts/creating-checkouts/selling-entities.md) is facilitating the transaction.

```javascript
var complianceOptions = {
    compliance: {
      entity: 'DR_IRELAND-ENTITY',
      language: 'es',
      country: 'DE'
    }
}
var compliance = digitalRiver.createElement('compliance', complianceOptions);
```

#### `language`

This required string determines the language of the text displayed in the element as well as the linked-to disclosure documents. The value you assign `language` doesn't affect what disclosures are displayed, only how their text is rendered.&#x20;

For a list of accepted values, refer to [Supported languages](../../supported-languages.md).&#x20;

#### `country`

A required string, formatted as an [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) code, represents the customer's shopping country. Since legal requirements vary slightly from country to country, the value you assign to this property determines which specific disclosures are rendered in the element. For example, some `country` values display a link to the customer's cancellation rights, while others do not.

If the transaction involves [physical products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), `country` should ideally be the same as the customer’s ship to country. If customers only purchase [digital products](../../../product-management/skus.md#how-products-are-classified-as-physical-or-digital), you can use their billing country.

#### `entity`

A required string that represents the transaction's designated [selling entity](../../../integration-options/checkouts/creating-checkouts/selling-entities.md). Like `compliance.country`, this property affects which disclosures are displayed in the element.

{% hint style="info" %}
In [checkouts](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts), you can find this value in `sellingEntity.id`.
{% endhint %}

For a list of accepted values, refer to [Supported selling entities](../../../integration-options/checkouts/creating-checkouts/selling-entities.md#supported-selling-entities).&#x20;

#### `jpCommerceLawPageUrl`

If `compliance.country` is `jp`, then the element displays a link to a disclosure that pertains to Japanese commercial transaction law.

If you'd like to replace the default URL behind this link with your own, use `jpCommerceLawPageUrl`.

```javascript
var complianceOptions = {
    classes: {
      base: 'DRElement'
    },
    compliance: {
      ...
      country: 'JP',
      jpCommerceLawPageUrl: 'https://acme.com/JapaneseCommerceLaw'
    }
}
var compliance = digitalRiver.createElement('compliance', complianceOptions);
```
