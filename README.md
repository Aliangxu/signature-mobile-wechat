## signature-mobile-wechat

signature-mobile-wechat support H5 and wechat miniprogram

This is a rewrite of original signature-mobile-wechat, starting and borrowing from [this fork](https://github.com/szimek/signature_pad).

## Installation

```bash
# with npm
npm install signature-mobile-wechat -S
# with yarn
yarn add signature-mobile-wechat -S
```

## Usage

### 1-导入包
```typescript
import { SignatureMobile, SignatureMobileWechat } from 'signature-mobile-wechat';
```
### 2-在微信小程序中使用
```
// 1-创建初始化
wx.createSelectorQuery()
  .select(`#canvas`)
  .fields({
    node: true,
    size: true,
  })
  .exec((res: any[]) => {
    const canvas: WechatMiniprogram.Canvas = res[0].node;
    const signatureMobileWechat = new SignatureMobileWechat(canvas, {
      minWidth: 2,
      maxWidth: 5,
      penColor: 'rgb(0, 0, 0)',
    });
  });
// 2-手势注册注入
handleTouchStart: function (e) {
  // console.log(e)
  this.data.signatureMobileWechat && this.data.signatureMobileWechat.handleTouchStart(e)
},
handleTouchMove: function (e) {
  // console.log(e)
  this.data.signatureMobileWechat && this.data.signatureMobileWechat.handleTouchMove(e)
},
handleTouchEnd: function (e) {
  // console.log(e)
  this.data.signatureMobileWechat && this.data.signatureMobileWechat.handleTouchEnd(e)
},
```
### 2-正常网页使用
```
const canvas = document.querySelector('canvas');
const signatureMobile = new SignatureMobile(canvas, {
  minWidth: 2,
  maxWidth: 5,
  penColor: 'rgb(0, 0, 0)',
});
```

### Options
<dl>
<dt>dotSize</dt>
<dd>(float or function) Radius of a single dot.</dd>
<dt>minWidth</dt>
<dd>(float) Minimum width of a line. Defaults to <code>0.5</code>.</dd>
<dt>maxWidth</dt>
<dd>(float) Maximum width of a line. Defaults to <code>2.5</code>.</dd>
<dt>throttle</dt>
<dd>(integer) Draw the next point at most once per every <code>x</code> milliseconds. Set it to <code>0</code> to turn off throttling. Defaults to <code>16</code>.</dd>
<dt>minDistance</dt>
<dd>(integer) Add the next point only if the previous one is farther than <code>x</code> pixels. Defaults to <code>5</code>.
<dt>backgroundColor</dt>
<dd>(string) Color used to clear the background. Can be any color format accepted by <code>context.fillStyle</code>. Defaults to <code>"rgba(0,0,0,0)"</code> (transparent black). Use a non-transparent color e.g. <code>"rgb(255,255,255)"</code> (opaque white) if you'd like to save signatures as JPEG images.</dd>
<dt>penColor</dt>
<dd>(string) Color used to draw the lines. Can be any color format accepted by <code>context.fillStyle</code>. Defaults to <code>"black"</code>.</dd>
<dt>velocityFilterWeight</dt>
<dd>(float) Weight used to modify new velocity based on the previous velocity. Defaults to <code>0.7</code>.</dd>
<dt>onBegin</dt>
<dd>(function) Callback when stroke begin.</dd>
<dt>onEnd</dt>
<dd>(function) Callback when stroke end.</dd>
</dl>

You can set options during initialization:
```javascript
var signatureMobile = new SignatureMobile(canvas, {
    minWidth: 5,
    maxWidth: 10,
    penColor: "rgb(66, 133, 244)"
});
```
or during runtime:
```javascript
var signatureMobile = new SignatureMobile(canvas);
signatureMobile.minWidth = 5;
signatureMobile.maxWidth = 10;
signatureMobile.penColor = "rgb(66, 133, 244)";
```