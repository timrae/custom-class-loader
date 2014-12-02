Port of the work in the [following blog](http://android-developers.blogspot.jp/2011/07/custom-class-loading-in-dalvik.html) 
to the new Gradle based Android Studio build system.

As the Android Studio Gradle plugin now provides [native multidex support](https://developer.android.com/tools/building/multidex.html),
which effectively solves the Android 65k method limit, the main motivation for using custom class loading at runtime is now 
extensibility. In my particular case, I'm trying to make a plugin framework for AnkiDroid.

Therefore the main focus of this version of the project is on building the secondary jar file in a clean and modular manner,
which makes it easy to update the main project without having to update the plugins. The main apk is in the app module, and the library which shows the toast is in the libraries/lib1 module with its own namespace `com.example.toastlib`

You can compile the .jar plugin file for the library using the `assembleExternalJar` task -- e.g. from the command line:

`gradlew assembleExternalJar`

which will generate the file `/libraries/lib1/build/outputs/com.example.toastlib.jar` which you can then copy to the sdcard on your device for the main app to import. 

To compile the main app it's currently necessary to make the following two changes to the build configuration:

change the first line of '/app/build.gradle' to `apply plugin: 'com.android.application'`
remove `':libraries:lib1'` from settings.gradle
