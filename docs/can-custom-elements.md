@module {function} can-custom-elements
@parent can-ecosystem
@group can-custom-elements.properties 1 properties
@group can-custom-elements.modules 2 modules
@group can-custom-elements.types 3 types

@description Allows you to create [custom element](https://developer.mozilla.org/en-US/docs/Web/Web_Components/Custom_Elements) classes with CanJS.

Safari only supports custom elements that derive from HTMLElement, so you'll usually want to use [can-custom-elements.element].

@signature `CustomElement(Element)`

Create a base Element class based on `Element`, any element that derives from [HTMLElement](https://developer.mozilla.org/en-US/docs/Web/API/HTMLElement).

**Important**: Safari only supports custom elements that derive from [HTMLElement].

```js
var CustomElement = require("can-custom-element");

var SuperButton = class extends CustomElement(HTMLButtonElement) {

};

customElements.define("super-button", SuperButton);
```

@param {HTMLElement} Element The base element from which to derive.
@return {can-custom-elements.CanElement} A derived element with CanJS behaviors added.

@body

## Use

`can-custom-elements` makes it possible to create standard custom elements (part of [web components](https://developer.mozilla.org/en-US/docs/Web/Web_Components)).

Use can-custom-elements to create a class that can be passed into [customElements.define](https://developer.mozilla.org/en-US/docs/Web/API/CustomElementRegistry/define) to register the element in the window.

```js
var Element = require("can-custom-elements").Element;
var stache = require("can-stache");
var define = require("can-define");

var view = stache("Hello {{name}}");

var MyApp = class extends Element {
	static get view() {
		return view;
	}
};

define(MyApp.prototype, {
	name: {
		value: "world"
	}
});

customElements.define("my-app", MyApp);

var el = document.createElement("my-app");

el.name; // -> "world"
```