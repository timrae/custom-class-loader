Port of the work in the [following blog](http://android-developers.blogspot.jp/2011/07/custom-class-loading-in-dalvik.html) 
to the new Gradle based Android Studio build system.

As the Android Studio Gradle plugin now provides [native multidex support](https://developer.android.com/tools/building/multidex.html),
which effectively solves the Android 65k method limit, the main motivation for using custom class loading at runtime is now 
extensibility. In my particular case, I'm trying to make a plugin framework for AnkiDroid.

Therefore the main focus of this version of the project is on building the secondary jar file in a clean and modular manner,
which makes it easy to update the main project without having to update the plugins.