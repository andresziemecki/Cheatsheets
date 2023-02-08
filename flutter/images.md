# Images in flutter

We can use image on the web or assets image (image in our directory).

## Network Image

Use of `Image` widget

``` dart
Image(image: NetworkImage('<url of the image>')),
```
## Assets Image

Good practice: Have the image in a new `assets` directory.

``` dart
Image(image: AssetImage('<local url of the image>')),
```

Uncomment in `pubspect.yaml` the `assets` keword and add ALL images url there.

Then a pop up button will appear to update dependencies of pubspect since it was changed.

There is a shortcut to do the same:

``` dart
Image.asset('<local url of the image>)
```

