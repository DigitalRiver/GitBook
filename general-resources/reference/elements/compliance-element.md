---
description: Learn how to use the Compliance element.
---

# Compliance element

With DigitalRiver.js, you can create a Compliance element that will automatically retrieve and build the compliance links that are required by Digital River. These links can be styled and placed on your page like other DigitalRiver.js elements.

## Creating a compliance element

To create a Compliance element, you should use the createElement function exposed through the DigitalRiver object.&#x20;

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
| `locale`  | Optional          | The language associated with the returned data. If you do not provide a locale and you provided a default locale when you started the DigitalRiver.js library, the strings will be localized to that default value. If you did not provide a default locale, the default language is English. | ar-EG, cs-CZ, da-DK, de-AT, de-CH, de-DE, el-GR, en-AU, en-BE, en-CA, en-CH, en-DK, en-FI, en-GB, en-IE, en-IN, en-MY, en-NL, en-NO, en-NZ, en-PR, en-SE, en-SG, en-US, en-ZA, es-AR, es-CL, es-CO, es-EC, es-ES, es-MX, es-PE, es-VE, et-EE, fi-FI, fr-BE, fr-CA, fr-CH, fr-FR, hu-HU, it-CH, it-IT, iw-IL, ja-JP, ko-KR, lt-LT, lv-LV, nl-BE, nl-NL, no-NO, pl-PL, pt-BR, pt-PT, ro-RO, ru-RU, sk-SK, sl-SI, sr-YU, sv-SE, th-TH, tr-TR, zh-CN, zh-HK, zh-TW |
| `entity`  | Required          | The entity facilitating the transaction.                                                                                                                                                                                                                                                      | DRES\_INC-ENTITY, DR\_WP-ENTITY, DR\_WPAB-ENTITY, C5\_INC-ENTITY, DR\_BRAZIL-ENTITY, DR\_BRAZIL2-ENTITY, DR\_CHINA-ENTITY, DR\_GMBH-ENTITY, DR\_INC-ENTITY, DR\_INDIA-ENTITY, DR\_IRELAND-ENTITY, DR\_JAPAN-ENTITY, DR\_KOREA-ENTITY, DR\_MEXICO-ENTITY, DR\_RUSSIA-ENTITY, DR\_TAIWAN-ENTITY, DR\_SARL-ENTITY, DR\_UK-ENTITY                                                                                                                                  |

### compliance.mount();

Call this function to place the created Compliance element on your page.

{% tabs %}
{% tab title="Example" %}
```
<div id="compliance"></div>

compliance.mount('compliance');
```
{% endtab %}
{% endtabs %}

### compliance.unmount();

Call this function to remove the Compliance element from your page. The element may be re-added to your page by calling mount().

{% tabs %}
{% tab title="Example" %}
```
compliance.unmount();
```
{% endtab %}
{% endtabs %}

### compliance.destroy();

Call this function to remove the Compliance element from your page as well as remove its functionality. You cannot re-add the destroyed element to your page via mount().

{% tabs %}
{% tab title="Example" %}
```
compliance.destroy();
```
{% endtab %}
{% endtabs %}

### compliance.update();

Call this function to update the Compliance element's data.

{% tabs %}
{% tab title="Example" %}
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
{% endtab %}
{% endtabs %}
