DownloadableCalligraphy
=======================

This library provides a way to set default (downloadable) fonts using [Calligraphy](https://github.com/chrisjenx/Calligraphy) methods.

This library supports [Downloadable Font](https://developer.android.com/guide/topics/ui/look-and-feel/downloadable-fonts.html) of Support Library 26.

# Credit
This library based on [chrisjenx/Calligraphy](https://developer.android.com/guide/topics/ui/look-and-feel/downloadable-fonts.html)

And this library use [Android Support Library](https://developer.android.com/guide/topics/ui/look-and-feel/downloadable-fonts.html)


## Getting started

### Dependency

Latest Version : [ ![Download](https://api.bintray.com/packages/takahirom/maven/downloadable-calligraphy/images/download.svg) ](https://bintray.com/takahirom/maven/downloadable-calligraphy/_latestVersion)

```gradle
implementation 'com.github.takahirom.downloadable.calligraphy:downloadable-calligraphy:[Latest Version]'
```

### Add Fonts

You can use Bundled Font or Downloadable Font.

#### Downloadable Font
You can add Downloadable Font using Android Studio.  
https://developer.android.com/guide/topics/ui/look-and-feel/downloadable-fonts.html#via-android-studio

#### Bundled Font
Add your custom fonts to `res/font/`. You can see the Font Resource document.  
https://developer.android.com/guide/topics/resources/font-resource.html

### Usage

```xml
<TextView android:fontFamily="@font/my_font"/>
``` 

### Installation

Define your default font using `CalligraphyConfig`, in your `Application` class in the `#onCreate()` method.

```java
@Override
public void onCreate() {
    super.onCreate();
    CalligraphyConfig.initDefault(new CalligraphyConfig.Builder()
                            .setDefaultFont(R.font.roboto_regular)
                            .build()
            );
    //....
}
```

### Inject into Context

Wrap the `Activity` Context:

```java
@Override
protected void attachBaseContext(Context newBase) {
    super.attachBaseContext(CalligraphyContextWrapper.wrap(newBase));
}
```

_You're good to go!_


## Usage

### Custom font per TextView

```xml
<TextView
    android:text="@string/hello_world"
    android:layout_width="wrap_content"
    android:layout_height="wrap_content"
    android:fontFamily="@font/roboto_bold"/>
```

# FAQ

### Font Resolution 

The `CalligraphyFactory` looks for the font in a pretty specific order, for the _most part_ it's
 very similar to how the Android framework resolves attributes.
 
1. `View` xml - attr defined here will always take priority.
2. `Style` xml - attr defined here is checked next.
3. `TextAppearance` xml - attr is checked next, the only caveat to this is **IF** you have a font 
 defined in the `Style` and a `TextAttribute` defined in the `View` the `Style` attribute is picked first!
4. `Theme` - if defined this is used.
5. `Default` - if defined in the `CalligraphyConfig` this is used of none of the above are found 
**OR** if one of the above returns an invalid font. 

### Exceptions / Pitfalls

To our knowledge (try: `grep -r -e "void set[^(]*(Typeface " <android source dir>`) there are two standard Android widgets that have multiple methods to set typefaces. They are:

 - android.support.v7.widget.SwitchCompat
 - android.widget.Switch

Both have a method called `setSwitchTypeface` that sets the typeface within the switch (e.g. on/off, yes/no). `SetTypeface` sets the typeface of the label. You will need to create your own subclass that overrides `setTypeface` and calls both `super.setTypeface` and `super.setSwitchTypeface`.





# Collaborators

- [@mironov-nsk](https://github.com/mironov-nsk)
- [@Roman Zhilich](https://github.com/RomanZhilich)
- [@Smuldr](https://github.com/Smuldr)
- [@Codebutler](https://github.com/codebutler)
- [@loganj](https://github.com/loganj)
- [@dlew](https://github.com/dlew)
- [@ansman](https://github.com/ansman)

# Licence

    Copyright 2013 Christopher Jenkins,
    Modifications Copyright (C) 2017 takahirom

    Licensed under the Apache License, Version 2.0 (the "License");
    you may not use this file except in compliance with the License.
    You may obtain a copy of the License at
    
        http://www.apache.org/licenses/LICENSE-2.0
    
    Unless required by applicable law or agreed to in writing, software
    distributed under the License is distributed on an "AS IS" BASIS,
    WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    See the License for the specific language governing permissions and
    limitations under the License.
