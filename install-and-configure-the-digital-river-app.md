---
description: Learn how to install and configure the Digital River app.
---

# Install and configure the Digital River app

## Step 1: Install the Digital River app

1. Download the Digital River app from [https://apps.vtex.com/](https://apps.vtex.com/).
2. Install the Digital River app in your account using the following command-line interface (CLI):\
   `vtex install vtexus.connector-digital-river`

If you have multiple VTEX accounts configured in a marketplace-seller relationship, install the Digital River app and repeat the following steps in each of the related accounts.&#x20;

## Step 2: Configure the Digital River settings

{% hint style="warning" %}
You must have a Digital River account and register all SKUs with Digital River. You can register the SKUs using this app's catalog sync feature or through the [Digital River API](https://docs.digitalriver.com/digital-river-api/). If a shopper attempts to check out with an unregistered SKU, the Digital River [Drop-in](https://docs.digitalriver.com/digital-river-api/payments/payment-integrations-1/drop-in) component will fail to load.&#x20;
{% endhint %}

1. Under the **Other** section in the admin sidebar, click `Digital River` and then `Configuration`.&#x20;
2. In the settings fields, enter your Digital River public key, Digital River token, VTEX app key, and VTEX app token.&#x20;
   * For initial testing, use a test Digital River token and leave the **Enable production mode** turned off.&#x20;
   * Turn on the **Enable automatic catalog sync** to enable syncing of SKUs from VTEX to Digital River each time you add or update a SKU in your VTEX catalog.&#x20;
   * Toggle the **Enable tax inclusive prices** to enable tax-inclusive prices if your catalog uses tax-inclusive product prices.
3. Click **Save Settings**.

{% hint style="warning" %}
For multiple VTEX accounts configured in a marketplace-seller relationship, use the same VTEX app key and VTEX app token for all of the accounts in which the app is installed. You can use any of the accounts to generate the key or token, and then grant additional permissions to the key or token by [creating a new user](https://help.vtex.com/en/tutorial/managing-users--tutorials\_512) on each of the other accounts using the VTEX app key in place of the user's email address, and then assigning the Owner role to that user.&#x20;
{% endhint %}

{% hint style="warning" %}
Digital River provides a tax calculation service. Therefore there should be no other tax calculation provider enabled on your account. If there is a tax calculation provider enabled on your account, you must disable it before you can configure Digital River.
{% endhint %}

## Step 3: Run the initial full catalog sync

{% hint style="warning" %}
You must enable the **Enable automatic catalog sync** setting before you can perform this step. See [Step 2: Configure the Digital River Settings](install-and-configure-the-digital-river-app.md#step-2-configure-the-digital-river-settings).
{% endhint %}

We recommended you run an initial full catalog sync between VTEX and Digital River. To do a full catalog sync:

1. Under the **Other** section in the admin sidebar, click **Digital River** and then click **Catalog Sync Logs**.&#x20;
2. Click the **SYNC CATALOG** button. This will send all current SKUs from your VTEX catalog to Digital River.&#x20;

{% hint style="warning" %}
Note that each product requires valid values for **Tax Code**, **ECCN**, and **Country of origin** in the VTEX catalog to be eligible to be sent to Digital River. The logs on this page will show whether the sync processed each SKU successfully or encountered an error due to missing information. Since this process runs in the background, there is a **RELOAD** button to refresh the logs.
{% endhint %}

## Step 4: Add Digital River Javascript to checkout6-custom.js

1. To add the following JavaScript to your checkout6-custom.js file, click **Store Setup** in your admin sidebar, click **Checkout**, then click the blue gear icon, and then click the **Code** tab.

```javascript
// DIGITAL RIVER Version 2.0.0
let checkoutUpdated = false
const digitalRiverPaymentGroupClass = '.DigitalRiverPaymentGroup'
const digitalRiverPaymentGroupButtonID =
  'payment-group-DigitalRiverPaymentGroup'

const digitalRiverPublicKey = 'pk_test_1234567890' // NOTE! Enter your Digital River public API key here

const paymentErrorTitle = 'Unable to check out with selected payment method.'
const paymentErrorDescription =
  'Please try a different payment method and try again.'
const loginMessage = 'Please log in to continue payment.'
const loginButtonText = 'LOG IN'
const addressErrorTitle = 'Incomplete shipping address detected.'
const addressErrorDescription =
  'Please check your shipping information and try again.'
const genericErrorTitle = 'Digital River checkout encountered an error.'
const genericErrorDescription =
  'Please check your shipping information and try again.'
let digitalriver
let digitalRiverCompliance

async function getCountryCode(country) {
  return await fetch(
    `${
      __RUNTIME__.rootPath || ``
    }/_v/api/digital-river/checkout/country-code/${country}`
  )
    .then((response) => {
      return response.json()
    })
    .then((json) => {
      return json.code
    })
}

function loadCompliance(orderForm) {
  const locale = orderForm && orderForm.clientPreferencesData && orderForm.clientPreferencesData.locale;
  const complianceOptions = {
    classes: {
      base: 'DRElement'
    },
    compliance: {
      locale,
      entity: 'DR_INC-ENTITY'
    }
  }
  if ($('#compliance').length == 0) {
    $('.container-main').append('<div id="compliance"></div>')
    digitalRiverCompliance = digitalriver.createElement('compliance', complianceOptions);
    digitalRiverCompliance.mount('compliance');
  } else {
    digitalRiverCompliance.update(complianceOptions);
  }
}

function renderErrorMessage(title, body, append = false) {
  if (!append) {
    $(digitalRiverPaymentGroupClass).html(
      `<div><div class='DR-card'><div class='DR-collapse DR-show'><h5 class='DR-error-message'>${title}</h5><div><p>${body}</p></div></div></div></div>`
    )
  
    return
  }

  $('#VTEX-DR-error').remove()
  $('.DR-pay-button').after(
    `<div id='VTEX-DR-error'><h5 class="DR-error-message">${title}</h5><div><p>${body}</p></div></div>`
  )
}

async function updateOrderForm(method, checkoutId) {
  const orderFormID = vtexjs.checkout.orderFormId

  return await $.ajax({
    url: `${window.location.origin}${
      __RUNTIME__.rootPath || ``
    }/api/checkout/pub/orderForm/${orderFormID}/customData/digital-river/checkoutId`,
    type: method,
    data: { value: checkoutId },
    success() {
      vtexjs.checkout.getOrderForm().done((orderForm) => {
        const { clientPreferencesData } = orderForm
        if (!clientPreferencesData) return
        return vtexjs.checkout.sendAttachment(
          'clientPreferencesData',
          clientPreferencesData
        )
      })
    },
  })
}

function showBuyNowButton() {
  $('.payment-submit-wrap').show()
}

function hideBuyNowButton() {
  $('.payment-submit-wrap').hide()
}

function clickBuyNowButton() {
  $('#payment-data-submit').click()
}

function loadDigitalRiverScript() {
  const e = document.createElement('script')

  ;(e.type = 'text/javascript'),
    (e.src = 'https://js.digitalriver.com/v1/DigitalRiver.js')
  const [t] = document.getElementsByTagName('script')

  t.parentNode.insertBefore(e, t)

  const f = document.createElement('link')

  ;(f.type = 'text/css'),
    (f.rel = 'stylesheet'),
    (f.href = 'https://js.digitalriverws.com/v1/css/DigitalRiver.css')
  const [u] = document.getElementsByTagName('link')

  u.parentNode.insertBefore(f, u)
}

function loadStoredCards(checkoutId) {
  fetch(`${__RUNTIME__.rootPath || ``}/_v/api/digital-river/checkout/sources?v=${new Date().getTime()}`)
    .then((response) => {
      return response.json()
    })
    .then(async (response) => {
      if (response.customer && response.customer.sources) {
        var sources = response.customer.sources
        if (sources.length > 0) {
          var radiosHtmls =
            '<div class="stored-credit-cards-title" style="margin-bottom: 16px;"><span class="DR-payment-method-name DR-payment-method-name-with-image" style="color: rgba(0,0,0,.75); font-size: 1rem; font-weight: 400; line-height: 20px; margin: 0px;">Saved Cards</span></div>'
          for (var i = 0; i < sources.length; i++) {
            radiosHtmls +=
              '<input name="DR-stored-cards" type="radio" id="' +
              sources[i].id +
              '" value="' +
              sources[i].id +
              '">'
            radiosHtmls +=
              '<label style="display: inline-block; vertical-align: sub; margin-bottom: 8px; margin-left: 4px; font-size: 0.875rem" for="' +
              sources[i].id +
              '">' +
              sources[i].creditCard.brand +
              ' ending with ' +
              sources[i].creditCard.lastFourDigits +
              ' expires ' +
              ('0' + sources[i].creditCard.expirationMonth).slice(-2) +
              '/' +
              sources[i].creditCard.expirationYear +
              '</label></br>'
          }
          radiosHtmls +=
            '<div class="stored-credit-cards" style="margin-top: 16px;"><button id="submit-stored-creditCard" style="background-color: #1264a3; color: #FFF; height: 56px; border-radius: .25rem; text-align: center; border-top: none!important; border: none; font-weight: 400; padding: 1rem; width: 250px; margin-bottom: 24px;">BUY NOW WITH SAVED CARD</button></div>'

          $('#drop-in').prepend(
            '<div class="DR-stored-cards">' + radiosHtmls + '</div>'
          )
          $('#submit-stored-creditCard').click(function () {
            var sourceId = $('input[name=DR-stored-cards]:checked').attr('id')
            fetch(
              `${
                __RUNTIME__.rootPath || ``
              }/_v/api/digital-river/checkout/update`,
              {
                method: 'POST',
                body: JSON.stringify({
                  checkoutId,
                  sourceId,
                  readyForStorage: false,
                }),
              }
            )
              .then((rawResponse) => {
                return rawResponse.json()
              })
              .then(() => {
                checkoutUpdated = true
                clickBuyNowButton()
              })
          })
          $('#' + sources[0].id).click()
        }
      }
    })
}

function loadDigitalRiver(orderForm) {
  const locale = orderForm && orderForm.clientPreferencesData && orderForm.clientPreferencesData.locale
    digitalriver = new DigitalRiver(digitalRiverPublicKey, {
      locale: locale ?? 'en-US',
    })
}

async function initDigitalRiver(orderForm) {
  hideBuyNowButton()

  if (
    $('#drop-in-spinner').length ||
    ($('#drop-in').length && $('#drop-in').html().length)
  ) {
    return
  }

  $(digitalRiverPaymentGroupClass).html(
    `<div id='drop-in-spinner'><i class="icon-spinner icon-spin"></i></div>`
  )

  $(digitalRiverPaymentGroupClass).append(`<div id='drop-in'></div>`)

  if (!orderForm.canEditData) {
    hideBuyNowButton()
    $(digitalRiverPaymentGroupClass).html(
      `<div><div class='DR-card'><div class='DR-collapse DR-show'><h5 class='DR-error-message'>${loginMessage}</h5><div><a style='cursor: pointer;' onClick='window.vtexid.start()' class='DR-button-text'>${loginButtonText}</a></div></div></div></div>`
    )
    return
  }

  fetch(`${__RUNTIME__.rootPath || ``}/_v/api/digital-river/checkout/create`, {
    method: 'POST',
    body: JSON.stringify({ orderFormId: orderForm.orderFormId, taxIdPayload: { // NOTE: The taxIdPayload field is optional
      taxId: {
        "type": "uk",
        "value": "GB999999999"
      },
      customerType: "business"
    }}),
  })
    .then((response) => {
      return response.json()
    })
    .then(async (response) => {
      const { checkoutId = null, paymentSessionId = null } = response

      if (!checkoutId || !paymentSessionId) {
        renderErrorMessage(genericErrorTitle, genericErrorDescription, false)

        return
      }

      await updateOrderForm('PUT', checkoutId)

      const country = await getCountryCode(
        orderForm.shippingData.address.country
      )

      const configuration = {
        sessionId: paymentSessionId,
        options: {
          flow: 'checkout',
          showComplianceSection: false,
          showSavePaymentAgreement: true,
          showTermsOfSaleDisclosure: true,
          button: {
            type: 'buyNow',
          },
        },
        billingAddress: {
          firstName: orderForm.clientProfileData.firstName,
          lastName: orderForm.clientProfileData.lastName,
          email: orderForm.clientProfileData.email,
          phoneNumber: orderForm.clientProfileData.phone,
          address: {
            line1: `${
              orderForm.shippingData.address.number
                ? `${orderForm.shippingData.address.number} `
                : ''
            }${orderForm.shippingData.address.street}`,
            line2: orderForm.shippingData.address.complement,
            city: orderForm.shippingData.address.city,
            state: orderForm.shippingData.address.state,
            postalCode: orderForm.shippingData.address.postalCode,
            country,
          },
        },
        onSuccess(data) {
          fetch(
            `${
              __RUNTIME__.rootPath || ``
            }/_v/api/digital-river/checkout/update`,
            {
              method: 'POST',
              body: JSON.stringify({
                checkoutId,
                sourceId: data.source.id,
                readyForStorage: data.readyForStorage,
              }),
            }
          )
            .then((rawResponse) => {
              return rawResponse.json()
            })
            .then(() => {
              checkoutUpdated = true
              clickBuyNowButton()
            })
        },
        onCancel(data) {},
        onError(data) {
          console.error(data)
          renderErrorMessage(paymentErrorTitle, paymentErrorDescription, true)
        },
        onReady(data) {
          loadStoredCards(checkoutId)
        },
      }
      const dropin = digitalriver.createDropin(configuration)
      $('#drop-in-spinner').remove();
      $('#drop-in').children().remove();
      dropin.mount('drop-in')
    })
}

$(document).ready(function () {
  loadDigitalRiverScript();
  if (~window.location.hash.indexOf('#/payment')) {
    if (
      $('.payment-group-item.active').attr('id') ===
      digitalRiverPaymentGroupButtonID
    ) {
      vtexjs.checkout.getOrderForm().done(function (orderForm) {
        loadDigitalRiver(orderForm);
        initDigitalRiver(orderForm)
      })
    } else {
      showBuyNowButton()
    }
  }
})

$(window).on('orderFormUpdated.vtex', function (evt, orderForm) {
  loadDigitalRiver(orderForm);
  loadCompliance(orderForm);
  if (
    ~window.location.hash.indexOf('#/payment') &&
    $('.payment-group-item.active').attr('id') ===
      digitalRiverPaymentGroupButtonID
  ) {
    if (
      !orderForm.shippingData.address ||
      !orderForm.shippingData.address.street ||
      !orderForm.shippingData.address.city ||
      !orderForm.shippingData.address.state ||
      !orderForm.shippingData.address.postalCode ||
      !orderForm.shippingData.address.country
    ) {
      return
    } else {
      initDigitalRiver(orderForm)
    }
  }
})
```

## Step 5: Configure payment settings

1. In your admin sidebar, click **Transactions**, click **Payments**, and then click **Settings**.
2. Click the **Gateway Affiliations** tab and then click the green plus sign to add a new affiliation.
3. Click **DigitalRiverV2** from the **Others** list.
4. Modify the **Affiliation name** if needed, choose an **Auto Settlement** behavior from the dropdown (Digital River recommends setting this to **Disabled: Do Not Auto Settle**), and then click **Save**. Leave **Application Key** and **Application Token** blank.
5. Click the **Payment Conditions** tab and click the green plus sign to add a new payment condition.
6. Click **DigitalRiver** from the **Other** list.
7. In the **Process with affiliation** dropdown, choose the name of the affiliation that you created in step 3 of this task.&#x20;
8. Set the **status** to **Active** and click **Save**.&#x20;

{% hint style="warning" %}
By clicking **Save**, you will activate the payment method in checkout!
{% endhint %}

## Step 5: Enable production mode

1. After successfully testing the payment method in test mode, under the **Other** section in the admin sidebar, click **Digital River**, and then click **Configuration**.&#x20;
2. Replace your test Digital River **** token with a production token, and turn on the **Enable Production mode** toggle.&#x20;
3. Click **Save**. Your checkout page will start accepting production orders.
