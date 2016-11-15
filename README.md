# plugin-barcode-ios
This plugin contains a lightweight, easy-to-use barcode scanner of the of official plugin for iOS 8+. This library is built on top of Apple's excellent AVFoundation framework, and will continue to receive updates as Apple releases them.

This plugin uses the following native library as a core.

https://github.com/mikebuss/MTBBarcodeScanner

This plugin fixed the memory leak present in the official plugin and requires less memory 

This library was born because the original library take a lot of memory and leave a lot of objects in the memory (memory leak), at moment to add this library you need to do all things manually but i think that in the next days I'll create the configuration to add this library by terminal.

# Step 1 

- You have to add `quartzCore.framework` 
<img width="1512" alt="adding-frameworks" src="https://cloud.githubusercontent.com/assets/11760456/20302434/309669b8-ab1f-11e6-8a80-6ec3be1527db.png">


- Copy **flash_off.imageset** and **flash_on.imageset** into the folder **Images.xcassets** in general you can find this into Resoureces group item (your xcode project)

- Copy **www/barcodescanner.js** into the folder **www/plugins** if you want a clean folder you can create a subfolder that you can call **cordova-plugin-barcodescanner**

- Copy the folder **cordova-plugin-barcodescanner** into your project, into this folder you can find all native code 

# Step 2

- Open your **config.xml** file and add this code:
```xml
 <feature name="BarcodeScanner">
        <param name="ios-package" value="CDVBarcodeScanner" />
 </feature>
```
- Open your **cordova_plugins.js** file and add the item below into **module.exports** array 
```js 
{
    "file": "plugins/cordova-plugin-barcodescanner/www/barcodescanner.js",
    "id": "cordova-plugin-barcodescanner.BarcodeScanner",
    "clobbers": [
      "cordova.plugins.barcodeScanner"
    ]
  }
```
**be carful where you see file you have to put your path where you have you put _barcodescanner.js_ file into _www_ folder**

iOS 10 it's mandatory to add a NSCameraUsageDescription in the info.plist.

NSCameraUsageDescription describes the reason that the app accesses the user’s camera. When the system prompts the user to allow access, this string is displayed as part of the dialog box.

So you need to open your info.plist file and add `Privacy - Camera Usage Description` and as a value `To scan barcodes`

#Using the plugin

The plugin creates the object `cordova/plugin/BarcodeScanner` with the method` scan(success, fail)`.
The following barcode types are currently supported:

- QR_CODE
- DATA_MATRIX
- UPC_E
- UPC_A
- EAN_8
- EAN_13
- CODE_128
- CODE_39
- ITF

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
          "preferFrontCamera" : true, 
          "showFlipCameraButton" : true, 
          "formats" : "QR_CODE,PDF_417" // default: all but PDF_417 and RSS_EXPANDED
      }
   );
```

# Encoding a Barcode

Not implemented 

# Note 
There is also another way to install this plugin you have to install before the [official plugin](https://github.com/phonegap/phonegap-plugin-barcodescanner) and after you have to replace the official classes with these classes

## Licence ##

The MIT License

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

