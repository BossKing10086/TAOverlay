[![Build Status](https://travis-ci.org/TaimurAyaz/TAOverlay.svg?branch=master)](https://travis-ci.org/TaimurAyaz/TAOverlay) 

![TAOverlay](https://raw.githubusercontent.com/TaimurAyaz/TAOverlay/master/TAOverlayBanner.png)

**TAOverlay** is a minimalistic and simple overlay meant to display useful information to the user.  

![TAOverlay](https://raw.githubusercontent.com/TaimurAyaz/TAOverlay/master/screenshot.png)

## Requirements

* iOS 7.0+
* ARC

## Installation

* Drag the `TAOverlay/TAOverlay` folder into your project.
* Ensure that `TAOverlay.bundle` is added to `Targets->Build Phases->Copy Bundle Resources`.
* import `"TAOverlay.h"`

## Usage 

Using **TAOverlay** in your app is very simple.

### Showing TAOverlay

You can show the **TAOverlay** using one of the following:

```
+ (void) showOverlayWithLabel:(NSString *)status Options:(TAOverlayOptions)options;
```
* The `status` parameter is the text to display on the overlay. If the value is 'nil', overlay is shown without a label
* The `options` parameter is mask of options indicating the type and appearence of the overlay

```
+ (void) showOverlayWithLabel:(NSString *)status Image:(UIImage *)image Options:(TAOverlayOptions)options;
```
* The `status` parameter is the text to display on the overlay. If the value is 'nil', overlay is shown without a label
* The `image` parameter is the image to display as an icon on the overlay. The image **cannot** be 'nil'
* The `options` parameter is mask of options indicating the appearence of the overlay

```
+ (void) showOverlayWithLabel:(NSString *)status ImageArray:(NSArray *)imageArray Duration:(CGFloat)duration Options:(TAOverlayOptions)options;
```
* The `status` parameter is the text that you want displayed
* The `imageArray` parameter is an array containing UIImage objects. Use this if your animation is easily expressable in images. The array **cannot** be 'nil'
* The `duration` parameter is the duration of the animation to cycle through the array of images
* The `options` parameter is mask of options indicating the appearence of the overlay


### Dismissing TAOverlay

You can hide the **TAOverlay** using:

```
+ (void) hideOverlay;
```

### Example

```
[TAOverlay showOverlayWithLabel:@"This is the status" Options:(TAOverlayOptionOverlayTypeActivityDefault | TAOverlayOptionAllowUserInteraction | TAOverlayOptionOverlaySizeFullScreen | TAOverlayOptionAutoHide)];
```
The above shows the **TAOverlay** with the following properties:  

* It's **status** is "This is a status"
* It's **type** is the default iOS Activity Indicator
* It's **size** is fullscreen 
* It has **user interaction** enabled
* It has **auto hide** enabled  

*( More on these optons below )*



## Customization

**TAOverlay** has a lot of customization options. 

### TAOverlayOptions  

**TAOverlayOptions** defines the following set of bitmasks that can be used to fine tune the appearence of the overlay:  
*( passed as parameters in the "show" methods of TAOverlay )*

**Appearence options**

* `TAOverlayOptionOpaqueBackground` option indicates that the overlay does not have a blur effect, rather, a solid background
* `TAOverlayOptionOverlayShadow` options indicates that the overlay has a semi-transparent shadow over the whole screen behind it
* `TAOverlayOptionAllowUserInteraction` option indicates that the user can interact with objects behind the overlay
* `TAOverlayOptionAutoHide` option indicates that the overlay auto hides after a certain time, based on the length of the status string 

**Type options**

* `TAOverlayOptionOverlayTypeActivityDefault` option indicates that the overlay shows ongoing activity using the default iOS Activity Indicator
* `TAOverlayOptionOverlayTypeActivityLeaf` options indicates that the overlay shows ongoing activity using a custom activity indicator of the style of a leaf ***Default option***
* `TAOverlayOptionOverlayTypeActivityBlur` option indicates that the overlay shows ongoing activity using a custom activity indicator of the style of a blurred halo
* `TAOverlayOptionOverlayTypeActivitySquare` option indicates that the overlay shows ongoing activity using a custom activity indicator of the style of a rounded rectangle
* `TAOverlayOptionOverlayTypeSuccess` option indicates that the overlay shows a check mark inside a circle, signifying, successful completion of a task
* `TAOverlayOptionOverlayTypeWarning` option indicates that the overlay shows an exclamation mark inside a circle, warning the user of something
* `TAOverlayOptionOverlayTypeError` option indicates that the overlay shows a cross mark inside a circle, signifying, an un-successful event
* `TAOverlayOptionOverlayTypeInfo` option indicates that the overlay shows an information mark inside a circle, informing the user of something

**Size options**

* `TAOverlayOptionOverlaySizeFullScreen` option indicates that the overlay fills the whole screen
* `TAOverlayOptionOverlaySizeBar` options indicates that the overlay takes a bar like shape ***Default option***
* `TAOverlayOptionOverlaySizeRoundedRect` option indicates that the overlay takes a rounded rect shape

### Definitions

The header file includes the following definitions to tweak the appearence of the overlay:

* `OVERLAY_LABEL_FONT` The **font** of the status label
* `OVERLAY_LABEL_COLOR` The **text color** of the status label
* `OVERLAY_ACTIVITY_DEFAULT_COLOR` The **color** of the default type activity indicator
* `OVERLAY_ACTIVITY_LEAF_COLOR` The **color** of the leaf type activity indicator
* `OVERLAY_ACTIVITY_BLUR_COLOR` The **color** of the blur type activity indicator
* `OVERLAY_ACTIVITY_SQUARE_COLOR` The **color** of the square type activity indicator
* `OVERLAY_SHADOW_COLOR` The **color** of the semi-transparent shadow behind the overlay
* `OVERLAY_BACKGROUND_COLOR` The **color** of the background of the overlay
* `OVERLAY_BLUR_TINT_COLOR` The **tint color** of the blur of the overlay
* `OVERLAY_SUCCESS_COLOR` The **color** of the success icon
* `OVERLAY_WARNING_COLOR` The **color** of the warning icon
* `OVERLAY_ERROR_COLOR` The **color** of the error icon
* `OVERLAY_INFO_COLOR` The **color** of the information icon
* `OVERLAY_ICON_THICKNESS` The **thickness** of success, warning, error and information icons
* `ANIMATION_DURATION` The **animation duration** of the appearence and disappearence animations


### Custom images

Custom images can be shown using the latter of the "show" methods described above. **TAOverlay** includes a UIImage category for masking images to a specific color. Use the following method to do so:

```
- (UIImage *) maskImageWithColor:(UIColor *)color;
```
* The `color` parameter is the color with which a given image is masked
* The `return value` is the masked image


## Notifications

**TAOverlay** posts the following notifications via `NSNotificationCenter` in response to being shown/dismissed:

* `TAOverlayWillAppearNotification` when the show animation starts.
* `TAOverlayDidAppearNotification` when the show animation completes.
* `TAOverlayWillDisappearNotification` when the dismiss animation starts.
* `TAOverlayDidDisappearNotification` when the dismiss animation completes.

Each notification passes a `userInfo` dictionary holding the Overlay's status string (if any), retrievable via `TAOverlayStatusUserInfoKey`.

## ToDo

* Customization methods
* Add progress indicator
* Enhance overlay to more than just providing information

## Contributing to this project

If you have feature requests or bug reports, feel free to help out by sending pull requests or by [creating new issues](https://github.com/taimurayaz/TAOverlay/issues/new) :)
## Credits

**TAOverlay** is brought to you by Taimur Ayaz. If you're using **TAOverlay** in your project, attribution would be much appreciated :)

## License  

Copyright (c) 2015 Taimur Ayaz

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
