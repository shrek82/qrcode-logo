# qrcode-logo
基于node-gd图形处理库，用于生成带logo的二维码图片。

#效果

![qrcode image](https://raw.githubusercontent.com/fisherw/resource-cache/master/img/test_qr.png "基础二维码")

![qrcode logo image](https://raw.githubusercontent.com/fisherw/resource-cache/master/img/testqr_logo.png "带logo二维码")

![qrcode logo image](https://raw.githubusercontent.com/fisherw/resource-cache/master/img/testqr_logo1.png "带logo二维码1")

# 示例

##生成带logo的二维码
```javascript
var fs = require('fs'),
    qrCodeLogo = require('../index'),

    url = 'https://www.baidu.com/',
    qrcodeImgFilePath = '/Users/test/myworkspace/qr_logo.png',
    logoBuffer = fs.readFileSync('/Users/test/myworkspace/logo.png', {
        encoding: null
    });

qrCodeLogo(url, qrcodeImgFilePath, {
    size: 10,  // 二维码大小
    logo: logoBuffer // logo数据
});
```


##仅生成二维码图片
```javascript
var fs = require('fs'),
    qrCodeLogo = require('../index'),

    url = 'https://www.baidu.com/',
    qrcodeImgFilePath = '/Users/test/myworkspace/qr.png';

qrCodeLogo(url, qrcodeImgFilePath, function (err, img) {
    console.log(err, img); // img为生成二维码图片信息（包含高度、宽度等信息）
});
```

##生成带logo（带圆角边框）且带底部文本的二维码图片
```javascript
var fs = require('fs'),
    qrCodeLogo = require('../index'),

    url = 'https://www.baidu.com/',
    qrcodeImgFilePath = '/Users/test/myworkspace/qr_logo.png',
    logoBuffer = fs.readFileSync('/Users/test/myworkspace/logo.png', {
        encoding: null
    });

qrCodeLogo(url, qrcodeImgFilePath, {
    size: 10,  // 二维码大小
    margin: 2,
    logo: logoBuffer, // logo数据
    logoBorder: {   // border边框配置
        width: 4,
        color: 0xcccfff
    },
    bottomText: {  // 底部文本框配置
        text: 'A12',
        bgColor: 0xeeefff
    }
});
```

#API

##调用方式
qrcode(text, outpath, qrOpts, cb) 或 qrcode(text, outpath, cb)

##参数
###text（必填）
(String)生成二维码的文本、url。

###outpath（必填）
(String）生成的二维码图片的文件路径。

###cb（可选）
生成二维码图片文件回调方法: function (err, img) {
    // err 错误认息
    // img  生成的二维码图片信息（高度、宽度、色值等）
}

###qrOpts.size（可选）
(Number)二维码图片大小，默认值为10（pixel)

###qrOpts.parse_url（可选）
(Boolean)是否优化处理text为url的情况， 默认为true

###qrOpts.logo（可选）
(Buffer) logo图片的buffer数据(目前仅支持png、jpeg格式图片)。 logo图片会设置额外背景色为白色（若logo为透明背景，则背景色会改为白色）

###qrOpts.logoBorder.width（可选）
(Number)边框大小(pixel)。值为空时，不作边框渲染。
        
###qrOpts.logoBorder.radius（可选）
(Number)logo圆角大小, 默认值为10(pixel)。

###qrOpts.logoBorder.color（可选）
(Number)边框颜色，使用十六进制颜色值.默认值为0xffffff.

###qrOpts.bottomText.height（可选）
(Number)文本框高度。默认值45。

###qrOpts.bottomText.align（可选）
(String) 文本对齐方式。默认居中对齐。

###qrOpts.bottomText.size（可选）
(Number)文本字体大小。默认值25。
        
###qrOpts.bottomText.angle（可选）
(Number) 文本旋转角度，默认0（0~360）。

###qrOpts.bottomText.color（可选）
(Number) 文本颜色，使用十六进制颜色值。默认值0x000000。

###qrOpts.bottomText.bgColor（可选）
(Number) 文本框背景颜色，使用十六进制颜色值。默认值0xffffff。

###qrOpts.bottomText.fontFilePath（可选）
(String) 文本字体文件路径。仅支持ttf字体文件。默认为楷体（gb-2312).




