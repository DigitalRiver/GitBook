---
description: >-
  Access a list of Digital River's supported languages and learn more about how
  to use them
---

# Supported languages

In certain API requests and JavaScript functions, you can pass a language value, which determines how checkout experiences, disclosures, purchase invoices, and credit memos get translated.

{% hint style="info" %}
For some languages, such as Chinese and English, you can also append a country or region code that localizes the translation.
{% endhint %}

Depending on whether you create your checkout experience using [Prebuilt Checkout](../integration-options/low-code-checkouts/drop-in-checkout.md) or take the [Direction Integrations](../integration-options/checkouts/) approach, refer to the following sections to learn more about which requests and functions accept a language and what behavior it controls:

{% tabs %}
{% tab title="Prebuilt Checkout" %}
* [Localize the checkout experience](digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/#localize-the-modal) on the [Configuring the modal](digitalrivercheckout.js-reference/digitalrivercheckout-object/configuring-prebuilt-checkout/) page
* [Language](digital-river-api-reference/checkout-sessions.md#language) on the [Checkout-sessions](digital-river-api-reference/checkout-sessions.md) page
{% endtab %}

{% tab title="Direct Integrations" %}
* [Initializing DigitalRiver.js](reference/digital-river-publishable-api-key.md)&#x20;
* [Getting compliance details](reference/digitalriver-object.md#digitalriver.compliance.getdetails-businessentitycode-locale) on the [`DigitalRiver` object](reference/digitalriver-object.md) page
* [Compliance element](reference/elements/compliance-elements.md)
* [Localizing invoices and credit memos](../integration-options/checkouts/creating-checkouts/designating-a-locale.md)
{% endtab %}
{% endtabs %}

The following are the supported values:

<table><thead><tr><th width="198">Language</th><th>Value</th></tr></thead><tbody><tr><td>Arabic</td><td><code>ar</code></td></tr><tr><td>Chinese Hong Kong</td><td><code>zh-hk</code></td></tr><tr><td>Chinese Simplified</td><td><code>zh-cn</code></td></tr><tr><td>Chinese Taiwan</td><td><code>zh-tw</code></td></tr><tr><td>Czech</td><td> <code>cs</code></td></tr><tr><td>Danish</td><td> <code>da</code></td></tr><tr><td>Dutch</td><td><code>nl</code></td></tr><tr><td>English</td><td><code>en</code></td></tr><tr><td>British English</td><td><code>en-gb</code></td></tr><tr><td>Finnish</td><td><code>fi</code></td></tr><tr><td>French</td><td><code>fr</code> </td></tr><tr><td>French Canadian</td><td><code>fr-ca</code></td></tr><tr><td>German</td><td><code>de</code></td></tr><tr><td>Greek</td><td><code>el</code></td></tr><tr><td>Hungarian</td><td><code>hu</code></td></tr><tr><td>Italian</td><td><code>it</code></td></tr><tr><td>Japanese</td><td><code>ja</code></td></tr><tr><td>Korean   </td><td><code>ko</code></td></tr><tr><td>Norwegian</td><td><code>no</code></td></tr><tr><td>Polish</td><td><code>pl</code></td></tr><tr><td>Portuguese</td><td><code>pt</code></td></tr><tr><td>Portuguese Brazil</td><td><code>pt-br</code></td></tr><tr><td>Russian</td><td><code>ru</code></td></tr><tr><td>Slovak</td><td><code>sk</code></td></tr><tr><td>Spanish</td><td><code>es</code></td></tr><tr><td>Latin American Spanish</td><td><code>es-419</code></td></tr><tr><td>Swedish</td><td><code>sv</code></td></tr><tr><td>Thai</td><td><code>th</code></td></tr><tr><td>Turkish</td><td><code>tr</code></td></tr></tbody></table>
