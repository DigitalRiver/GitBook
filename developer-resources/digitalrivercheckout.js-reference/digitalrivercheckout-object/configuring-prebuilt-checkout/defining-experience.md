---
description: >-
  Gain a better understanding of how to use the experience object to style a
  Prebuilt Checkout
---

# Defining experience

In [`options.style`](./#stylize-the-modal), you can use `experience` to assign values to the properties of the [CSS selectors](https://developer.mozilla.org/en-US/docs/Web/CSS/CSS\_selectors) that control [Prebuilt Checkout's](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#drop-in-checkout-modal-window) appearance and visual behavior.

{% hint style="success" %}
When defining a [create checkout-session request](https://www.digitalriver.com/docs/digital-river-api-reference/#tag/Drop-in-Checkout-Sessions/operation/createDropInCheckoutSession), you can also assign the [`experience`](defining-experience.md#the-complete-experience) object to [`style`](../../../digital-river-api-reference/checkout-sessions.md#style) .
{% endhint %}

On this page, you'll find:

* [A description of the primary parts of `experience`](defining-experience.md#primary-parts-of-experience)
* [Express payment method styling options](defining-experience.md#styling-express-payment-methods)
* [The rules that govern `experience`](defining-experience.md#the-rules-of-experience)
* [The complete `experience`](defining-experience.md#the-complete-experience)
* [Deprecated style objects](defining-experience.md#deprecated-style-objects)

{% hint style="info" %}
For details on how to perform even more granular styling of the [payment collection stage](../../../../integration-options/low-code-checkouts/drop-in-checkout.md#payment), refer to [Define the payment experience](./#define-the-payment-experience) on the [Configuring Prebuilt Checkout](./).&#x20;
{% endhint %}

## Primary parts of `experience`

* At the [`experience`](defining-experience.md#the-complete-experience) level are styles, which control Prebuilt Checkout's general, overall appearance, such as its `backgroundColor` and fonts, as well as the color and roundness of its border. At this level, you can also define a `logo`.\
  \
  &#x20;At the next level down in `experience` are `elements` and `sections`.&#x20;
* `elements` are the various parts of the `experience`, such as `progressBars`, `headings`, `text`, `tables`, `separators`, `links`, `textFields`, `checkboxes`, `radioButtons`, and `buttons`.
* `sections` are the various stages that users might pass through while checking out, along with the `header` and `footer` they see during each stage. With the exception of `header`, all `sections` have `elements`.
* The keys in the JSON correspond to a CSS property. The following are some common keys in the `experience` object and the CSS property that their value defines:

| JSON key          | CSS property                                                                          |
| ----------------- | ------------------------------------------------------------------------------------- |
| `borderRadius`    | [border-radius](https://developer.mozilla.org/en-US/docs/Web/CSS/border-radius)       |
| `backgroundColor` | [background-color](https://developer.mozilla.org/en-US/docs/Web/CSS/background-color) |
| `borderColor`     | [border-color](https://developer.mozilla.org/en-US/docs/Web/CSS/border-color)         |
| `textDecoration`  | [text-decoration](https://developer.mozilla.org/en-US/docs/Web/CSS/text-decoration)   |
| `fontStyle`       | [font-style](https://developer.mozilla.org/en-US/docs/Web/CSS/font-style)             |
| `fontFamily`      | [font-family](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family)           |
| `letterSpacing`   | [letter-spacing](https://developer.mozilla.org/en-US/docs/Web/CSS/letter-spacing)     |
| `color`           | [color](https://developer.mozilla.org/en-US/docs/Web/CSS/color)                       |
| `fontSize`        | [font-size](https://developer.mozilla.org/en-US/docs/Web/CSS/font-size)               |
| `fontWeight`      | [font-weight](https://developer.mozilla.org/en-US/docs/Web/CSS/font-weight)           |
| `boxShadow`       | [box-shadow](https://developer.mozilla.org/en-US/docs/Web/CSS/box-shadow)             |

* You can add [pseudo-class keywords](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) to change how something is styled based on its state or condition, such as when a user clicks a checkbox, hovers over a button or selects a payment method or when a value is determined to be invalid. In most cases, you define these keywords in `elements`.&#x20;

```json
"textFields": {
   ...
   ":hover": {
      "borderColor": "black"
   },
   ":focus": {
      "borderColor": "#00a7e1"
   },
   ":invalid": {
      "borderColor": "rgb(211, 47, 47)",
      "errorMessageColor": "rgb(211, 47, 47)"
   }
}
```

The following table captures examples of various styles you can control:

<table data-header-hidden><thead><tr><th width="414"></th><th></th></tr></thead><tbody><tr><td><code>experience.logo</code></td><td><img src="../../../../.gitbook/assets/image (198).png" alt="" data-size="original"></td></tr><tr><td><code>elements.progressBars.previous</code></td><td><img src="../../../../.gitbook/assets/image (227).png" alt="" data-size="original"></td></tr><tr><td><code>elements.progressBars.current</code></td><td><img src="../../../../.gitbook/assets/image (202).png" alt="" data-size="original"></td></tr><tr><td><code>elements.progressBars.future</code></td><td><img src="../../../../.gitbook/assets/image (201).png" alt="" data-size="original"></td></tr><tr><td><code>elements.headings</code></td><td><img src="../../../../.gitbook/assets/image (204).png" alt="" data-size="original"></td></tr><tr><td><code>elements.text</code></td><td><img src="../../../../.gitbook/assets/image (226).png" alt="" data-size="original"></td></tr><tr><td><code>elements.separators</code></td><td><img src="../../../../.gitbook/assets/image (205).png" alt="" data-size="original"></td></tr><tr><td><code>elements.links</code></td><td><img src="../../../../.gitbook/assets/image (206).png" alt="" data-size="original"></td></tr><tr><td><code>elements.textFields</code></td><td><img src="../../../../.gitbook/assets/image (207).png" alt="" data-size="original"></td></tr><tr><td><code>elements.textFields.label</code></td><td><img src="../../../../.gitbook/assets/image (208).png" alt="" data-size="original"></td></tr><tr><td><code>elements.checkboxes</code></td><td><img src="../../../../.gitbook/assets/image (209).png" alt="" data-size="original"></td></tr><tr><td><code>elements.checkboxes.label</code></td><td><img src="../../../../.gitbook/assets/image (210).png" alt="" data-size="original"></td></tr><tr><td><code>elements.radioButtons</code></td><td><img src="../../../../.gitbook/assets/image (211).png" alt="" data-size="original"></td></tr><tr><td><code>elements.radioButtons.label</code></td><td><img src="../../../../.gitbook/assets/image (212).png" alt="" data-size="original"></td></tr><tr><td><code>elements.buttons.forward</code></td><td><img src="../../../../.gitbook/assets/image (213).png" alt="" data-size="original"></td></tr><tr><td><code>elements.buttons.back</code></td><td><img src="../../../../.gitbook/assets/image (214).png" alt="" data-size="original"></td></tr><tr><td><code>elements.buttons.edit</code></td><td><img src="../../../../.gitbook/assets/image (215).png" alt="" data-size="original"></td></tr><tr><td><code>sections.header</code></td><td><img src="../../../../.gitbook/assets/image (216).png" alt="" data-size="original"></td></tr><tr><td><code>sections.footer</code></td><td><img src="../../../../.gitbook/assets/image (217).png" alt="" data-size="original"></td></tr><tr><td><code>sections.orderSummary</code></td><td><img src="../../../../.gitbook/assets/image (218).png" alt="" data-size="original"></td></tr><tr><td><code>sections.expressCheckout</code> <br><br>For details, refer to <a href="defining-experience.md#styling-express-payment-methods">Styling express payment methods</a>.</td><td><img src="../../../../.gitbook/assets/image (219).png" alt="" data-size="original"></td></tr><tr><td><code>sections.addressInformation</code></td><td><img src="../../../../.gitbook/assets/image (220).png" alt="" data-size="original"></td></tr><tr><td><code>sections.shippingChoice</code></td><td><img src="../../../../.gitbook/assets/image (221).png" alt="" data-size="original"></td></tr><tr><td><code>sections.taxIdentifiers</code></td><td><img src="../../../../.gitbook/assets/image (223).png" alt="" data-size="original"></td></tr><tr><td><a data-footnote-ref href="#user-content-fn-1"><code>sections.payment</code></a></td><td><img src="../../../../.gitbook/assets/image (224).png" alt="" data-size="original"></td></tr><tr><td><code>sections.payment.paymentMethodName</code></td><td><img src="../../../../.gitbook/assets/image (225).png" alt="" data-size="original"></td></tr></tbody></table>

## Styling express payment methods

You can use `expressCheckout` to style the various payment method buttons which display in that section.

### `payPal`

<table data-full-width="false"><thead><tr><th width="152">Key</th><th>Description</th><th>Supported values</th></tr></thead><tbody><tr><td><code>label</code></td><td>Customizes the button's label</td><td><code>paypal</code> (default), <code>pay</code>, <code>checkout</code>, <code>buynow</code></td></tr><tr><td><code>size</code></td><td>Sets the size of the button</td><td><code>responsive</code> (default), <code>small</code>, <code>medium</code>, <code>large</code> </td></tr><tr><td><code>color</code></td><td>Sets the color of the button</td><td><code>gold</code> (default), <code>silver</code>, <code>black</code>, <code>white</code>, <code>blue</code></td></tr><tr><td><code>shape</code></td><td>Determines whether the button is pill or rectangular shaped</td><td><code>pill</code> (default),  <code>rect</code></td></tr></tbody></table>

### `googlePay`

<table data-full-width="false"><thead><tr><th>Key</th><th>Description</th><th>Supported values</th></tr></thead><tbody><tr><td><code>buttonType</code></td><td>Defines the button's label and type</td><td><code>plain</code> (default), <code>long</code></td></tr><tr><td><code>buttonColor</code></td><td>Defines the button's background color</td><td><code>dark</code> (default), <code>light</code></td></tr></tbody></table>

### `applePay`

<table data-full-width="false"><thead><tr><th>Key</th><th>Description</th><th>Supported values</th></tr></thead><tbody><tr><td><code>buttonType</code></td><td>Defines the button's label and type</td><td><code>plain</code>, <code>buy</code></td></tr><tr><td><code>buttonColor</code></td><td>Defines the button's background color</td><td><code>light</code>, <code>light-outline</code>, <code>dark</code></td></tr></tbody></table>

### `amazonPay`

<table data-full-width="false"><thead><tr><th>Key</th><th>Description</th><th>Supported values</th></tr></thead><tbody><tr><td><code>buttonColor</code></td><td>Defines the button's background color</td><td><code>Gold</code> (default), <code>LightGray</code>, <code>DarkGray</code></td></tr></tbody></table>

## The rules of `experience`

The structure of [`experience`](defining-experience.md#the-complete-experience) determines which styles take precedence in the CSS. Generally, styles at a lower-level in the JSON hierarchy take precedence over styles at a higher level:

* A style in `elements` overrides that style in `experience`

```json
"experience": {
   ...
   "color": "#eb34de",
   ...
   "elements": {
       ...
      "text": {
          "color": "rgba(0, 0, 0, 0.87)",
	   ...
       }
       ...
  }
```

* A [pseudo-class selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) style in `elements` overrides that style in the same `elements`

```json
{
  "experience": {
    ...
    "elements": {
      ...
      "checkboxes": {
        "color": "rgba(0, 0, 0, 0.6)",
        ":checked": {
          "color": "#003058"
        },
        ...
      },
      ...
    },
    ...
    }
  }
}
```

* A style in `sections` overrides that style in `experience`

```json
{
  "experience": {
    ...
    "borderRadius": "30px",
    ...
    "sections": {
      ...
      "addressInformation": {
        "elements": {
          ...
          "textFields": {
            "borderRadius": "4px",
            ...
          },
          ...
        }
      },
      ...
    }
  }
}
```

* A style in an `elements` of `sections` overrides that style in the corresponding `elements`

```json
{
  "experience": {
    ...
    "elements": {
      ...
      "textFields": {
        ...
        "borderColor": "rgba(19, 0, 5, 0.23)",
        ...
      },
      ...
    },
    "sections": {
     ...
      "addressInformation": {
        "elements": {
          ...
          "textFields": {
            ...
            "borderColor": "rgba(0, 0, 0, 0.23)",
	     ...
          },
          ...
        }
      },
      ...
    }
  }
}
```

* A [pseudo-class selector](https://developer.mozilla.org/en-US/docs/Web/CSS/Pseudo-classes) style in an `elements` of `sections` overrides that pseudo-class selector style in the corresponding `elements`

```json
{
  "experience": {
    ...
    "elements": {
      ...
      "textFields": {
        ...
        ":hover": {
          "borderColor": "black"
        },
        ...
      },
      ...
    },
    "sections": {
     ...
      "addressInformation": {
        "elements": {
          ...
          "textFields": {
            ...
            ":hover": {
              "borderColor": "blue"
            },
            ...
          },
          ...
        }
      },
      ...
    }
  }
}
```

## The complete `experience`

The following is an example of the full `experience` object.

{% code lineNumbers="true" %}
```json
{
  "experience": {
    "logo": "https://www.digitalriver.com/wp-content/themes/digital-river-2022/assets/images/digital-river-logo-black-blue.svg",
    "backgroundColor": "#f0f4fa",
    "borderRadius": "30px",
    "borderColor": "rgba(0, 0, 0, 0.23)",
    "color": "#212121",
    "secondaryColor": "#757575",
    "fontFamily": "Kumbh Sans, Roboto,Arial, sans-serif",
    "fontStyle": "normal",
    "letterSpacing": "0",
    "elements": {
      "progressBars": {
        "previous": {
          "fill": "#003058",
          "color": "#003058"
        },
        "current": {
          "fill": "#003058",
          "color": "#003058"
        },
        "future": {
          "fill": "rgba(0, 0, 0, 0.38)",
          "color": "rgba(0, 0, 0, 0.6)"
        }
      },
      "headings": {
        "color": "#212121"
      },
      "text": {
        "color": "rgba(0, 0, 0, 0.87)",
        "fontSize": "0.875rem",
        "fontStyle": "normal",
        "label": {
          "fontWeight": 600
        }
      },
      "separators": {
        "color": "rgba(0, 0, 0, 0.12)"
      },
      "links": {
        "color": "#00a7e1",
        "textDecoration": "underline rgba(0, 0, 0, 0)",
        "footer": {
          "color": "#fff",
          "textDecoration": "underline rgba(0, 0, 0, 0)"
        }
      },
      "textFields": {
        "borderRadius": "4px",
        "borderColor": "rgba(0, 0, 0, 0.23)",
        "backgroundColor": "transparent",
        "color": "black",
        ":hover": {
          "borderColor": "black"
        },
        ":focus": {
          "borderColor": "#00a7e1"
        },
        ":invalid": {
          "borderColor": "rgb(211, 47, 47)",
          "errorMessageColor": "rgb(211, 47, 47)"
        },
        "label": {
          "color": "rgba(0, 0, 0, 0.87)",
          "fontSize": "0.875rem",
          "fontStyle": "normal"
        }
      },
      "checkboxes": {
        "color": "rgba(0, 0, 0, 0.6)",
        ":checked": {
          "color": "#003058"
        },
        "label": {
          "color": "rgb(33, 33, 33)"
        }
      },
      "radioButtons": {
        "color": "rgba(0, 0, 0, 0.6)",
        ":checked": {
          "color": "#003058"
        },
        ":focus": {
          "legend": {
            "color": "#00a7e1"
          }
        },
        "label": {
          "color": "rgb(33, 33, 33)",
          "fontStyle": "normal"
        },
        "legend": {
          "color": "rgba(0, 0, 0, 0.6)",
          "fontStyle": "normal"
        }
      },
      "buttons": {
        "forward": {
          "color": "#fff",
          "backgroundColor": "rgb(0, 48, 88)",
          ":hover": {
            "backgroundColor": "rgb(0, 167, 225)",
            "textColor": "#aed9f2",
            "boxShadow": "rgba(0, 0, 0, 0.2) 0px 2px 4px -1px, rgba(0, 0, 0, 0.14) 0px 4px 5px 0px, rgba(0, 0, 0, 0.12) 0px 1px 10px 0px"
          },
          ":active": {
            "boxShadow": "rgba(0, 0, 0, 0.2) 0px 5px 5px -3px, rgba(0, 0, 0, 0.14) 0px 8px 10px 1px, rgba(0, 0, 0, 0.12) 0px 3px 14px 2px"
          }
        },
        "back": {
          "color": "#212121",
          "backgroundColor": "transparent",
          ":hover": {
            "backgroundColor": "rgba(25, 118, 210, 0.04)"
          }
        },
        "edit": {
          "color": "#212121"
        }
      }
    },
    "sections": {
      "header": {
        "backgroundColor": "transparent",
        "showLogo": true
      },
      "footer": {
        "backgroundColor": "#001c33",
        "color": "#fff",
        "elements": {
          "links": {
            "textDecoration": "underline rgba(0, 0, 0, 0)",
            "color": "#fff"
          }
        }
      },
      "orderSummary": {
        "backgroundColor": "rgb(245, 247, 249)",
        "color": "black",
        "secondaryColor": "#757575",
        "elements": {
          "headings": {
            "fontWeight": 600,
            "color": "black"
          },
          "tables": {
            "productName": {
              "fontWeight": 600
            },
            "total": {
              "fontWeight": 600
            }
          }
        }
      },
      "expressCheckout": {
        "elements": {
          "headings": {
            "color": "black"
          }
        },
        "payPal": {
          "label": "checkout",
          "size": "responsive",
          "color": "gold",
          "shape": "pill"
        },
        "applePay": {
          "buttonType": "plain",
          "buttonColor": "dark"
        },
        "googlePay": {
          "buttonType": "plain",
          "buttonColor": "dark"
        },
        "amazonPay": {
          "buttonColor": "Gold"
        }
      },
      "addressInformation": {
        "elements": {
          "headings": {
            "color": "rgb(33, 33, 33)"
          },
          "textFields": {
            "borderRadius": "4px",
            "borderColor": "rgba(0, 0, 0, 0.23)",
            "backgroundColor": "transparent",
            "color": "black",
            ":hover": {
              "borderColor": "black"
            },
            ":focus": {
              "borderColor": "#00a7e1"
            },
            ":invalid": {
              "borderColor": "rgb(211, 47, 47)",
              "errorMessageColor": "rgb(211, 47, 47)"
            }
          },
          "checkboxes": {
            "color": "rgba(0, 0, 0, 0.6)",
            ":checked": {
              "color": "#003058"
            },
            "label": {
              "color": "rgb(33, 33, 33)"
            }
          }
        }
      },
      "shippingChoice": {
        "borderRadius": "4px",
        "elements": {
          "text": {
            "color": "rgb(33, 33, 33)",
            "fontSize": "0.875rem",
            "fontStyle": "normal",
            "label": {
              "fontWeight": 600
            }
          },
          "radioButtons": {
            "color": "rgba(0, 0, 0, 0.6)",
            ":checked": {
              "color": "#003058"
            },
            "label": {
              "color": "rgb(33, 33, 33)"
            }
          }
        }
      },
      "taxIdentifiers": {
        "elements": {
          "text": {
            "color": "rgb(33, 33, 33)",
            "fontSize": "0.875rem",
            "fontStyle": "normal",
            "label": {
              "fontWeight": 600
            },
            "appliedTaxIdentifier": {
              "color": "rgb(33, 33, 33)",
              "fontSize": "1.2rem",
              "fontStyle": "normal",
              "fontWeight": 400,
              "label": {
                "color": "rgba(0, 0, 0, 0.6)",
                "fontSize": "1rem",
                "fontStyle": "normal",
                "fontWeight": 400
              }
            }
          },
          "textFields": {
            "borderRadius": "4px",
            "borderColor": "rgba(0, 0, 0, 0.26)",
            "color": "rgb(33, 33, 33)",
            "label": {
              "color": "rgb(33, 33, 33)",
              "fontSize": "1rem",
              "fontStyle": "normal"
            }
          },
          "links": {
            "color": "#00a7e1",
            "textDecoration": "underline rgba(0, 0, 0, 0)"
          },
          "checkboxes": {
            "color": "rgba(0, 0, 0, 0.6)",
            ":checked": {
              "color": "#003058"
            },
            "label": {
              "color": "rgb(33, 33, 33)"
            }
          },
          "headings": {
            "color": "rgb(33, 33, 33)"
          },
          "radioButtons": {
            "color": "rgba(0, 0, 0, 0.6)",
            ":checked": {
              "color": "#003058"
            },
            ":focus": {
              "legend": {
                "color": "#00a7e1"
              }
            },
            "label": {
              "color": "rgb(33, 33, 33)",
              "fontStyle": "normal"
            },
            "legend": {
              "color": "rgba(0, 0, 0, 0.6)",
              "fontStyle": "normal"
            }
          }
        }
      },
      "payment": {
        "borderRadius": "4px",
        "paymentMethodName": {
          "color": "rgba(0, 0, 0, 0.75)",
          "fontSize": "1rem",
          "fontWeight": 400,
          "fontStyle": "normal",
          ":selected": {
            "color": "rgb(0, 167, 225)",
            "fontWeight": "bold",
            "fontStyle": "normal"
          }
        },
        "elements": {
          "text": {
            "color": "rgb(33, 33, 33)",
            "fontSize": "0.875rem",
            "fontStyle": "normal",
            "label": {
              "fontWeight": 600
            }
          },
          "textFields": {
            "borderRadius": "4px",
            "borderColor": "rgba(0, 0, 0, 0.26)",
            "color": "rgb(33, 33, 33)",
            "label": {
              "color": "rgba(0, 0, 0, 0.87)",
              "fontSize": "0.875rem",
              "fontStyle": "normal"
            }
          },
          "links": {
            "color": "#0000ee",
            "textDecoration": "underline",
            "footer": {
              "color": "rgba(0, 0, 0, 0.87)",
              "textDecoration": "none",
              ":hover": {
                "color": "#0000ee",
                "textDecoration": "underline"
              }
            }
          },
          "checkboxes": {
            ":checked": {
              "color": "#003058"
            },
            "label": {
              "color": "rgba(0, 0, 0, 0.87)"
            }
          }
        }
      }
    }
  }
}
```
{% endcode %}

## Deprecated style objects

The [`experience`](defining-experience.md#the-complete-experience) object is our recommended styling solution. However, in [`options.style`](./#stylize-the-modal), you can alternatively define `modal` and `textField`.

```javascript
const options = {
  style: {
    modal: {
      logo: 'https://www.mysite.com/logo.png',
      themeColor: {
        primary: '#00a7e1',
        highlight: '#b6e8fb',
        background: {
          header: '#b6e8fb',
          mainContent: '#fff',
          orderSummary: '#e4edf7',
          footer: '#001c33'
        },
        text: {
          link: '#003058',
          footerLink: '#0befc5',
          sectionHeading: '#083bf1',
          button: '#ffc439',
          textButton: '#0befc5'
        }
      },
      borderRadius: '3px',
      fontFamily: 'Arial, Helvetica, sans-serif',
      fontStyle: 'italic',
      fontVariant: 'normal',
      letterSpacing: '3px'
    },
    textField: {
      base: {
        color: '#00a7e1',
        fontFamily: 'Arial, Helvetica, sans-serif',
        fontSize: '20px',
        fontStyle: 'italic',
        fontVariant: 'normal',
        letterSpacing: '3px'
      },
      borderRadius: '4px'
    }
  }
};
```

[^1]: 
