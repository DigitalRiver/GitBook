---
description: >-
  Gain a better understanding of what the compliance element does and how to use
  it.
---

# Compliance element

The compliance element displays the [selling entity](../../../shopper-apis/orders-1/selling-entities.md) facilitating a transaction and renders links to applicable disclosures, such as terms of sale, cookie policies, and cancellation rights.

<div align="left">

<figure><img src="../../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

</div>

On this page, you'll find information on [creating](compliance-element.md#creating-a-compliance-element), [mounting](compliance-element.md#mount), [unmounting](compliance-element.md#unmount), [destroying](compliance-element.md#destroy), [updating](compliance-element.md#update), and [configuring](compliance-element.md#compliance-element-configuration-object) the element.

## Creating a compliance element

To create a compliance element, pass `'compliance'` and its [configuration object](compliance-element.md#compliance-element-configuration-object) to `createElement()`, which is exposed by the [`DigitalRiver` object](../digitalriver-object.md).

{% tabs %}
{% tab title="Example" %}
{% code overflow="wrap" %}
```
var complianceOptions = {
  classes: {
    base: 'DRElement'
  },
  compliance: {
    locale: 'en-US',
    entity: 'DR_INC-ENTITY'
  }
}
var compliance = digitalRiver.createElement('compliance', complianceOptions);
```
{% endcode %}
{% endtab %}
{% endtabs %}

| Parameter | Required/Optional | Description                                                                                                                                                                                                                                                                                   | Accepted Values                                                                                                                                                                                                                                                                                                                                                                                                                                                |
| --------- | ----------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| locale    | Optional          | The language associated with the returned data. If you do not provide a locale and you provided a default locale when you started the DigitalRiver.js library, the strings will be localized to that default value. If you did not provide a default locale, the default language is English. | ar-EG, cs-CZ, da-DK, de-AT, de-CH, de-DE, el-GR, en-AU, en-BE, en-CA, en-CH, en-DK, en-FI, en-GB, en-IE, en-IN, en-MY, en-NL, en-NO, en-NZ, en-PR, en-SE, en-SG, en-US, en-ZA, es-AR, es-CL, es-CO, es-EC, es-ES, es-MX, es-PE, es-VE, et-EE, fi-FI, fr-BE, fr-CA, fr-CH, fr-FR, hu-HU, it-CH, it-IT, iw-IL, ja-JP, ko-KR, lt-LT, lv-LV, nl-BE, nl-NL, no-NO, pl-PL, pt-BR, pt-PT, ro-RO, ru-RU, sk-SK, sl-SI, sr-YU, sv-SE, th-TH, tr-TR, zh-CN, zh-HK, zh-TW |
| entity    | Required          | The entity facilitating the transaction.                                                                                                                                                                                                                                                      | DRES\_INC-ENTITY, DR\_WP-ENTITY, DR\_WPAB-ENTITY, C5\_INC-ENTITY, DR\_BRAZIL-ENTITY, DR\_BRAZIL2-ENTITY, DR\_CHINA-ENTITY, DR\_GMBH-ENTITY, DR\_INC-ENTITY, DR\_INDIA-ENTITY, DR\_IRELAND-ENTITY, DR\_JAPAN-ENTITY, DR\_KOREA-ENTITY, DR\_MEXICO-ENTITY, DR\_RUSSIA-ENTITY, DR\_TAIWAN-ENTITY, DR\_SARL-ENTITY, DR\_UK-ENTITY                                                                                                                                  |

## mount();

Call this function to place the created compliance element on your page.

```
<div id="compliance"></div>

compliance.mount('compliance');
```

## `unmount();`

Call this function to remove the compliance element from your page. The element may be re-added to your page by calling [mount()](compliance-element.md#mount).

```
compliance.unmount();
```

## destroy();

Call this function to remove the Compliance element from your page and its functionality. You cannot re-add the destroyed element to your page via [mount()](compliance-element.md#mount).

```
compliance.destroy();
```

## update();

Call this function to update the Compliance element's data.

```
let complianceOptions = {
  classes: {
    base: 'DRElement'
  },
  compliance: {
    locale: 'ja-JP',
    entity: 'DR_JAPAN-ENTITY'
  }
}
compliance.update(complianceOptions);
```

|   |
| - |
