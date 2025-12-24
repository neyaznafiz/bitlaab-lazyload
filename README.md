
# Lazyload

A lightweight JavaScript utility built on top of the **IntersectionObserver API** to lazily:

- 🖼️ Load images
- 🎥 Load videos
- ⚙️ Execute functions

Only when the target element enters the viewport.

Lazyload defers loading of **images** and **videos**, and delays **execution of functions** on long web pages until they enter the viewport. Resources outside the visible area are not loaded or executed until the user scrolls to them, **improving performance and reducing unnecessary network usage**. This behavior is the opposite of preloading.

This is a modern, dependency-free vanilla JavaScript utility built on top of the **Intersection Observer API**. It observes when target elements enter the browser’s viewport and then dynamically loads images, loads videos, or executes functions exactly once.  Modern browser APIs and best practices are followed to ensure efficiency, simplicity, and flexibility.

---

## Features

- Lazy load images and videos
- Execute functions on viewport entry
- Configurable viewport, margins, and thresholds
- Zero dependencies

---

## 📦 Installation

```bash
npm install @ashcroft/lazyload@latest
```
Or
```bash
yarn add @ashcroft/lazyload@latest
```
```js
import Lazyload from "@ashcroft/lazyload";
// or
const Lazyload = require("@ashcroft/lazyload");
```

Or import directly using **CDN**
```js
import { Lazyload } from "https://unpkg.com/@ashcroft/lazyload/lazyload.js";
```


---

## Global Options
**Most of the time you don't need this, the package internally handle it. Only use when you want manual control.**

```js
options: {
    root: null,
    loadBefore: 0,
    loadAfter: 0
}
```

| Option | Type | Description |
|------|------|------------|
| root | string \| null | Viewport container selector |
| loadBefore | number | Margin before entering viewport |
| loadAfter | number | Visibility ratio (0–1) |


## Global Methods

| Method    | Description |
|-----------|------------------|
| image()   | Load images when element will enter into the viewport. |
| video()   | Load videos when element will enter into the viewport. |
| execute() | Execute function when element will enter into the viewport. |

---

## 🖼️ image()
It will load images when item will enter into the viewport. the method accept 5 parameters:
- **wrapper:** (Optional) - The wrapper of the `srcTarget`. The value of it is `CSS Selector`. </br>
**e.g.,** `wrapper: "#image-wrapper"` </br> **Note:** If you don't provide the `wrapper` it will select all of the elements with the selector of `srcTarget` from `DOM`, otherwise it will select only from the `wrapper`. You can handle it on your needs.

- **srcTarget:** (Required) - The selector of the elements where the image `src` will be set. The value of it is `CSS Selector`. </br>
**e.g.,** `srcTarget: ".lazy-img"`

- **attr:** (Optional) - An attribute where image url will be set. If you use this parameter, the image url will be set into this attribute of the `srcTarget` element, otherwise it will set `src` attribute with the image url into the `srcTarget` element by default. </br>
**e.g.,** `attr: "data-image"` </br>
**result** `<img data-image="/demo-1.jpg" />`

- **images:** (Optional) - An array of string(image url). </br>
**e.g.,** `images: [ "/demo-1.jpg", "/demo-2.jpg"]`

- **options:** (Optional) - The configuration of the lazyload. the value of it is an `object` with 3 properties and all are optional. </br>
**e.g.,** `options: {root: null, loadBefore: 0, loadAfter: 0}`

### You can load image in two ways:

#### First Example
Setting the `image url` into an attribute called `data-lazy-url`

```html
<div id="image-wrapper">
    <img class="lazy-img" data-lazy-url="/demo-1.jpg" />
    <img class="lazy-img" data-lazy-url="/demo-2.jpg" />
</div>
```

```js
const lazyload = new Lazyload();

lazyload.image({
    wrapper: "#image-wrapper",
    srcTarget: ".lazy-img",
    options: { // Most of the time you don't need to set this parameter,
    // the package internally handle it.
    // Only use when you want manual control.
        root: null,
        loadBefore: 0,
        loadAfter: 0
    }
});
```

#### Second Example
Passing `images: []`(Array of image urls) parameter into the `lazyload.image()` function.

```html
<div id="image-wrapper">
    <img class="lazy-img" />
    <img class="lazy-img" />
</div>
```

```js
const lazyload = new Lazyload();

lazyload.image({
    wrapper: "#image-wrapper",
    srcTarget: ".lazy-img",
    images: ["/demo-1.jpg", "/demo-2.jpg"],
    options: { // Most of the time you don't need to set this parameter,
    // the package internally handle it.
    // Only use when you want manual control.
        root: null,
        loadBefore: 0,
        loadAfter: 0
    }
});
```

---

## 🎥 video()
It will load videos when item will enter into the viewport. the method accept 5 parameters:
- **wrapper:** (Optional) - The wrapper of the `srcTarget`. The value of it is `CSS Selector`. </br>
**e.g.,** `wrapper: "#image-wrapper"` </br> **Note:** If you don't provide the `wrapper` it will select all of the elements with the selector of `srcTarget` from `DOM`, otherwise it will select only from the `wrapper`. You can handle it on your needs.

- **srcTarget:** (Required) - The selector of the elements where the video `src` will be set. The value of it is `CSS Selector`. </br>
**e.g.,** `srcTarget: ".lazy-img"`

- **attr:** (Optional) - The attribute where video url will be set. If you use this parameter, the video url will be set into this attribute of the `srcTarget` element, otherwise it will set `src` attribute with the video url into the `srcTarget` element by default. </br>
**e.g.,** `attr: "data-video"` </br>
**result** `<img data-video="/demo-1.mp4" />`

- **videos:** (Optional) - An array of string(video url). </br>
**e.g.,** `videos: ["/demo-1.mp4", "/demo-2.mp4"]`

- **options:** (Optional) - The configuration of the lazyload. the value of it is an `object` with 3 properties and all are optional. </br>
**e.g.,** `options: {root: null, loadBefore: 0, loadAfter: 0}`

### You can load videos in two ways:

#### First Example
Setting the `video url` into an attribute called `data-lazy-url`

```html
<div id="video-wrapper">
    <video class="lazy-video item" data-lazy-url="/demo-1.mp4"></video>
    <video class="lazy-video item" data-lazy-url="/demo-2.mp4"></video>
</div>
```

```js
const lazyload = new Lazyload();

lazyload.video({
    wrapper: "#video-wrapper",
    srcTarget: ".lazy-video",
    options: { // Most of the time you don't need to set this parameter,
    // the package internally handle it.
    // Only use when you want manual control.
        root: null,
        loadBefore: 0,
        loadAfter: 0
    }
});
```

#### Second Example
Passing `videos: []`(Array of video urls) parameter into the `lazyload.video()` function.

```html
<div id="video-wrapper">
    <video class="lazy-video item"></video>
    <video class="lazy-video item"></video>
</div>
```

```js
const lazyload = new Lazyload();

lazyload.video({
    wrapper: "#image-wrapper",
    srcTarget: ".lazy-video",
    videos: ["/demo-1.mp4", "/demo-2.mp4"],
    options: { // Most of the time you don't need to set this parameter,
    // the package internally handle it.
    // Only use when you want manual control.
        root: null,
        loadBefore: 0,
        loadAfter: 0
    }
});
```

---

## ⚙️ execute()
It will execute function when `viewportEntry` element will enter into the viewport. the method accept 3 parameters:

- **viewportEntry:** (Required) - The `viewportEntry` is the element where will be the function call, when the element enter into the viewport the function will be called. The value of it is `CSS Selector`. </br>
**e.g.,** `viewportEntry: "#stats"`

- **exeFn:** (Required) - The value of this parameter is a `function()` which will be execute. </br>
**e.g.,** `exeFn: () = {};`

- **options:** (Optional) - The configuration of the lazyload. the value of it is an `object` with 3 properties and all are optional. </br>
**e.g.,** `options: {root: null, loadBefore: 0, loadAfter: 0}`

### Example

```html
<div id="stats"></div>
```

```js
const lazyload = new Lazyload();

lazyload.execute({
    viewportEntry: "#stats",
    exeFn: () => console.log("Visible"),
    options: { // Most of the time you don't need to set this parameter,
    // the package internally handle it.
    // Only use when you want manual control.
        root: null,
        loadBefore: 0,
        loadAfter: 0
    }
});
```

---

## 📄 License

MIT
