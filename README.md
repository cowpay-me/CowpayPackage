
# Cowpay iOS Framework Documentation

This repository provides comprehensive guidance on integrating the Cowpay iOS Framework into your iOS applications. The Cowpay framework allows seamless in-app payment processing, giving users a secure and efficient payment experience.

## Table of Contents

1. [Requirements](#requirements)
2. [Installation](#installation)
3. [Import](#import)
4. [Usage](#usage)
5. [Values Description](#values-description)

---

## Requirements

- **Minimum Xcode version**: 14.2
- **iOS Deployment**: 15.2 or later

## Installation

### 1. Manual Installation

1. Download the zip file from the [Versions page](https://lumin-soft.gitbook.io/cowpay/cowpay-ios-framework/versions).
2. Unzip the file to find `CowpayFramework.xcframework`.
3. Drag `CowpayFramework.xcframework` into your project’s Frameworks section.

### 2. Swift Package Manager

1. In Xcode, go to your project's **General** settings and select your target.
2. Scroll to the **Frameworks** section and click the **+** button.
3. Select **Add Other** > **Add Package Dependency**.
4. Enter the following URL in the search bar:  
   ```
   https://github.com/cowpay-me/CowpayPackage.git
   ```
5. You can add the latest version or specify an exact version by adjusting the **Dependency Rule**.
6. Click **Add Package** to complete the integration.

## Import

To use the framework, import it at the top of your Swift files:

```swift
import CowpayFramework
```

## Usage

### Step 1: Implement `CowpayCallBack` Protocol

This protocol provides callbacks to track payment status.

#### For UIKit
```swift
class YourViewController: UIViewController, CowpayCallBack {
    func onClosedByUser() {
        // Handle closure
    }
    func onSuccess(model: PaymentSuccessModel) {
        // Handle success
    }
    func onError(model: PaymentErrorModel) {
        // Handle error
    }
}
```

#### For SwiftUI
```swift
struct YourView: View, CowpayCallBack {
    func onClosedByUser() {
        // Handle closure
    }
    func onSuccess(model: PaymentSuccessModel) {
        // Handle success
    }
    func onError(model: PaymentErrorModel) {
        // Handle error
    }
}
```

### Step 2: Initialize Payment Info

Define the payment details using the `PaymentInfo` model:

```swift
let paymentInfo = try PaymentInfo(
    description: "Transaction Description",
    merchantReferenceId: "UniqueReferenceID",
    amount: 100.0,
    customerEmail: "user@example.com",
    customerFirstName: "John",
    customerLastName: "Doe",
    customerMobile: "0123456789",
    customerMerchantProfileId: "CustomerID",
    isFeesOnCustomer: true
)
```

### Step 3: Configure `CowpayInitModel`

Set up the `CowpayInitModel` with necessary details and callback protocol.

```swift
let cowpayInitModel = try CowpayInitModel(
    merchantCode: "YourMerchantCode",
    merchantHashCode: "YourMerchantHashCode",
    merchantMobile: "0123456789",
    logoStringUrl: "https://example.com/logo.png",
    cowpayEnvironment: .staging,
    localizationCode: .en,
    cowpayCallback: self,
    paymentInfo: paymentInfo
)
```

### Step 4: Launch Cowpay Payment

#### For UIKit
```swift
let cowpayViewController = CowpayFrameWork.initCowpayViewController(cowpayInitModel: cowpayInitModel)
self.present(cowpayViewController, animated: true)
```

#### For SwiftUI
```swift
NavigationLink(
    destination: CowpayFrameWork.initCowpaySwiftUIView(cowpayInitModel: cowpayInitModel),
    isActive: $navigateKey
) { EmptyView() }
```

## Values Description

| Key                     | Description                                                                         |
|-------------------------|-------------------------------------------------------------------------------------|
| `localizationCode`      | Language code; `.en` for English, `.ar` for Arabic (default is `.en`).              |
| `amount`                | Payment amount, two decimal values like "15.60".                                    |
| `customerEmail`         | Customer's valid email.                                                             |
| `customerMobile`        | International format customer mobile.                                               |
| `customerFirstName`     | Customer's first name.                                                              |
| `customerLastName`      | Customer's last name.                                                               |
| `isFeesOnCustomer`      | Boolean for whether fees are on customer (default is `false`).                      |
| `logoStringUrl`         | URL for merchant's logo (optional).                                                 |
| `merchantMobile`        | Merchant's mobile number.                                                           |
| `description`           | Charge request description.                                                         |
| `customerMerchantProfileId` | Customer profile ID on your system.                                           |
| `merchantReferenceId`   | Unique identifier for the charge request.                                           |
| `cowpayEnvironment`     | `.staging` or `.production`.                                                        |
| `merchantHashCode`      | Hash code available in your Cowpay dashboard.                                       |
| `merchantCode`          | Merchant code from your Cowpay dashboard.                                           |
| `onSuccess`             | Callback when a transaction succeeds.                                               |
| `onError`               | Callback when an error occurs.                                                      |
| `onClosedByUser`        | Callback when user closes the payment interface.                                    |


---

For further assistance, please visit our [documentation](https://lumin-soft.gitbook.io/cowpay/cowpay-ios-framework) or contact Cowpay support.
