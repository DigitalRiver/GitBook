---
description: Learn how to localize purchase invoices and credit memos
---

# Localizing invoices and credit memos

To control how [purchase invoices and credit memos](../../../order-management/accessing-invoices-and-credit-memos.md) are localized, you can define the checkout's [`language`](designating-a-locale.md#language) or its [`locale`](designating-a-locale.md#locale).

## Language

If you send a [supported `language`](designating-a-locale.md#supported-languages) in a [create](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/createCheckouts) or [update](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts/operation/updateCheckouts) checkout request, then Digital River maps it to one of our [supported locales](designating-a-locale.md#supported-locales) and uses that value to set the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) [`locale`](designating-a-locale.md#locale).

### Supported languages

For a list of accepted values, refer to [Supported languages](../../../developer-resources/supported-languages.md).

## Locale

At the time of order creation, Digital River uses the [checkout's](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Checkouts) `locale` to set that same attribute in the [order](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Orders), which determines how [purchase invoices and credit memos](../../../order-management/accessing-invoices-and-credit-memos.md) are localized.&#x20;

The default value is `en-US`.

### Supported locales

The following table lists all the `locale` values, which combine a two-letter [ISO 639-1](https://en.wikipedia.org/wiki/ISO\_639-1) language code with an [ISO 3166-1 alpha-2](https://en.wikipedia.org/wiki/ISO\_3166-1\_alpha-2) country code, that Digital River supports:

| Locale  | Language  | Country                   |
| ------- | --------- | ------------------------- |
| `fr_BE` | French    | Belgium                   |
| `fr_CH` | French    | Switzerland               |
| `fr_FR` | French    | France                    |
| `fr_CA` | French    | Canada                    |
| `it_CH` | Italian   | Switzerland               |
| `it_IT` | Italian   | Italy                     |
| `nl_BE` | Dutch     | Belgium                   |
| `nl_NL` | Dutch     | Netherlands               |
| `no_NO` | Norwegian | Norway                    |
| `pl_PL` | Polish    | Poland                    |
| `ja_JP` | Japanese  | Japan                     |
| `ro_RO` | Romanian  | Romania                   |
| `ko_KR` | Korean    | Korea                     |
| `zh_CN` | Chinese   | China                     |
| `zh_TW` | Chinese   | Taiwan, Province of China |
| `cs_CZ` | Czech     | Czechia                   |
| `da_DK` | Danish    | Denmark                   |
| `fi_FI` | Finnish   | Finland                   |
| `de_AT` | German    | Austria                   |
| `de_CH` | German    | Switzerland               |
| `de_DE` | German    | Germany                   |
| `es_ES` | Spanish   | Spain                     |
| `sv_SE` | Swedish   | Sweden                    |
| `en_US` | English   | United States             |
