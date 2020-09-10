# image_pixels

Lets you build a widget that depends on the _width_ and _height_ of some image, 
and the _color of its pixels_.

## Extend the image background-color  
 
The `ImagePixels.container` constructor adds a background-color
that is the same color as the image pixel at the `colorAlignment` position.

For example, if you put the image inside of a `Container` you get this:

```dart   
Container(
    width: 250,
    height: 100,                           
    alignment: Alignment.center,
    child: 
        Container(    
            width: 40.0, 
            height: 60.0, 
            child: Image(image: myImageProvider),
        ),
);
```
 
![](https://github.com/marcglasberg/image_pixels/blob/master/example/lib/images/with_container.jpg)

<br>

Now, if you wrap it with an `ImagePixels.container`:

```dart
ImagePixels.container(
    imageProvider: myImageProvider,    
    colorAlignment: Alignment.topLeft,
    child: 
        Container(
            width: 250,
            height: 100,                           
            alignment: Alignment.center,
            child: 
                Container(    
                    width: 40.0, 
                    height: 60.0, 
                    child: Image(image: myImageProvider),
                ),
        );
);
```

![](https://github.com/marcglasberg/image_pixels/blob/master/example/lib/images/with_image_pixels.jpg)

<br>

## Using a builder

The `ImagePixels` constructor lets you define an image through an `imageProvider`,
and then use a `builder` to build a child widget that depends on the image dimension
and the color of its pixels.

The default constructor lets you provide the `imageProvider`, the `builder`, and a
`defaultColor` to be used when reading pixels outside of the image 
(or while the image is downloading).

For example, this will print the size of the image:

```dart
ImagePixels(
    imageProvider: imageProvider,
    defaultColor: Colors.grey,
    builder: ({
          bool hasImage,
          int width,
          int height,
          ui.Image image,
          ByteData byteData,
          Color Function(int x, int y) pixelColorAt,
          Color Function(Alignment alignment) pixelColorAtAlignment,
        }) =>
            Text("The image size is: $width x $height"),
      );
```

<br>

### Builder parameters

The `builder` parameter is of type `BuilderFromImage`, with the following parameters: 

* If the image is already available, `hasImage` is true, 
and `width` and `height` indicate the image dimensions.

* While the image is **not** yet available, 
`hasImage` is false, and `width` and `height` are `null`.

* The `defaultColor` will be used when reading pixels outside of the image, 
or while the image is downloading.

* The functions `pixelColorAt` and `pixelColorAtAlignment` 
can be used by the `builder` to read the color of the image pixels. 

* If the coordinates point to outside of the image, 
or if the image is not yet available, then these functions will return the
default-color provided in the `ImagePixels` constructor.

* The `image` parameter contains the image as a `ui.Image` type. 
It will be `null` while the image is still downloading.

* The `byteData` parameter contains the image already converted into a `ByteDate` type. 
It will be `null` while the image is still downloading.

<br>

## Other use cases

* **Getting the tapped pixel color** — 
By wrapping the child of the `ImagePixel` with a `GestureDetector` you get the tapped position, 
and then it's easy to get the color of the tapped image pixel.

* **Modifying the image** — 
The child of the `ImagePixel` can be a `CustomPainter`, 
and then you can use a **canvas** to paint whatever you want
on top of the image, or else create an entirely new image from the original image pixels.

<br>

***

*The Flutter packages I've authored:*
* <a href="https://pub.dev/packages/async_redux">async_redux</a>
* <a href="https://pub.dev/packages/provider_for_redux">provider_for_redux</a>
* <a href="https://pub.dev/packages/i18n_extension">i18n_extension</a>
* <a href="https://pub.dev/packages/align_positioned">align_positioned</a>
* <a href="https://pub.dev/packages/network_to_file_image">network_to_file_image</a>
* <a href="https://pub.dev/packages/image_pixels">image_pixels</a>
* <a href="https://pub.dev/packages/matrix4_transform">matrix4_transform</a>
* <a href="https://pub.dev/packages/back_button_interceptor">back_button_interceptor</a>
* <a href="https://pub.dev/packages/indexed_list_view">indexed_list_view</a>
* <a href="https://pub.dev/packages/animated_size_and_fade">animated_size_and_fade</a>
* <a href="https://pub.dev/packages/assorted_layout_widgets">assorted_layout_widgets</a>
* <a href="https://pub.dev/packages/weak_map">weak_map</a>

*My Medium Articles:*
* <a href="https://medium.com/flutter-community/https-medium-com-marcglasberg-async-redux-33ac5e27d5f6">Async Redux: Flutter’s non-boilerplate version of Redux</a> (versions: <a href="https://medium.com/flutterando/async-redux-pt-brasil-e783ceb13c43">Português</a>)
* <a href="https://medium.com/flutter-community/i18n-extension-flutter-b966f4c65df9">i18n_extension</a> (versions: <a href="https://medium.com/flutterando/qual-a-forma-f%C3%A1cil-de-traduzir-seu-app-flutter-para-outros-idiomas-ab5178cf0336">Português</a>)
* <a href="https://medium.com/flutter-community/flutter-the-advanced-layout-rule-even-beginners-must-know-edc9516d1a2">Flutter: The Advanced Layout Rule Even Beginners Must Know</a> (versions: <a href="https://habr.com/ru/post/500210/">русский</a>)

*My article in the official Flutter documentation*:
* <a href="https://flutter.dev/docs/development/ui/layout/constraints">Understanding constraints</a>

<br>_Marcelo Glasberg:_<br>
_https://github.com/marcglasberg_<br>
_https://twitter.com/glasbergmarcelo_<br>
_https://stackoverflow.com/users/3411681/marcg_<br>
_https://medium.com/@marcglasberg_<br>

