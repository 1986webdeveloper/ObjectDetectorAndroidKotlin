# ObjectDetectorAndroidKotlin

This is demonstration of Object detection with the use of TensorFlow. TensorFlow is an end-to-end open source platform for machine learning.

App gets the current frames from the camera and it uses this frame to get predictions using the SSD-Mobilenet model trained using the Tensorflow Object Detection API.


A device running Android 5.0 (API 21) or higher is required to run the demo due to the use of the camera2 API.


<b>Requirements :</b>
- NDK (if you have not installed you can download it from here : https://developer.android.com/ndk/downloads)
- Tensorflow (if you have not installed you can download it from here : https://www.tensorflow.org/install)

<b>Here how to use it :</b>

- Add below code on top of your app level build.gradle file
```java
project.buildDir = 'gradleBuild'
getProject().setBuildDir('gradleBuild')

project.ext.ASSET_DIR = projectDir.toString() + '/assets'
project.ext.TMP_DIR   = project.buildDir.toString() + '/downloads'
apply from: "download-models.gradle"
```
- Add sourceSets inside android
```java
android{
        sourceSets {
           main {
               assets.srcDirs = [project.ext.ASSET_DIR]
                jniLibs.srcDirs = ['libs']
            }

          debug.setRoot('build-types/debug')
          release.setRoot('build-types/release')
          }
}
```
- Add tensorflow in your dependencies
```gradle
implementation 'org.tensorflow:tensorflow-android:1.13.1'
```
- OverlayView callback is used when object is tracked, which returns Canvas. So draw that canvas in camera preview inside DetectorActivity.
```java
trackingOverlay.addCallback(
        new OverlayView.DrawCallback() {
          @Override
          public void drawCallback(final Canvas canvas) {
            tracker.draw(canvas);
          }
        });
```

<b>Output:</b>

![alt text](https://github.com/1986webdeveloper/ObjectDetectorAndroidKotlin/blob/master/ezgif-4-0c8fe35564d4.gif)
