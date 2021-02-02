## GlideWebpDecoder

[![license](http://img.shields.io/badge/license-Apache2.0-brightgreen.svg?style=flat)](https://github.com/zjupure/GlideWebpDecoder/blob/master/LICENSE)
[![Release Version](https://img.shields.io/badge/release-2.0-red.svg)](https://github.com/zjupure/GlideWebpDecoder/releases)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg)](https://github.com/zjupure/GlideWebpDecoder/pulls)

GlideWebpDecoder is a [Glide](https://github.com/bumptech/glide) integration library for decoding and displaying webp images on Android platforms. It is based on [libwebp](https://github.com/webmproject/libwebp) project and takes some implementation from [Fresco](https://github.com/facebook/fresco) and [GlideWebpSupport](https://github.com/roths/GlideWebpSupport) as references.

## Features

* play animated webp images on all Android versions
* show transparent or lossless webp images on Android devices lower than 4.2.1 (BitmapFactory support webp decode on 4.2+ android system so we have no need to handle)

## Dependency Integration

Library is available in jcenter. If you build with Gradle, just add the following dependencies to your `build.gradle` file.
Different Glide version is corresponding to different GlideWebpDecoder due to the annotation processor compatibility. The version rule of GlideWebpDecoder is "{major_version}.{glide_version}".
For example, if you use glide 4.12.0, the corresponding version of GlideWebpDecoder should be 2.0.4.12.0

Library will only follow the latest three version of Glide. If you use a lower version glide, please clone the project and modify it yourself.

**Notice**

Since Glide 4.10.0 has migrate to AndroidX, so your project must use AndroidX with Glide 4.10.0+. 

WebpDecoder with AndroidX support starts from version 1.6.{GLIDE_VERSION} and won't support glide version below 4.10.0 anymore.

If your project use glide version below 4.10.0, you can only use webpdecoder 1.6 version or below.


```gradle
def GLIDE_VERSION = "4.12.0"
// webpdecoder
implementation "com.zlc.glide:webpdecoder:2.0.${GLIDE_VERSION}"
// glide 4.10.0+
implementation "com.github.bumptech.glide:glide:${GLIDE_VERSION}"
annotationProcessor "com.github.bumptech.glide:compiler:${GLIDE_VERSION}"
```

Then you are free to use GlideWebpDecoder just like using other Glide integration library.

## Usage

Basic usage see [Glide](https://github.com/bumptech/glide) API [documents](https://bumptech.github.io/glide/)

If you want to use `BitmapTransformation` or library [glide-transformations](https://github.com/wasabeef/glide-transformations), please use `WebpDrawableTransformation` to wrap your original `BitmapTransformation` when loading image with Glide request.

Code Snippet as follow. Run sample project to see other Glide built-in transformation effect.

```
Transformation<Bitmap> circleCrop = new CircleCrop();
GlideApp.with(mContext)
        .load(url)
        .optionalTransform(circleCrop)
        .optionalTransform(WebpDrawable.class, new WebpDrawableTransformation(circleCrop))
        .into(imageView);
```

## Proguard

The library use native code to decode webp, so you should put the following lines to your `proguard.cfg` and keep the jni interface.

```pro
-keep public class com.bumptech.glide.integration.webp.WebpImage { *; }
-keep public class com.bumptech.glide.integration.webp.WebpFrame { *; }
-keep public class com.bumptech.glide.integration.webp.WebpBitmapFactory { *; }
```

## Acknowledgement

* [libwebp](https://github.com/webmproject/libwebp)
* [Fresco](https://github.com/facebook/fresco)
* [GlideWebpSupport](https://github.com/roths/GlideWebpSupport)

## License

The Library is [Apache-2.0-licensed](https://github.com/zjupure/GlideWebpDecoder/blob/master/LICENSE), part code is [MIT-licensed](https://github.com/facebook/fresco/blob/master/LICENSE) see [Fresco](https://github.com/facebook/fresco) for detail.

