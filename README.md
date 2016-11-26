## React Native Android Library Boilerplate
This project serves as a boilerplate to create custom React Native native modules that can later be installed through NPM and easily be used in production.

## Getting started
1. Clone the project
2. Customize the project name by doing the following:
    * Edit `author` and `name` in `package.json`
    * Customize the Java package name (`com.domain.package`) as follows:
        1. Modify it in `android/src/main/AndroidManifest.xml`.
        2. Rename the folders starting from `android/src/main/java` to match your package name.
        3. Adjust `package io.cmichel.boilerplate;` in the top of the `Module.java` and `Package.java` files in `android/src/main//java/package/path` to match it.
    * Edit the name of your module in 

        ```java
        @Override
        public String getName() {
            return "Boilerplate";
        }
        ```

        and adjust it in `index.android.js`
3. Modify/Build the Project in Android Studio
    * Start `Android Studio` and select `File -> New -> Import Project` and select the **android** folder of this package.
    * If you get a `Plugin with id 'android-library' not found` Error, install `android support repository`.
    * If you get asked to upgrade _gradle_ to a new version, you can skip it.

## Installing it as a library in your main project
There are many ways to do this, here's the way I do it:

1. Push it to **GitHub**.
2. Do `npm install --save git+https://github.com/MrToph/react-native-android-library-boilerplate.git` in your main project.
3. Link the library:
    * Add the following to `android/settings.gradle`:
        ```
        include ':react-native-android-library-boilerplate'
        project(':react-native-android-library-boilerplate').projectDir = new File(settingsDir, '../node_modules/react-native-android-library-boilerplate/android')
        ```

    * Add the following to `android/app/build.gradle`:
        ```xml
        ...

        dependencies {
            ...
            compile project(':react-native-android-library-boilerplate')
        }
        ```
    * Add the following to `android/app/src/main/java/**/MainApplication.java`:
        ```java
        package com.motivation;

        import io.cmichel.boilerplate.Package;  // add this for react-native-android-library-boilerplate

        public class MainApplication extends Application implements ReactApplication {

            @Override
            protected List<ReactPackage> getPackages() {
                return Arrays.<ReactPackage>asList(
                    new MainReactPackage(),
                    new Package()     // add this for react-native-android-library-boilerplate
                );
            }
        }
        ```
4. Simply `import/require` it by the name defined in your library's `package.json`:

    ```javascript
    import Boilerplate from 'react-native-android-library-boilerplate'
    Boilerplate.show('Boilerplate runs fine', Boilerplate.LONG)
    ```
5. You can test and develop your library by importing the `node_modules` library into **Android Studio** if you don't want to install it from _git_ all the time.