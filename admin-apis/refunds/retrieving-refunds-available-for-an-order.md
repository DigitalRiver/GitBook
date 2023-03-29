---
description: Learn how to get the available refunds for a specific order.
---

# Getting the available refunds for a specific order

Use the [`GET /orders/{orderId}/refunds-available`](https://drapi.io/commerce/test/#tag/Refund/paths/\~1orders\~1%7BorderId%7D\~1refunds-available/get) request to get the  amount available for a refund (`amountAvailableForRefund`) for the specified order identifier (`orderId`).

{% tabs %}
{% tab title="cURL" %}
{% code overflow="wrap" %}
```http
curl --location --request GET 'https://api.digitalriver.com/orders/{orderid}/refunds-available' \
--header 'authorization: bearer ***\
...
```
{% endcode %}
{% endtab %}

{% tab title="200 OK response" %}
{% code overflow="wrap" %}
```json
{
  "currency": "string",
  "lineItems": [
    {
      "lineItemId": "string",
      "price": {
        "total": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalTax": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalShipping": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalShippingTax": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalDutiesAndTariffs": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalDutiesAndTariffsTax": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalFee": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        },
        "totalFeeTax": {
          "amount": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountAvailableForRefund": {
            "value": 0,
            "formattedValue": "string"
          },
          "amountRefunded": {
            "value": 0,
            "formattedValue": "string"
          }
        }
      },
      "product": {
        "companyId": "string",
        "id": "string"
      },
      "status": "string"
    }
  ],
  "price": {
    "total": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalTax": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalShipping": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalShippingTax": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalDutiesAndTariffs": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalDutiesAndTariffsTax": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalFee": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    },
    "totalFeeTax": {
      "amount": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountAvailableForRefund": {
        "value": 0,
        "formattedValue": "string"
      },
      "amountRefunded": {
        "value": 0,
        "formattedValue": "string"
      }
    }
  },
  "status": "string"
}
```
{% endcode %}
{% endtab %}
{% endtabs %}
