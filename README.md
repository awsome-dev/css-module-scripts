# CSS module scripts

- import attribute
  - [Browser support - web-platform-tests/interop](https://github.com/web-platform-tests/interop/issues/597)
  - [Spec - TC39](https://github.com/tc39/proposal-import-attributes)
  - [Spec - WHATWG](https://github.com/whatwg/html/pull/4898)
  - Standards Positions
    - [WebKit](https://github.com/WebKit/standards-positions/issues/128)
    - [Mozilla](https://github.com/mozilla/standards-positions/issues/373)
  - implementation
    - [ ] [TypeScript](https://github.com/microsoft/TypeScript/issues/46689)
    - [x] [Rollup](https://rollupjs.org/configuration-options/#output-externalimportattributes)
    - [x] [SWC](https://github.com/swc-project/swc/pull/7868)
    - [x] [Babel](https://babeljs.io/docs/babel-plugin-proposal-import-attributes-to-assertions) [Babel 7.22.0](https://babeljs.io/blog/2023/05/26/7.22.0#import-attributes-15536-15620)
    - [ ] [esbuild](https://github.com/evanw/esbuild/issues/3384)
- Constructible style sheets / adoptedStyleSheets property
  - [Browser support - caniuse.com](https://caniuse.com/?search=adoptedStyleSheets)
  - [Constructible style sheets/adopted style sheets polyfill](https://github.com/calebdwilliams/construct-style-sheets)
  - [adoptedStyleSheets - MDN](https://developer.mozilla.org/en-US/docs/Web/API/Document/adoptedStyleSheets)

### Sample Code

```ts
const tagName = 'sample-elements'
const cssfile = `./${tagName}.css`
class SampleElement extends HTMLElement {
  constructor() {
    super();
    if (this.shadowRoot　=== null) {
      const shadow = this.attachShadow({mode: 'open'})
      const tmpl = this.querySelector('template')
      if (tmpl !== null) {
        shadow.appendChild(tmpl.content.cloneNode(true))
      }
    }
  }
  connectedCallback() {
    const shadow = this.shadowRoot
    if (shadow !== null) {
      shadow.addEventListener('click', async (_) => {
        const css = await import(cssfile, { with: { type: 'css' } });
          shadow.adoptedStyleSheets = [css]
      })
    }
  }
}
customElements.define(tagName, SampleElement);
```
