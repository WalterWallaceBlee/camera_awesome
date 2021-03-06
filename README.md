<p align="center">
	<a href="https://apparence.io/">
		<img src="https://github.com/Apparence-io/camera_awesome/raw/master/logo/banner.png" width="456" alt="camerawesome_logo">
	</a>
</p>

## 🚀&nbsp; Overview

Flutter plugin to add Camera support inside your project.

CamerAwesome include a lot of useful features like:

- 📲 Live camera **flip** ( switch between **rear** & **front** camera without rebuild ).
- ⚡️ No init needed, just add CameraAwesome widget !
- ⌛️ Instant **focus**.
- 📸 Device **flash** support.
- 🎚 **Zoom**.
- 🖼 **Fullscreen** or **SizedBox** preview support.
- 🎮 Complete example.
- 🎞 Taking a **picture** ( of course 😃 ).

## 📖&nbsp; Installation and usage

### Set permissions
   - **iOS** add these on ```ios/Runner/Info.plist``` file

```xml
<key>NSCameraUsageDescription</key>
<string>Your own description</string>
```

  - **Android**
    - Set permissions before ```<application>```
    <br />

    ```xml
    <uses-permission android:name="android.permission.CAMERA" />
    <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
    ```

    - Change the minimum SDK version to 21 (or higher) in ```android/app/build.gradle```
    <br />

    ```
    minSdkVersion 21
    ```

### Import the package
```dart
import 'package:camerawesome/camerawesome_plugin.dart';
```

### Define notifiers (if needed) & controller
ValueNotifier is a usefull change notifier from Flutter framework. It fires an event on all listener when value changes.
[Take a look here for ValueNotifier doc](https://api.flutter.dev/flutter/foundation/ValueNotifier-class.html)

```dart
class MyApp extends StatefulWidget {
  @override
  _MyAppState createState() => _MyAppState();
}

class _MyAppState extends State<MyApp> with TickerProviderStateMixin {
  // [...]
  // Notifiers
  ValueNotifier<CameraFlashes> _switchFlash = ValueNotifier(CameraFlashes.NONE);
  ValueNotifier<Sensors> _sensor = ValueNotifier(Sensors.BACK);
  ValueNotifier<Size> _photoSize = ValueNotifier(null);

  // Controller
  PictureController _pictureController = new PictureController();
  // [...]
}
```


If you want to change a config, all you need is setting the value. CameraAwesome will handle the rest.

Example:
```dart
_switchFlash.value = CameraFlashes.AUTO
```


### Create your camera

```dart
// [...]
@override
  Widget build(BuildContext context) {
    return CameraAwesome(
      testMode: false,
      onPermissionsResult: (bool result) { }
      selectDefaultSize: (List<Size> availableSizes) => Size(1920, 1080),
      onCameraStarted: () { },
      onOrientationChanged: (CameraOrientations newOrientation) { },
      zoom: 0.64,
      sensor: _sensor,
      photoSize: _photoSize,
      switchFlashMode: _switchFlash,
      orientation: DeviceOrientation.portraitUp,
      fitted: true,
    );
  };
// [...]
```


<details>
<summary>Reveal parameters list</summary>
<p>

| Param | Type  | Description | Required |
| ---   | ---   | ---         | --- |
| testMode | ```boolean``` | true to wrap texture |  |
| onPermissionsResult | ```OnPermissionsResult``` | implement this to have a callback after CameraAwesome asked for permissions |  |
| selectDefaultSize | ```OnAvailableSizes``` | implement this to select a default size from device available size list | ✅ |
| onCameraStarted | ```OnCameraStarted``` | notify client that camera started |  |
| onOrientationChanged | ```OnOrientationChanged``` | notify client that orientation changed |  |
| switchFlashMode | ```ValueNotifier<CameraFlashes>``` | change flash mode |  |
| zoom | ```ValueNotifier<double>``` | Zoom from native side. Must be between **0** and **1** |  |
| sensor | ```ValueNotifier<Sensors>``` | sensor to initiate **BACK** or **FRONT** | ✅ |
| photoSize | ```ValueNotifier<Size>``` | choose your photo size from the [selectDefaultSize] method |  |
| orientation | ```DeviceOrientation``` | initial orientation |  |
| fitted | ```bool``` | whether camera preview must be as big as it needs or cropped to fill with. false by default |  |

</p>
</details>

### Take a photo 🎉

```dart
await _pictureController.takePicture('THE_IMAGE_PATH/myimage.jpg');
```

## 📱&nbsp; Tested devices

CamerAwesome was developed to support **most devices** on the market but some feature can't be **fully** functional. You can check if your device support all feature by clicking bellow.

Feel free to **contribute** to improve this **compatibility list**.

<details>
<summary>Reveal grid</summary>
<p>

| Devices       | Flash | Focus | Zoom | Flip |
| ------------- | ----- | ----- | ---- | ---- |
| iPhone X      | ✅    | ✅    | ✅    | ✅   |
| iPhone 7      | ✅    | ✅    | ✅    | ✅   |
| One Plus 6T   | ✅    | ✅    | ✅    | ✅   |
| Xiaomi redmi  | ✅    | ✅    | ✅    | ✅   |
| Honor 7       | ✅    | ✅    | ✅    | ✅   |

</p>
</details>

## 🎯&nbsp; Our goals

Feel free to help by submitting PR !

- [ ] 📡 Broadcast live image stream
- [ ] 🎥 Record video
- [ ] 🌠 Focus on specific point
- [x] ~~🌤 Exposure level~~
- [x] ~~Add e2e tests~~
- [x] ~~Fullscreen/SizedBox support~~
- [x] ~~Complete example~~
- [x] ~~Take a picture~~
- [x] ~~Zoom level~~
- [x] ~~Live switching camera~~
- [x] ~~Device flash support~~
- [x] ~~Auto focus~~

## Sponsor
[Initiated and sponsored by Apparence.io.](https://apparence.io)


## 👥&nbsp; Contribution

Contributions are welcome.
Contribute by creating a PR or create an issue 🎉.