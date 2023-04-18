# Bolt Quick Start for Composable Commerce

## Bolt's Checkout Package

This project adds Bolt's Managed Checkout Package to the SFCC PWA Starter Kit. This is Bolt's most comprehensive  integration. After selecting the checkout button, a Bolt-hosted checkout modal provides the full end-to-end checkout experience. The following features are included out of the box: 
- Access to the Bolt Account Network (~17 Million Shopper Accounts) that power a one-click checkout experience for logged in shoppers. 
- Passwordless authentication to recognize returning shoppers.
- A fully optimized checkout experience that includes Address Verification, Address Auto-Complete, form validation, etc.
- Native SFCC integrations for Shipping, Tax, Coupons, Order Creation, etc.
- Integrations with Alternative Payment Methods (PayPal, GooglePay, ApplePay, Klarna, AfterPay, ZipPay, etc)
- A rich collection of no-code configurable checkout settings. 

## PWA Integrations Details

### Bolt Code Additions
This repo includes two new files with the PWA Starter App:

1. A BoltButton component
2. A Custom Hook to load external scripts 

These are located in the `/app/bolt/` directory.

The `BoltButton` Component is used in the following files in the PWA Starter Kit: 
- `app/pages/cart/partials/cart-cta.jsx`
- `app/hooks/use-add-to-cart-modal.js`


### BoltButton Component
The `BoltButton` Component is defined in `/app/bolt/components/bolt-button.jsx`

The `BoltButton` Component uses a custom hook, defined in `/app/bolt/hooks/useExternalScripts`, to embed Bolt's Frontend JavaScript in the head of the DOM. 

After Bolt's Frontend JS is initialized, the `BoltButton` component invokes the `BoltCheckout.configure` passing the JWT to Bolt's Backend. 

The Bolt Button renders the Bolt Checkout button. 

![](/diagrams/checkout-init.png)

### Checkout Flow. 
Once a shopper launches the Bolt Checkout iFrame, Bolt handles the communication with SFCC on our backend via OCAPI endpoints. 

![](/diagrams/checkout-shipping-and-tax.png)

![](/diagrams/checkout-create-order-and-auth.png)


## SFRA Cartridge - Shared Integration Compontents 
The implementation of Bolt in the PWA uses the same SFCC backend as Bolt's SFRA Catridge. You can find the [Bolt Cartridge on the Appexchange](https://appexchange.salesforce.com/listingDetail?listingId=a0N4V00000Jx53PUAR&tab=e). Refer to [Bolt's SFRA Cartridge Integration Docs](https://help.bolt.com/products/checkout/sfcc-sfra-v2/installation/) for integration instructions.  
- Define web services and custom attributes via xml metadata imports
- Define the configuration settings in the Merchant Preferences in Business Manager
- Grant Bolt Access in Account Manager
- Specify the resources that Bolt can access via OCAPI 

## Open Issues / Next Steps
1. The current solution hard codes the Bolt Publishable key into into the Bolt Component. Technically this is fine, since the Bolt Publishable Key is not an API secret and is shared over the network. However, this be set dynamically via a configuration object (ideally pulled in from the Custom Bolt Merchant Preferences configured in Business Manager). 

2. The redirect to the native PWA CheckoutConfirmation.jsx has not yet been tested. In initial tests, we have used a [Bolt-hosted Order Confirmation page](https://help.bolt.com/add-ons/confirmation-page/) (an optional checkout add-on product that some merchants use).
