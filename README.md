# Cordova Plugin Qrcode Barcode Scanner
================================

## Installation

Install via repo url directly ( unstable )

    phonegap plugin add https://github.com/seamlink-dev/cordova-plugin-qrcode-barcode-scanner.git

Optional variables:
This plugin requires the Android support library v4. The minimum version is `24.1.0`. Default value is `27.+`.  Check out the latest version [here](https://developer.android.com/topic/libraries/support-library/revisions.html).
```
phonegap plugin add https://github.com/seamlink-dev/cordova-plugin-qrcode-barcode-scanner.git --variable ANDROID_SUPPORT_V4_VERSION="27.1.1"
```
### Supported Platforms

- Android
- iOS

Note: the Android source for this project includes an Android Library Project.
plugman currently doesn't support Library Project refs, so its been
prebuilt as a jar library. Any updates to the Library Project should be
committed with an updated jar.

## Using the plugin ##
The plugin creates the object `cordova.plugins.barcodeScanner` with the method `scan(success, fail)`.

The following barcode types are currently supported:

|  Barcode Type | Android | iOS |
|---------------|:-------:|:---:|
| QR_CODE       |    ✔    |  ✔  |
| DATA_MATRIX   |    ✔    |  ✔  |
| UPC_A         |    ✔    |  ✔  |
| UPC_E         |    ✔    |  ✔  |
| EAN_8         |    ✔    |  ✔  |
| EAN_13        |    ✔    |  ✔  |
| CODE_39       |    ✔    |  ✔  |
| CODE_93       |    ✔    |  ✔  |
| CODE_128      |    ✔    |  ✔  |
| CODABAR       |    ✔    |  ✖  |
| ITF           |    ✔    |  ✔  |
| RSS14         |    ✔    |  ✖  |
| PDF_417       |    ✔    |  ✔  |
| RSS_EXPANDED  |    ✔    |  ✖  |
| MSI           |    ✖    |  ✖  |
| AZTEC         |    ✔    |  ✔  |

`success` and `fail` are callback functions. Success is passed an object with data, type and cancelled properties. Data is the text representation of the barcode data, type is the type of barcode detected and cancelled is whether or not the user cancelled the scan.

A full example could be:
```js
   cordova.plugins.barcodeScanner.scan(
      function (result) {
          alert("We got a barcode\n" +
                "Result: " + result.text + "\n" +
                "Format: " + result.format + "\n" +
                "Cancelled: " + result.cancelled);
      },
      function (error) {
          alert("Scanning failed: " + error);
      },
      {
          preferFrontCamera : true, // iOS and Android
          showFlipCameraButton : true, // iOS and Android
          showTorchButton : true, // iOS and Android
          torchOn: true, // Android, launch with the torch switched on (if available)
          saveHistory: true, // Android, save scan history (default false)
          prompt : "Place a barcode inside the scan area", // Android
          resultDisplayDuration: 500, // Android, display scanned text for X ms. 0 suppresses it entirely, default 1500
          formats : "QR_CODE,PDF_417", // default: all but PDF_417 and RSS_EXPANDED
          orientation : "landscape", // Android only (portrait|landscape), default unset so it rotates with the device
          disableAnimations : true, // iOS
          disableSuccessBeep: false // iOS and Android
      }
   );
```

## Encoding a Barcode ##

The plugin creates the object `cordova.plugins.barcodeScanner` with the method `encode(type, data, success, fail)`.

Supported encoding types:

* TEXT_TYPE
* EMAIL_TYPE
* PHONE_TYPE
* SMS_TYPE

```
A full example could be:

   cordova.plugins.barcodeScanner.encode(cordova.plugins.barcodeScanner.Encode.TEXT_TYPE, "http://www.nytimes.com", function(success) {
            alert("encode success: " + success);
          }, function(fail) {
            alert("encoding failed: " + fail);
          }
        );
```

## iOS quirks ##

Since iOS 10 it's mandatory to add a `NSCameraUsageDescription` in the `Info.plist`.

`NSCameraUsageDescription` describes the reason that the app accesses the user's camera.
When the system prompts the user to allow access, this string is displayed as part of the dialog box. If you didn't provide the usage description, the app will crash before showing the dialog. Also, Apple will reject apps that access private data but don't provide an usage description.

To add this entry you can use the `edit-config` tag in the `config.xml` like this:

```
<edit-config target="NSCameraUsageDescription" file="*-Info.plist" mode="merge">
    <string>To scan barcodes</string>
</edit-config>
```

## Thanks on Github ##

So many -- check out the original [iOS](https://github.com/phonegap/phonegap-plugins/tree/DEPRECATED/iOS/BarcodeScanner),  [Android](https://github.com/phonegap/phonegap-plugins/tree/DEPRECATED/Android/BarcodeScanner) and
[BlackBerry 10](https://github.com/blackberry/WebWorks-Community-APIs/tree/master/BB10-Cordova/BarcodeScanner) repos.

## Licence ##

The MIT License

Copyright (c) 2010 Matt Kane

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in
all copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN
THE SOFTWARE.
