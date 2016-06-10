# About
***
在写相机应用时需要用到图片裁剪框，但是又没有找到一个合适的第三方，没办法只能自己写了。写完后封装了一下，就有了这个**CYImageCrop**。

虽然叫做 ImageCrop，但实际上并没有裁剪的功能，而是提供了一个裁剪框的视图，以及获取到裁剪区域的 frame 的接口，还有每次裁剪后可以提供一个回调。具体的裁剪工作，还是要自己去实现的，当然，这并不困难~

# Preview
***
还是先看看预览图，后面再讲怎么用吧🤔
![](http://7xrad5.com1.z0.glb.clouddn.com/CYImageCropPreview.gif)

# Installation
***

## Manually
下载这个仓库，把仓库中的 `CYImageCrop` 文件夹拖入工程中

## Cocoapods
创建 `Podfile` 文件，添加 `pod 'CYImageCrop'`
在终端输入 `pod install` 或者 `pod update`

# Usage
```
#import "UIImageView+CYCrop.h"
```
在需要显示裁剪框时

```
[self.imageView cy_showCropViewWithType:CYCropScaleTypeCustom];
```
目前提供了一下集中裁剪框的类型：

```
typedef NS_ENUM(NSInteger, CYCropScaleType) {
    CYCropScaleTypeCustom,		// 自定义
    CYCropScaleTypeOriginal,	// 原始比例
    CYCropScaleType1To1,
    CYCropScaleType3To2,
    CYCropScaleType2To3,
    CYCropScaleType4To3,
    CYCropScaleType3To4,
    CYCropScaleType16To9,
    CYCropScaleType9To16,
};
```

当你不需要裁剪框时，你可以直接隐藏它：

```
[self.imageView cy_hideCropView];
```

我还提供了其他的一些接口来更精细的控制裁剪框视图

```
/** 裁剪视图,通过这个属性你可以设置更多裁剪框的细节 */
@property (nonatomic, strong, readonly)CYCropView *cy_cropView;

// 下面这两个属性是提供给具体裁剪时使用的
/** 返回实际裁剪区域的 frame  */
@property (nonatomic, assign, readonly)CGRect cy_cropFrame;
/** 返回实际裁剪区域占据整个视图的位置比例（0，0，0，0）是左上角 （1，1，1，1）是右下角*/
@property (nonatomic, assign, readonly)CGRect cy_cropFrameRatio;

/** 设置缩放类型 */
- (void)cy_setScaleType:(CYCropScaleType)scaleType;

/** 设置每次拖拽裁剪框后的回调 */
- (void)cy_setComplectionHandler:(void (^)())complectionHandler;
```


`UIImageView` 的 `cy_cropView` 属性是一个 `CYCropView` 类型的视图，通过它，你可以更进一步的定制裁剪框，目前有这额外的几个属性可以设置: 

```
/** 裁剪框边框粗细 */
@property (nonatomic, assign)CGFloat borderWidth;
/** 遮罩层颜色 */
@property (nonatomic, strong)UIColor *maskColor;
/** 裁剪框最小边长 */
@property (nonatomic, assign)CGFloat minLenghOfSide;
```
你也可以自己实例化一个 CYCropView，并把它添加到你自己的视图上而不仅仅是 UIImageView，当然，你需要自己管理这个 cropView 的生命周期。

```
CYCropView *cropView = [[CYCropView alloc] initWithFrame:customView.bounds]];
[customView addSubview: cropView];
```

**如果需要更直观的感受，可以看此仓库下的 Demo 🤔**

# 联系我
***

微博 [@Cyrus_dev](http://weibo.com/u/5822241060)

