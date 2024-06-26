# :camera: cordova-plugin-barcode-scanner

## Purpose of this Project

The purpose of this project is to provide a barcode scanner utilizing the Google ML Kit Vision library for the Cordova framework on Android devices while using AVCaptureSession on iOS devices.

It's based on the following plugins:
MobisysGmbH/cordova-plugin-mlkit-barcode-scanner
phonegap/phonegap-plugin-barcodescanner

## Plugin Dependencies

| Dependency                        | Version   | Info                       |
| --------------------------------- | --------- | -------------------------- |
| `cordova-android`                 | `>=8.0.0` |                            |
| `cordova-ios`                     | `>=4.5.0` |                            |
| `cordova-plugin-androidx`         | `^3.0.0`  | If cordova-android < 9.0.0 |

## Installation

Run this command in your project root:

```bash
cordova plugin add https://github.com/atruletech/cordova-plugin-barcode-scanner
```

## Supported Platforms

- Android
- iOS/iPadOS

## Barcode Support

| 1d formats   | Android | iOS |
| ------------ | ------- | --- |
| Codabar      | ✓       | ✓   |
| Code 39      | ✓       | ✓   |
| Code 93      | ✓       | ✓   |
| Code 128     | ✓       | ✓   |
| EAN-8.       | ✓       | ✓   |
| EAN-13       | ✓       | ✓   |
| ITF          | ✓       | ✓   |
| MSI          | ✗       | ✗   |
| RSS Expanded | ✗       | ✗   |
| RSS-14       | ✗       | ✗   |
| UPC-A        | ✓       | ✓   |
| UPC-E        | ✓       | ✓   |

| 2d formats  | Android | iOS |
| ----------- | ------- | --- |
| Aztec       | ✓       | ✓   |
| Codablock   | ✗       | ✗   |
| Data Matrix | ✓       | ✓   |
| MaxiCode    | ✗       | ✗   |
| PDF417      | ✓       | ✓   |
| QR Code     | ✓       | ✓   |

:information_source: Note that this API does not recognize barcodes in these forms:

- 1D Barcodes with only one character
- Barcodes in ITF format with fewer than six characters
- Barcodes encoded with FNC2, FNC3 or FNC4
- QR codes generated in the ECI mode

## Usage

To use the plugin simply call `cordova.plugins.barcodeScanner.scan(options, sucessCallback, failureCallback)`. See the sample below.

```javascript
cordova.plugins.barcodeScanner.scan(
  options,
  (result) => {
    // Do something with the data
    alert(result);
  },
  (error) => {
    // Error handling
  },
);
```

### Plugin Options

The default options are shown below.
All values are optional.

The detectorType can either be 'card' or null. When set to null, the focus rect is drawn as a square. When set to card it's drawn as a rectangle, ideal for scanning PDF417 driver's licenses or ID cards.

```javascript
const defaults = {
    beepOnSuccess: false,
    detectorType: null, // [ null | 'card' ]
    formats: {
        Code128: true,
        Code39: true,
        Code93: true,
        CodaBar: true,
        DataMatrix: true,
        EAN13: true,
        EAN8: true,
        ITF: true,
        QRCode: true,
        UPCA: true,
        UPCE: true,
        PDF417: false,
        Aztec: true,
    },
    rotateCamera: false, // Android only
    showTorchButton: true,
    vibrateOnSuccess: false,
};
```

### Output/Return value

```javascript
result: {
  text: string;
  format: string;
}
```
## Known Issues

On some devices the camera may be upside down.

Here is a list of devices with this problem:

- Zebra MC330K (Manufacturer: Zebra Technologies, Model: MC33)

Current Solution:
if your device has this problem, you can call the plugin with the option `rotateCamera` set to `true`.
This will rotate the camera stream by 180 degrees.

## Development

### Versioning

⚠️ Before incrementing the version in `package.json`, remember to increment the version in `plugin.xml` by hand.
