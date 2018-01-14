#  THTiledImageView

[![Version](https://img.shields.io/badge/pod-v0.2.0-blue.svg)
[![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg?style=flat)](https://github.com/younatics/YNDropDownMenu/blob/master/LICENSE)
[![Build Status](https://img.shields.io/badge/build-passing-brightgreen.svg)
[![Platform](https://img.shields.io/badge/platform-ios-lightgrey.svg)
[![Swift 4.0](https://img.shields.io/badge/Swift-4.0-%23FB613C.svg)](https://developer.apple.com/swift/)

## Feature


## Installation

```
pod "THTiledImageView"
```

## How to use

### SubClassing

1. `THTiledImageScrollView` is subclass of UIScrollVIew. Create `THTiledImageScrollView` from Storyboard or programmatically.

2. Create dataSource class that is subclass of `THTiledImageViewDataSource` like this.

```
var dataSource: THTiledImageViewDataSource?
```

3. You can set `THTiledImageViewDataSource` options like this.

```
func setupExample(imageSize: CGSize, tileSize: [CGSize], imageURL: URL) {

    dataSource = MyTileImageViewDataSource(imageSize: imageSize, tileSize: tileSize, imageURL: imageURL)
    dataSource?.thumbnailImageName = "bench"

    // 줌을 가장 많이 확대한 수준
    dataSource?.maxTileLevel = 5

    // 줌이 가장 확대가 안 된 수준
    dataSource?.minTileLevel = 1

    dataSource?.maxZoomLevel = 8

    dataSource?.imageExtension = "jpg"
    tileImageScrollView.set(dataSource: dataSource!)

    dataSource?.requestBackgroundImage { _ in
        // do something after image shows.
    }
}
```

### Cutting Image

❗️ So far cutting and rendering images cannot be done simultaneously. You should cut image first, and relaunch the app.

We offer you image cutting function(`UIImage.saveTileOf(size:name:withExtension:)`.



```
let tiles: [CGSize] = [CGSize(width: 2048, height: 2048), CGSize(width: 1024, height: 1024),
CGSize(width: 512, height: 512), CGSize(width: 256, height: 256),
CGSize(width: 128, height: 128)]

UIImage.saveTileOf(size: tiles, name: "bench", withExtension: "jpg")
```

Tiled images will be saved on your cache directory. Path of the cache directory:

```
let cachesPath = NSSearchPathForDirectoriesInDomains(.cachesDirectory, .userDomainMask, true)[0] as String
```

#### Tiled Images path

If imagefile saved successfully, you can see images from cache directory. Here is the rule of directory path and image file name rules.
```
Path Rules ./imageName/imageSize/{imageName_imageSize_level_x_y}.jpg
Example    ./bench/256/bench_256_1_0_0.jpg
```
