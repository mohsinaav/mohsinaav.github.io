---
layout: post
title: Contributions to open source project - 'html5-qrcode'
categories: Html
---

Html5-QRCode is a light-weight library to easily integrate QR code scanning functionality to a web application. All details regarding the project are clearly stated in it's github page - [html5-qrcode](https://github.com/mebjas/html5-qrcode). An end-to-end implementation is done by the author - [scanapp.org](https://scanapp.org/#reader). I recently came across it and had the chance to contribute to it by adding few changes. 

<img src="/assets/images/html5_qrcode_cam_default.png" alt="Homepage" width="500"/>

By default, the library would allow two type of scanning options - `Camera based scan` and `File based scan`. An [issue](https://github.com/mebjas/html5-qrcode/issues/405) was raised seeking an option to configure this scanning option. I was able to edit this configuration, such that the user can either use only `Camera based scan` or only `File based scan` or use in the default manner. 

```
let config = {
  fps: 10,
  qrbox: {width: 100, height: 100},
  rememberLastUsedCamera: true,
  // Only support camera scan type.
  supportedScanTypes: [
  Html5QrcodeScanType.SCAN_TYPE_CAMERA,
  Html5QrcodeScanType.SCAN_TYPE_FILE]
};
```
Here the property `supportedScanTypes` in the config, lets the user decide the type of scanning option. If you only need the camera as the scanning option, you can use the code below:
```
// Only support camera scan type.
supportedScanTypes: [Html5QrcodeScanType.SCAN_TYPE_CAMERA]
```
In case if only file scanning option is required, you can use this one:
```
// Only support file scan type.
supportedScanTypes: [Html5QrcodeScanType.SCAN_TYPE_FILE]
```
By default, both scanning options are available. Now, if you want the file based scanning to be the default option on page load, set the configuration as below:
```
// Only support camera scan type.
supportedScanTypes: [
Html5QrcodeScanType.SCAN_TYPE_FILE,
Html5QrcodeScanType.SCAN_TYPE_CAMERA]
```
This is how the scanapp.org would look like on using the above configurations.
|<img src="/assets/images/html5_qrcode_camera_selected.png" alt="Cam selected" width="300" height="300"/>| <img src="/assets/images/html5_qrcode_file_selected.png" alt="File Selected" width="300" height="300"/>|
|-----------------|------------------|
|Camera only option|File only option|

