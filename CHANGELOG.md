# Changelog

## 3.2.0 - April 18, 2025

- Reusing JSONEncoder from CheckoutSheetKitSwift to reduce function overhead
- The UIColor extension now caches color instances to avoid redundant parsing of hex strings and creation of new UIColor objects

## 3.2.0 - December 18, 2024

- Handle geolocation requests for Android devices

## 3.1.2 - November 4, 2024

- Add `consumerProguardRules` build.gradle option to prevent minification of
  classes in release builds.

## 3.1.1 - November 1, 2024

- Logs invalid JSON for lifecycle events

## 3.1.0 - October 25, 2024

Upgrades Swift dependency to
[3.1.1](https://github.com/Shopify/checkout-sheet-kit-swift/releases/tag/3.1.1)
and Android to
[3.2.0](https://github.com/Shopify/checkout-sheet-kit-android/releases/tag/3.2.0).

### Updates

#### Both platforms

- New `invalidate()` function to manually clear the preload cache
- Prevent recovery flow for multipass URLs containing one-time tokens
- Open deep links externally

#### iOS

- Ignore cancelled redirects, add OS debug logging

### Android

- Implement `onShowFileChooser`, calling delegate
- Ensure no existing parent is present before adding to container

## 3.0.4 - October 14, 2024

- Fixes type imports/exports when `verbatimModuleSyntax` TS rule is enabled

## 3.0.3 - August 9, 2024

- Upgrades Swift and Android dependencies to `3.0.4`
- Updates Web Pixel schema

## 3.0.2 - August 6, 2024

- Upgrades Swift and Android dependencies to `3.0.3`

## 3.0.1 - June 19, 2024

- Upgrades the underlying Swift dependency, fixing an issue where pixel events
  do not fire after checkout completion.

## 3.0.0 - May 20, 2024

This version of the Checkout Sheet Kit ships with improvements to error
handling. Error messages will now contain `message`, `code` and `recoverable`
attributes.

In the event of a HTTP error, internal SDK error or mid-experience crash, the
Checkout Sheet Kit will now automatically invoke a recovery mechanism in an
effort to degrade gracefully.

Offering a world-class user experience is paramount, so please note that when
the recovery state occurs, there are caveats to the developer experience:

1. Checkout theming may fallback to the default checkout theme.
2. **Web pixels lifecycle events will not fire.**
3. `completed` events will contain an `orderId` _only_.

### Updated dependencies

- [`checkout-sheet-kit-swift@3.0.0`](https://github.com/Shopify/checkout-sheet-kit-swift/releases)
- [`checkout-sheet-kit-android@3.0.0`](https://github.com/Shopify/checkout-sheet-kit-android/releases)

## 2.0.1 - April 4, 2024

- Fixes an issue where opening `mailto` links externally causes the application
  to crash.

## 2.0.0 - March 21, 2024

### Updated dependencies

- [`checkout-sheet-kit-swift@2.0.1`](https://github.com/Shopify/checkout-sheet-kit-swift/releases)
- [`checkout-sheet-kit-android@2.0.1`](https://github.com/Shopify/checkout-sheet-kit-android/releases)

### New features

1. The loading spinner has been replaced by a progress bar. This will result in
   a faster perceived load time since the SDK will now no longer wait for full
   page load to show the DOM content.
2. The "title" of the webview is now configurable via a `Localizable.xcstrings`
   file on iOS, a `res/values/strings.xml` on Android or using the `title`
   attribute on the ShopifyCheckoutSheetKit configuration.

<!-- prettier-ignore -->
> [!IMPORTANT]
> The `title` attribute on the configuration will configure iOS _only_.

```diff
ShopifyCheckoutSheetKit.setConfig({
+ title: "Localized value"
})
```

1. The `completed` event now returns details about the order, including the
   order ID:

```diff
- const checkoutCompletedSubscription = shopify.addEventListener('completed', () => {
+ const checkoutCompletedSubscription = shopify.addEventListener('completed', event => {
+  console.log('[CheckoutCompletedEvent]', event.orderDetails.id);
});
```

### Breaking changes

1. `spinnerColor` has been replaced by `tintColor` for iOS and
   `progressIndicator` for android.

## 1.0.5 - March 5, 2024

- Updates the underlying swift SDK from `1.0.1` to `1.0.2` to include
  <https://github.com/Shopify/checkout-sheet-kit-swift/pull/143>

## 1.0.4 - March 4, 2024

- Fixes an issue where the parent view controller is dismissed after the
  checkout sheet is dismissed.

## 1.0.3 - February 21, 2024

- Fixes an issue where the checkout can remain in a frozen empty state after
  being dismissed.

## 1.0.2 - February 21, 2024

- Improve "close" event logic by only dismissing the Checkout sheet.

## 1.0.1 - February 20, 2024

- Adds support for view controllers other than the `rootViewController`. This
  allows triggering the Checkout Sheet from modals and formSheets etc.

## 1.0.0 - January 31, 2024

ShopifyCheckoutSheetKit is now generally available for
[Swift](https://github.com/Shopify/checkout-sheet-kit-swift),
[Android](https://github.com/Shopify/checkout-sheet-kit-android) and
[React Native](https://github.com/Shopify/checkout-sheet-kit-react-native) -
providing the world's highest converting, customizable, one-page checkout.

## 0.2.0 - January 30, 2024

Exposes a new `pixel` event type, which enables you to consume
[Standard](https://shopify.dev/docs/api/web-pixels-api/standard-events) and
[Custom](https://shopify.dev/docs/api/web-pixels-api/emitting-data#publishing-custom-events)
Web Pixels from Checkout and relay them to your third-party analytics providers.

## 0.1.1 - January 15, 2024

Updates the README on the NPM regsitry entry page.

## 0.1.0 - January 15, 2024

Initial publication of the `@shopify/checkout-sheet-kit` package.

Please refer to the [Readme](./README.md) for setup intstructions and usage.


