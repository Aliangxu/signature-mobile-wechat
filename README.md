## signature-mobile-wechat

signature-mobile-wechat support wechat miniprogram

This is a rewrite of original signature-mobile-wechat, starting and borrowing from [this fork](https://github.com/szimek/signature_pad).

## Installation

```bash
# with npm
npm install signature-mobile-wechat -S
# with yarn
yarn add signature-mobile-wechat -S
```

## Usage

```typescript
import { SignatureMobile, SignatureMobileWechat } from 'signature-mobile-wechat';

// 在微信小程序中使用
wx.createSelectorQuery()
  .select(`#canvas`)
  .fields({
    node: true,
    size: true,
  })
  .exec((res: any[]) => {
    const { width, height } = res[0];

    const canvas: WechatMiniprogram.Canvas = res[0].node;

    const signaturePad = new SignatureMobileWechat(canvas, {
      minWidth: 2,
      maxWidth: 5,
      penColor: 'rgb(0, 0, 0)',
    });
  });

// 正常网页使用
const canvas = document.querySelector('canvas');

const signaturePad = new SignatureMobile(canvas, {
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
var signaturePad = new SignatureMobile(canvas, {
    minWidth: 5,
    maxWidth: 10,
    penColor: "rgb(66, 133, 244)"
});
```
or during runtime:
```javascript
var signaturePad = new SignatureMobile(canvas);
signaturePad.minWidth = 5;
signaturePad.maxWidth = 10;
signaturePad.penColor = "rgb(66, 133, 244)";
```