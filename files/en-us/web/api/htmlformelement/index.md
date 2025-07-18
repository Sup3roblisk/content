---
title: HTMLFormElement
slug: Web/API/HTMLFormElement
page-type: web-api-interface
browser-compat: api.HTMLFormElement
---

{{APIRef("HTML DOM")}}

The **`HTMLFormElement`** interface represents a {{HTMLElement("form")}} element in the DOM. It allows access to—and, in some cases, modification of—aspects of the form, as well as access to its component elements.

{{InheritanceDiagram}}

## Instance properties

_This interface also inherits properties from its parent, {{domxref("HTMLElement")}}._

- {{domxref("HTMLFormElement.acceptCharset")}}
  - : A string reflecting the value of the form's [`accept-charset`](/en-US/docs/Web/HTML/Reference/Elements/form#accept-charset) HTML attribute.
- {{domxref("HTMLFormElement.action")}}
  - : A string reflecting the value of the form's [`action`](/en-US/docs/Web/HTML/Reference/Elements/form#action) HTML attribute, containing the URI of a program that processes the information submitted by the form.
- {{domxref("HTMLFormElement.autocomplete")}}
  - : A string reflecting the value of the form's [`autocomplete`](/en-US/docs/Web/HTML/Reference/Attributes/autocomplete) HTML attribute, indicating whether the controls in this form can have their values automatically populated by the browser.
- {{domxref("HTMLFormElement.encoding")}} or {{domxref("HTMLFormElement.enctype")}}
  - : A string reflecting the value of the form's [`enctype`](/en-US/docs/Web/HTML/Reference/Elements/form#enctype) HTML attribute, indicating the type of content that is used to transmit the form to the server. Only specified values can be set. The two properties are synonyms.
- {{domxref("HTMLFormElement.elements")}} {{ReadOnlyInline}}
  - : A {{domxref("HTMLFormControlsCollection")}} holding all form controls belonging to this form element.
- {{domxref("HTMLFormElement.length")}} {{ReadOnlyInline}}
  - : A `long` reflecting the number of controls in the form.
- {{domxref("HTMLFormElement.name")}}
  - : A string reflecting the value of the form's [`name`](/en-US/docs/Web/HTML/Reference/Elements/form#name) HTML attribute, containing the name of the form.
- {{domxref("HTMLFormElement.noValidate")}}
  - : A boolean value reflecting the value of the form's [`novalidate`](/en-US/docs/Web/HTML/Reference/Elements/form#novalidate) HTML attribute, indicating whether the form should not be validated.
- {{domxref("HTMLFormElement.method")}}
  - : A string reflecting the value of the form's [`method`](/en-US/docs/Web/HTML/Reference/Elements/form#method) HTML attribute, indicating the HTTP method used to submit the form. Only specified values can be set.
- {{domxref("HTMLFormElement.rel")}}
  - : A string reflecting the value of the form's [`rel`](/en-US/docs/Web/HTML/Reference/Attributes/rel) HTML attribute, which represents what kinds of links the form creates as a space-separated list of enumerated values.
- {{domxref("HTMLFormElement.relList")}} {{ReadOnlyInline}}
  - : A {{domxref("DOMTokenList")}} that reflects the [`rel`](/en-US/docs/Web/HTML/Reference/Attributes/rel) HTML attribute, as a list of tokens.
- {{domxref("HTMLFormElement.target")}}
  - : A string reflecting the value of the form's [`target`](/en-US/docs/Web/HTML/Reference/Elements/form#target) HTML attribute, indicating where to display the results received from submitting the form.

Named inputs are added to their owner form instance as properties, and can overwrite native properties if they share the same name (e.g., a form with an input named `action` will have its `action` property return that input instead of the form's [`action`](/en-US/docs/Web/HTML/Reference/Elements/form#action) HTML attribute).

## Instance methods

_This interface also inherits methods from its parent, {{domxref("HTMLElement")}}._

- {{domxref("HTMLFormElement.checkValidity", "checkValidity()")}}
  - : Returns `true` if the element's child controls are subject to [constraint validation](/en-US/docs/Web/HTML/Guides/Constraint_validation) and satisfy those constraints; returns `false` if some controls do not satisfy their constraints. Fires an event named {{domxref("HTMLInputElement/invalid_event", "invalid")}} at any control that does not satisfy its constraints; such controls are considered invalid if the event is not canceled. It is up to the programmer to decide how to respond to `false`.
- {{domxref("HTMLFormElement.reportValidity", "reportValidity()")}}
  - : Returns `true` if the element's child controls satisfy their [validation constraints](/en-US/docs/Web/HTML/Guides/Constraint_validation). When `false` is returned, cancelable {{domxref("HTMLInputElement/invalid_event", "invalid")}} events are fired for each invalid child and validation problems are reported to the user.
- {{domxref("HTMLFormElement.requestSubmit", "requestSubmit()")}}
  - : Requests that the form be submitted using the specified submit button and its corresponding configuration.
- {{domxref("HTMLFormElement.reset", "reset()")}}
  - : Resets the form to its initial state.
- {{domxref("HTMLFormElement.submit", "submit()")}}
  - : Submits the form to the server.

## Events

Listen to these events using `addEventListener()`, or by assigning an event listener to the `oneventname` property of this interface.

- {{domxref("HTMLFormElement/formdata_event", "formdata")}}
  - : The `formdata` event fires after the entry list representing the form's data is constructed.
- {{domxref("HTMLFormElement/reset_event", "reset")}}
  - : The `reset` event fires when a form is reset.
- {{domxref("HTMLFormElement/submit_event", "submit")}}
  - : The `submit` event fires when a form is submitted.

## Usage notes

### Obtaining a form element object

To obtain an `HTMLFormElement` object, you can use a [CSS selector](/en-US/docs/Web/CSS/CSS_selectors) with {{domxref("Document.querySelector", "querySelector()")}}, or you can get a list of all of the forms in the document using its {{domxref("Document.forms", "forms")}} property.

{{domxref("Document.forms")}} returns an array of `HTMLFormElement` objects listing each of the forms on the page. You can then use any of the following syntaxes to get an individual form:

- `document.forms[index]`
  - : Returns the form at the specified `index` into the array of forms.
- `document.forms[id]`
  - : Returns the form whose ID is `id`.
- `document.forms[name]`
  - : Returns the form whose `name` attribute's value is `name`.

### Accessing the form's elements

You can access the list of the form's data-containing elements by examining the form's {{domxref("HTMLFormElement.elements", "elements")}} property. This returns an {{domxref("HTMLFormControlsCollection")}} listing all of the form's user data entry elements, both those which are descendants of the `<form>` and those which are made members of the form using their `form` attributes.

You can also get the form's element by using its `name` attribute as a key of the `form`, but using `elements` is a better approach—it contains _only_ the form's elements, and it cannot be mixed with other attributes of the `form`.

### Issues with Naming Elements

Some names will interfere with JavaScript access to the form's properties and elements.

For example:

- `<input name="id">` will take precedence over `<form id="…">`. This means that `form.id` will not refer to the form's id, but to the element whose name is `"id"`. This will be the case with any other form properties, such as `<input name="action">` or `<input name="post">`.
- `<input name="elements">` will render the form's `elements` collection inaccessible. The reference `form.elements` will now refer to the individual element.

To avoid such problems with element names:

- _Always_ use the `elements` collection to avoid ambiguity between an element name and a form property.
- _Never_ use `"elements"` as an element name.

If you are not using JavaScript, this will not cause a problem.

### Elements that are considered form controls

The elements included by `HTMLFormElement.elements` and `HTMLFormElement.length` are the following:

- {{HTMLElement("button")}}
- {{HTMLElement("fieldset")}}
- {{HTMLElement("input")}} (with the exception that any whose [`type`](/en-US/docs/Web/HTML/Reference/Elements/input#type) is `"image"` are omitted for historical reasons)
- {{HTMLElement("object")}}
- {{HTMLElement("output")}}
- {{HTMLElement("select")}}
- {{HTMLElement("textarea")}}

No other elements are included in the list returned by `elements`, which makes it an excellent way to get at the most important elements when processing forms.

## Examples

Creating a new form element, modifying its attributes, then submitting it:

```js
const f = document.createElement("form"); // Create a form
document.body.appendChild(f); // Add it to the document body
f.action = "/cgi-bin/some.cgi"; // Add action and method attributes
f.method = "POST";
f.submit(); // Call the form's submit() method
```

Extract information from a `<form>` element and set some of its attributes:

```html
<form name="formA" action="/cgi-bin/test" method="post">
  <p>Press "Info" for form details, or "Set" to change those details.</p>
  <p>
    <button type="button" id="info">Info</button>
    <button type="button" id="set-info">Set</button>
    <button type="reset">Reset</button>
  </p>

  <textarea id="form-info" rows="15" cols="20"></textarea>
</form>
```

```js
document.getElementById("info").addEventListener("click", () => {
  // Get a reference to the form via its name
  const f = document.forms["formA"];
  // The form properties we're interested in
  const properties = [
    "elements",
    "length",
    "name",
    "charset",
    "action",
    "acceptCharset",
    "action",
    "enctype",
    "method",
    "target",
  ];
  // Iterate over the properties, turning them into a string that we can display to the user
  const info = properties
    .map((property) => `${property}: ${f[property]}`)
    .join("\n");

  // Set the form's <textarea> to display the form's properties
  document.forms["formA"].elements["form-info"].value = info; // document.forms["formA"]['form-info'].value would also work
});

document.getElementById("set-info").addEventListener("click", (e) => {
  // Get a reference to the form via the event target
  // e.target is the button, and .form is the form it belongs to
  const f = e.target.form;
  // Argument should be a form element reference.
  f.action = "a-different-url.cgi";
  f.name = "a-different-name";
});
```

Submit a `<form>` into a new window:

```html
<form action="test.php" target="_blank">
  <p>
    <label>First name: <input type="text" name="first-name" /></label>
  </p>
  <p>
    <label>Last name: <input type="text" name="last-name" /></label>
  </p>
  <p>
    <label><input type="password" name="pwd" /></label>
  </p>

  <fieldset>
    <legend>Pet preference</legend>

    <p>
      <label><input type="radio" name="pet" value="cat" /> Cat</label>
    </p>
    <p>
      <label><input type="radio" name="pet" value="dog" /> Dog</label>
    </p>
  </fieldset>

  <fieldset>
    <legend>Owned vehicles</legend>

    <p>
      <label
        ><input type="checkbox" name="vehicle" value="Bike" />I have a
        bike</label
      >
    </p>
    <p>
      <label
        ><input type="checkbox" name="vehicle" value="Car" />I have a car</label
      >
    </p>
  </fieldset>

  <p><button>Submit</button></p>
</form>
```

## Specifications

{{Specifications}}

## Browser compatibility

{{Compat}}

## See also

- The HTML element implementing this interface: {{HTMLElement("form")}}.
