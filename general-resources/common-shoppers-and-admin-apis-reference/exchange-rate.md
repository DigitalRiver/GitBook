---
description: Understand how Digital River manages the exchange rate.
---

# Exchange rate

Digital River pulls a new exchange rate once a day and stores it. The SalesOrderActivity and [Settlement report](https://help.digitalriver.com/help/gc/Reports/Settlement-report.htm?Highlight=ePen) (ePen) apply this exchange rate to orders taken on that day. The SalesFeed includes the exchange rate on a per-order basis.

{% hint style="info" %}
Digital River uses the exchange rate on the day the shopper submitted the order. Not necessarily the day Digital River fulfilled the order.
{% endhint %}
