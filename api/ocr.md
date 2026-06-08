# OCR

The `ocr` module is used for recognizing text in images.

AutoJs6's OCR feature is implemented based on [Google ML Kit](https://developers.google.com/ml-kit?hl=en) 's [Text Recognition API](https://developers.google.com/ml-kit/vision/text-recognition/android?hl=en) and [Baidu PaddlePaddle](https://www.paddlepaddle.org.cn/)'s [Paddle Lite](https://github.com/PaddlePaddle/Paddle-Lite).

---

<p style="font: bold 2em sans-serif; color: #FF7043">ocr</p>

---

## [@] ocr

`ocr` can be used as a global object:

```js
typeof ocr; // "function"
typeof ocr.detect; // "function"
typeof ocr.recognizeText; // "function"
```

### ocr(options?)

**`6.4.0`** **`Overload [1-2]/9`**

- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR recognition options
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Recognizes all text contained in the current screen screenshot and returns an array of text strings.

`ocr()` is equivalent to the following combined code:

```js
images.requestScreenCapture();
let img = images.captureScreen();
ocr(img);
```

It is also an alias for [ocr.recognizeText(options?)](#m-recognizetext).

### ocr(region)

**`6.4.0`** **`Overload 3/9`**

- **region** { [OmniRegion](omniTypes#omniregion) } - OCR recognition region
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Recognizes all text contained in the specified region of the current screen screenshot and returns an array of text strings.

`ocr(region)` is equivalent to the following combined code:

```js
images.requestScreenCapture();
let img = images.captureScreen();
ocr(img, region);
```

It is also a convenience method for [ocr({ region: region })](#-ocr),

and an alias for [ocr.recognizeText(region)](#m-recognizetext).

For more usage of the OCR region parameter `region`, see the [OcrOptions#region](ocrOptionsType#p-region) section.

### ocr(img, options?)

**`6.3.0`** **`Overload [4-5]/9`**

- **img** { [ImageWrapper](imageWrapperType) } - Wrapped image object
- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR recognition options
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Recognizes all text contained in the image and returns an array of text strings.

Alias for [ocr.recognizeText(img, options?)](#m-recognizetext).

```js
/* Request screen capture permission. */
images.requestScreenCapture();

/* Capture the screen and obtain the wrapped image object. */
let img = images.captureScreen();

/* Perform OCR recognition and get the result as a string array. */
let results = ocr(img);

/* Filter results: select texts that partially match "app", such as "apple", "disappear", etc. */
results.filter(text => text.includes('app'));
```

### ocr(img, region)

**`6.3.0`** **`Overload 6/9`**

- **img** { [ImageWrapper](imageWrapperType) } - Wrapped image object
- **region** { [OmniRegion](omniTypes#omniregion) } - OCR recognition region
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Recognizes all text contained in the specified region of the image and returns an array of text strings.

Convenience method for [ocr(img, { region: region })](#-ocr).

Alias for [ocr.recognizeText(img, region)](#m-recognizetext).

```js
/* Request screen capture permission. */
images.requestScreenCapture();

/* Capture the screen and obtain the wrapped image object. */
let img = images.captureScreen();

/* Perform OCR recognition within the region [0, 0, 100, 150] and get the result as a string array. */
let results = ocr(img, [0, 0, 100, 150]);

/* Filter results: select texts that partially match "app", such as "apple", "disappear", etc. */
results.filter(text => text.includes('app'));
```

For more usage of the OCR region parameter `region`, see the [OcrOptions#region](ocrOptionsType#p-region) section.

### ocr(imgPath, options?)

**`6.3.0`** **`Overload [7-8]/9`**

- **imgPath** { [string](dataTypes#string) } - Image path
- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR recognition options
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Recognizes all text contained in the image at the specified path and returns an array of text strings.

If the specified path cannot be resolved to a wrapped image object, a `TypeError` exception will be thrown.

Alias for [ocr.recognizeText(imgPath, options?)](#m-recognizetext).

```js
ocr('./picture.jpg'); /* Get all text from the local image file. */
```

### ocr(imgPath, region)

**`6.3.0`** **`Overload 9/9`**

- **imgPath** { [string](dataTypes#string) } - Image path
- **region** { [OmniRegion](omniTypes#omniregion) } - OCR recognition region
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

Recognizes all text contained in the specified region of the image at the given path and returns an array of text strings.

If the specified path cannot be resolved to a wrapped image object, a `TypeError` exception will be thrown.

Convenience method for [ocr(imgPath, { region: region })](#-ocr).

Alias for [ocr.recognizeText(imgPath, region)](#m-recognizetext).

```js
/* Get all text from the local image file within the region [0, 0, 100, 150]. */
ocr('./picture.jpg', [0, 0, 100, 150]);
```

For more usage of the OCR region parameter `region`, see the [OcrOptions#region](ocrOptionsType#p-region) section.

## [p] mode

**`6.3.4`** **`Getter/Setter`**

- **[ &lt;get&gt; = `'mlkit'` ]** { [OcrModeName](dataTypes#ocrModeName) }
- **&lt;set&gt;** { [OcrModeName](dataTypes#ocrModeName) }

获取或设置 OCR 的工作模式名称.

```js
/* AutoJs6 OCR 默认采用 MLKit 工作模式. */
console.log(ocr.mode); // "mlkit"

ocr.mode = 'paddle'; /* 切换到 Paddle 工作模式. */
console.log(ocr.mode); // "paddle"

ocr.mode = 'mlkit'; /* 再次切换到 MLKit 工作模式. */
console.log(ocr.mode); // "mlkit"
```

当使用不同的工作模式名称时, `ocr` 全局方法及其相关方法 (如 [ocr.detect](#m-detect)) 将使用不同的引擎, 进而可能获得不同的识别速度和结果.

> 注: 使用 Paddle 工作模式时, 建议开启 AutoJs6 的 "忽略电池优化" 开关, 并降低对 AutoJs6 节电及后台运行等方面的限制, 否则可能导致应用崩溃.

## [m] recognizeText

用于识别图像中的全部文本.

`recognizeText` 方法与工作模式有关, 例如当工作模式为 `paddle` 时, `ocr.recognizeText(...)` 与 `ocr.paddle.recognizeText(...)` 等价.

`ocr.recognizeText(...)` 相关方法均可简写为 `ocr(...)`.

### recognizeText(options?)

**`6.4.0`** **`Overload [1-2]/9`**

- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR 识别选项
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

识别当前屏幕截图中包含的所有文本, 返回文本数组.

`ocr.recognizeText()` 相当于以下代码的整合:

```js
images.requestScreenCapture();
let img = images.captureScreen();
ocr.recognizeText(img);
```

`ocr.recognizeText(options?)` 与 `ocr(options?)` 等价.

### recognizeText(region)

**`6.4.0`** **`Overload 3/9`**

- **region** { [OmniRegion](omniTypes#omniregion) } - OCR 识别区域
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

识别当前屏幕截图指定区域内包含的所有文本, 返回文本数组.

`ocr.recognizeText(region)` 相当于以下代码的整合:

```js
images.requestScreenCapture();
let img = images.captureScreen();
ocr.recognizeText(img, region);
```

[ocr.recognizeText({ region: region })](#m-recognizeText) 的便捷方法.

`ocr.recognizeText(region)` 与 `ocr(region)` 等价.

关于 OCR 区域参数 `region` 的更多用法, 参阅 [OcrOptions#region](ocrOptionsType#p-region) 小节.

### recognizeText(img, options?)

**`6.3.0`** **`Overload [4-5]/9`**

- **img** { [ImageWrapper](imageWrapperType) } - 包装图像对象
- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR 识别选项
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

识别图像包含的所有文本, 返回文本数组.

`ocr.recognizeText(img, options?)` 与 `ocr(img, options?)` 等价.

```js
images.requestScreenCapture(); /* 申请屏幕截图权限. */
let img = images.captureScreen(); /* 截屏并获取包装图像对象. */
ocr.recognizeText(img).filter(text => text.includes('app')); /* 过滤结果. */
```

### recognizeText(img, region)

**`6.3.0`** **`Overload 6/9`**

- **img** { [ImageWrapper](imageWrapperType) } - 包装图像对象
- **region** { [OmniRegion](omniTypes#omniregion) } - OCR 识别区域
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

识别指定区域内图像包含的所有文本, 返回文本数组.

[ocr.recognizeText(img, { region: region })](#m-recognizeText) 的便捷方法.

`ocr.recognizeText(img, region)` 与 `ocr(img, region)` 等价.

```js
images.requestScreenCapture(); /* 申请屏幕截图权限. */
let img = images.captureScreen(); /* 截屏并获取包装图像对象. */
ocr.recognizeText(img, [ 0, 0, 100, 150 ]).filter(text => text.includes('app')); /* 过滤结果. */
```

关于 OCR 区域参数 `region` 的更多用法, 参阅 [OcrOptions#region](ocrOptionsType#p-region) 小节.

### recognizeText(imgPath, options?)

**`6.3.0`** **`Overload [7-8]/9`**

- **imgPath** { [string](dataTypes#string) } - 图像路径
- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR 识别选项
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

识别指定路径对应图像包含的所有文本, 返回文本数组.

当指定路径无法解析为包装图像对象时, 将抛出 `TypeError` 异常.

`ocr.recognizeText(imgPath, options?)` 与 `ocr(imgPath, options?)` 等价.

```js
ocr.recognizeText('./picture.jpg'); /* 获取本地图像文件中的所有文本. */
```

### recognizeText(imgPath, region)

**`6.3.0`** **`Overload 9/9`**

- **imgPath** { [string](dataTypes#string) } - 图像路径
- **region** { [OmniRegion](omniTypes#omniregion) } - OCR 识别区域
- <ins>**returns**</ins> { [string](dataTypes#string)[[]](dataTypes#array) }

识别指定路径对应图像在指定区域内包含的所有文本, 返回文本数组.

当指定路径无法解析为包装图像对象时, 将抛出 `TypeError` 异常.

[ocr.recognizeText(imgPath, { region: region })](#m-recognizetext) 的便捷方法.

`ocr.recognizeText(imgPath, region)` 与 `ocr(imgPath, region)` 等价.

```js
/* 获取本地图像文件在区域 [ 0, 0, 100, 150 ] 内的所有文本. */
ocr.recognizeText('./picture.jpg', [ 0, 0, 100, 150 ]);
```

关于 OCR 区域参数 `region` 的更多用法, 参阅 [OcrOptions#region](ocrOptionsType#p-region) 小节.

## [m] detect

用于识别图像中的全部文本.

`detect` 方法与工作模式有关, 例如当工作模式为 `paddle` 时, `ocr.detect(...)` 与 `ocr.paddle.detect(...)` 等价.

与 [recognizeText](#m-recognizetext) 不同, `detect` 返回的结果包含更多信息, 包括 [ 文本标签, 置信度, 位置矩形 ] 等, `recognizeText` 精简了 `detect` 返回的结果, 仅包含文本标签数据.

### detect(options?)

**`6.4.0`** **`Overload [1-2]/9`**

- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR 识别选项
- <ins>**returns**</ins> { [OcrResult](dataTypes#ocrresult)[[]](dataTypes#array) }

识别当前屏幕截图中包含的所有文本, 返回 [OcrResult](dataTypes#ocrresult) 数组.

`ocr.detect()` 相当于以下代码的整合:

```js
images.requestScreenCapture();
let img = images.captureScreen();
ocr.detect(img);
```

### detect(region)

**`6.4.0`** **`Overload 3/9`**

- **region** { [OmniRegion](omniTypes#omniregion) } - OCR 识别区域
- <ins>**returns**</ins> { [OcrResult](dataTypes#ocrresult)[[]](dataTypes#array) }

识别当前屏幕截图指定区域内包含的所有文本, 返回 [OcrResult](dataTypes#ocrresult) 数组.

`ocr.detect(region)` 相当于以下代码的整合:

```js
images.requestScreenCapture();
let img = images.captureScreen();
ocr.detect(img, region);
```

同时也是 [ocr.detect({ region: region })](#m-detect) 的便捷方法.

关于 OCR 区域参数 `region` 的更多用法, 参阅 [OcrOptions#region](ocrOptionsType#p-region) 小节.

### detect(img, options?)

**`6.3.0`** **`Overload [4-5]/9`**

- **img** { [ImageWrapper](imageWrapperType) } - 包装图像对象
- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR 识别选项
- <ins>**returns**</ins> { [OcrResult](dataTypes#ocrresult)[[]](dataTypes#array) }

识别图像包含的所有文本, 返回 [OcrResult](dataTypes#ocrresult) 数组.

```js
/* 申请屏幕截图权限. */
images.requestScreenCapture();

/* 截屏并获取包装图像对象. */
let img = images.captureScreen();

/* 获取本地图像文件中的所有识别结果. */
let result = ocr.detect(img);

/* 筛选置信度高于 0.8 的结果. */
result.filter(o => o.confidence >= 0.8);
```

### detect(img, region)

**`6.3.0`** **`Overload 6/9`**

- **img** { [ImageWrapper](imageWrapperType) } - 包装图像对象
- **region** { [OmniRegion](omniTypes#omniregion) } - OCR 识别区域
- <ins>**returns**</ins> { [OcrResult](dataTypes#ocrresult)[[]](dataTypes#array) }

识别指定路径对应图像在指定区域内包含的所有文本, 返回 [OcrResult](dataTypes#ocrresult) 数组.

[ocr.detect(img, { region: region })](#m-detect) 的便捷方法.

```js
/* 申请屏幕截图权限. */
images.requestScreenCapture();

/* 截屏并获取包装图像对象. */
let img = images.captureScreen();

/* 获取本地图像文件在区域 [ 0, 0, 100, 150 ] 内的所有识别结果. */
let result = ocr.detect(img, [ 0, 0, 100, 150 ]);

/* 筛选置信度高于 0.8 的结果. */
result.filter(o => o.confidence >= 0.8);
```

关于 OCR 区域参数 `region` 的更多用法, 参阅 [OcrOptions#region](ocrOptionsType#p-region) 小节.

### detect(imgPath, options?)

**`6.3.0`** **`Overload [7-8]/9`**

- **imgPath** { [string](dataTypes#string) } - 图像路径
- **[ options ]** { [OcrOptions](ocrOptionsType) } - OCR 识别选项
- <ins>**returns**</ins> { [OcrResult](dataTypes#ocrresult)[[]](dataTypes#array) }

识别指定路径对应图像包含的所有文本, 返回 [OcrResult](dataTypes#ocrresult) 数组.

当指定路径无法解析为包装图像对象时, 将抛出 `TypeError` 异常.

```js
let result = ocr.detect('./picture.jpg'); /* 获取本地图像文件中的所有识别结果. */
result.filter(o => o.confidence >= 0.8); /* 筛选置信度高于 0.8 的结果. */
```

### detect(imgPath, region)

**`6.3.0`** **`Overload 9/9`**

- **imgPath** { [string](dataTypes#string) } - 图像路径
- **region** { [OmniRegion](omniTypes#omniregion) } - OCR 识别区域
- <ins>**returns**</ins> { [OcrResult](dataTypes#ocrresult)[[]](dataTypes#array) }

识别指定路径对应图像在指定区域内包含的所有文本, 返回 [OcrResult](dataTypes#ocrresult) 数组.

当指定路径无法解析为包装图像对象时, 将抛出 `TypeError` 异常.

[ocr.detect(imgPath, { region: region })](#m-detect) 的便捷方法.

```js
/* 获取本地图像文件在区域 [ 0, 0, 100, 150 ] 内的所有识别结果. */
let result = ocr.detect('./picture.jpg', [ 0, 0, 100, 150 ]);

/* 筛选置信度高于 0.8 的结果. */
result.filter(o => o.confidence >= 0.8);
```

关于 OCR 区域参数 `region` 的更多用法, 参阅 [OcrOptions#region](ocrOptionsType#p-region) 小节.

## [m] tap

### tap(mode)

**`6.3.4`**

- **mode** { [OcrModeName](dataTypes#ocrModeName) } - OCR 工作模式
- <ins>**returns**</ins> { [void](dataTypes#void) }

用于切换 OCR 工作模式, 相当于 [ocr.mode](#p-mode) 的 setter 形式.

```js
ocr.tap('paddle');
ocr.mode = 'paddle'; /* 同上. */
```

## [m] summary

### summary()

**`6.4.0`**

获取 AutoJs6 OCR 功能的摘要.

摘要中表述了 OCR 功能当前使用的工作模式, 以及全部可用的工作模式.

```js
/* e.g. [ OCR summary ]
 * Current mode: mlkit
 * Available modes: [ mlkit, paddle ]
 */
console.log(ocr.summary());
```

## 工作模式与代码形式

截止 2023 年 9 月, AutoJs6 的 ocr 支持两种工作模式, `mlkit` (默认) 及 `paddle`.

工作模式的获取或设置可通过 [ocr.mode](#p-mode) 实现.

下面以 `mlkit` 为例, 总结 `mlkit` 工作模式可用的全部代码形式.

1. ocr.mlkit.detect(...)
2. ocr.mlkit.recognizeText(...)
3. ocr.mlkit(...)
4. [ocr.detect(...)](#m-detect)
5. [ocr.recognizeText(...)](#m-recognizetext)
6. [ocr(...)](#-ocr)

上述 6 种代码形式均可实现使用 `mlkit` 引擎进行光学字符识别.

其中, [ 3 ] 是 [ 2 ] 的简便写法, [ 6 ] 是 [ 5 ] 的简便写法.

另外, [ 4, 5, 6 ] 三种形式的条件, 是 OCR 工作模式为 `mlkit`, 即 `ocr.mode` 返回 `mlkit`. 否则需要调用 `ocr.mode = 'mlkit'` 切换工作模式.

下面再以 `paddle` 为例, 总结 `paddle` 工作模式可用的全部代码形式.

1. ocr.paddle.detect(...)
2. ocr.paddle.recognizeText(...)
3. ocr.paddle(...)
4. [ocr.detect(...)](#m-detect)
5. [ocr.recognizeText(...)](#m-recognizetext)
6. [ocr(...)](#-ocr)

同样, [ 4, 5, 6 ] 三种形式的条件, 是 OCR 工作模式为 `paddle`, 即 `ocr.mode` 返回 `paddle`. 否则需要调用 `ocr.mode = 'paddle'` 切换工作模式.

由此可见, `ocr(...)` 和 `ocr.detect(...)` 等方法是动态变化的, 其功能取决于工作模式. 这种形式的优点是写法简单, 但可读性相对较差, 可能难以辨识 OCR 的具体工作引擎. 如需兼顾可读性, 则可使用 `ocr.mlkit(...)` 和 `ocr.mlkit.detect(...)` 等形式.