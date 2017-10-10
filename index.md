
<h2 style="font-weight: bolder; font-family: 'Avenir Next'; font-size: 2.4em">Stencil</h2>
### the Rise of Web Components

[Mike Hartington | @mhartington](https://twitter.com/mhartington)

---

_or_

---

<!-- .slide: data-background="#ffffff" -->
<h2 style="font-weight: bolder; font-family: 'Avenir Next'">
How I learned to stop worrying and love the Web again
</h2>

---

### _Back in the Day…_

---

### Circa 2013

- Ionic was still just an idea
- Fast components were just difficult
- Frameworks at the time: 🗑 🔥

---

All we wanted

```html
  <ion-content>
    <ion-item>
      Hello World
    </ion-item>
  </ion-content>
```

---

### JavaScript at the time

- jQuery (not really a "framework")
- Backbone (MarionetteJS)
- AngularJS (still pretty new)

---

jQuery was nice, but not scalable

_enter AngularJS_

AngularJS Directives: 💙

_"jQuery Who?"_

---

### Fast Forward

---

- Angular (2,…,4, 5)
- (P)React
- Ember
- VueJs

**All excellent frameworks**

---

Component Authoring is still a pain

A new framework, a new API, a new problem

---

### Plus this new thing, PWAs

`framework.footPrint.importance++`

Every byte matters

---

## Enter Web Components

<img src="https://raw.githubusercontent.com/webcomponents/webcomponents-icons/master/logo/logo_256x256.png" />

---

Vanilla JS API for reusable components

Built into the browser

Easily polyfill-able

---

```js
  class BetterImg extends HTMLElement {

    constructor() {
      super();
      this.usingFallback = false;
    }

    get defaultWidth() {
      return 480;
    }

    get defaultHeight() {
      return 640;
    }

    connectedCallback() {
      this.init();
    }

    init() {
      this.innerHTML = this.template;
      this.addErrorListener();
      this.setSrc(this.url);
    }

    addErrorListener() {
      this.querySelector('img').onerror = this.onImgError.bind(this);
    }

    get url() {
      return this.getAttribute('url');
    }

    set url(value) {
      return this.url = value;
    }

    get width() {
      return this.getAttribute('width') || this.defaultWidth;
    }

    get height() {
      return this.getAttribute('height') || this.defaultHeight;
    }

    get fallback() {
      return this.getAttribute('fallback');
    }

    get logCallback() {
      return this.getAttribute('log');
    }

    get altText() {
      return this.getAttribute('alt') || "";
    }

    get template() {
      return `
        <img
          width=${this.width}
          height=${this.height}
          alt="${this.altText}"
        />
      `;
    }

    onImgError(err) {
      this.logError(err);
      this.useFallback();
    }

    useFallback() {
      if(this.fallback && !this.usingFallback) {
        this.setAttribute('url', this.fallback);
        this.setSrc(this.fallback);
        this.usingFallback = true;
      }
    }

    logError(err) {
      if(this.logCallback){
        window[this.logCallback](err);
      }
    }

    setSrc(url) {
      this.querySelector('img').src = url;
    }
  }

  customElements.define('better-img', BetterImg);
```

---

## Powerful...

<p class="fragment">But too low level</p>

---

- Reactive Data-binding
- Virtual DOM
- TypeScript support
- Async rendering ala React Fiber
- JSX
- SSR, pre-compilation

---

<!-- .slide: data-background="white" -->

<img src="imgs/stencil-logo.svg" width="200" />

<h1 style="color: #5850FF; font-weight: bolder;" >Stencil</h1>

---

- **Not a framework**
- Build time API
- Outputs Vanilla Web Components
- Borrows from other frameworks
<p class="fragment"> Did I mention, it's not a framework?</p>

---

<!-- .slide: data-background="#1b2b34" -->

<h1>
  <code style="color: #99c794">$ Demo</code>
</h1>

---

### API

<table>
  <tbody>
    <tr class="odd">
      <td><code>@Component</code></td>
      <td>Decorate a class a web component</td>
    </tr>
    <tr class="even">
      <td><code>@Prop()</code></td>
      <td>Expose a class property as an element property</td>
    </tr>
    <tr class="odd">
      <td><code>@State()</code></td>
      <td>Internal data that can cause a rerender</td>
    </tr>
    <tr class="even">
      <td><code>@Event()</code></td>
      <td>Decorator for custom events</td>
    </tr>
    <tr class="odd">
      <td><code>@Listen()</code></td>
      <td>Decorator for listening to custom events</td>
    </tr>
    <tr class="even">
      <td><code>@Element()</code></td>
      <td>Get a raw DOM reference to the current component</td>
    </tr>
  </tbody>
</table>

---

### Why make Stencil?
- Performance
- Stability
- Interoperability

---

### Who's this for

- **For us**
- UI framework authors
- Large dev teams
- App Devs

---

### What's next?

- Docs: [stenciljs.com](https://stenciljs.com/docs/intro)
- Demos: [Async Rendering](https://stencil-fiber-demo.firebaseapp.com)
- [Kind Community words](https://medium.com/@sinedied/stencil-js-its-finally-time-for-vanilla-web-components-927d26b573e1)
- Web-Component based State Mgmt?

---


### Build something cool?

Let us know, [@stenciljs](https://twitter.com/@stenciljs)

<img src="https://img.shields.io/badge/-Built%20With%20Stencil-16161d.svg?logo=data%3Aimage%2Fsvg%2Bxml%3Bbase64%2CPD94bWwgdmVyc2lvbj0iMS4wIiBlbmNvZGluZz0idXRmLTgiPz4KPCEtLSBHZW5lcmF0b3I6IEFkb2JlIElsbHVzdHJhdG9yIDE5LjIuMSwgU1ZHIEV4cG9ydCBQbHVnLUluIC4gU1ZHIFZlcnNpb246IDYuMDAgQnVpbGQgMCkgIC0tPgo8c3ZnIHZlcnNpb249IjEuMSIgaWQ9IkxheWVyXzEiIHhtbG5zPSJodHRwOi8vd3d3LnczLm9yZy8yMDAwL3N2ZyIgeG1sbnM6eGxpbms9Imh0dHA6Ly93d3cudzMub3JnLzE5OTkveGxpbmsiIHg9IjBweCIgeT0iMHB4IgoJIHZpZXdCb3g9IjAgMCA1MTIgNTEyIiBzdHlsZT0iZW5hYmxlLWJhY2tncm91bmQ6bmV3IDAgMCA1MTIgNTEyOyIgeG1sOnNwYWNlPSJwcmVzZXJ2ZSI%2BCjxzdHlsZSB0eXBlPSJ0ZXh0L2NzcyI%2BCgkuc3Qwe2ZpbGw6I0ZGRkZGRjt9Cjwvc3R5bGU%2BCjxwYXRoIGNsYXNzPSJzdDAiIGQ9Ik00MjQuNywzNzMuOWMwLDM3LjYtNTUuMSw2OC42LTkyLjcsNjguNkgxODAuNGMtMzcuOSwwLTkyLjctMzAuNy05Mi43LTY4LjZ2LTMuNmgzMzYuOVYzNzMuOXoiLz4KPHBhdGggY2xhc3M9InN0MCIgZD0iTTQyNC43LDI5Mi4xSDE4MC40Yy0zNy42LDAtOTIuNy0zMS05Mi43LTY4LjZ2LTMuNkgzMzJjMzcuNiwwLDkyLjcsMzEsOTIuNyw2OC42VjI5Mi4xeiIvPgo8cGF0aCBjbGFzcz0ic3QwIiBkPSJNNDI0LjcsMTQxLjdIODcuN3YtMy42YzAtMzcuNiw1NC44LTY4LjYsOTIuNy02OC42SDMzMmMzNy45LDAsOTIuNywzMC43LDkyLjcsNjguNlYxNDEuN3oiLz4KPC9zdmc%2BCg%3D%3D&colorA=16161d&style=flat-square" width="300" alt="">

---

## Thank you!

#### [stenciljs.com](https://stenciljs.com/)


`</html>`

