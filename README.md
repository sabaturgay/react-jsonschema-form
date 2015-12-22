react-jsonschema-form
=====================

[![Build Status](https://travis-ci.org/mozilla-services/react-jsonschema-form.svg)](https://travis-ci.org/mozilla-services/react-jsonschema-form)

A simple [React](http://facebook.github.io/react/) component capable of building HTML forms out of a [JSON schema](http://jsonschema.net/).

Requires React 0.14+.

## Installation

As a npm-based project dependency:

```
$ npm install react-jsonschema-form --save
```

As a script dependency served from a CDN:

```html
  <script src="https://npmcdn.com/react-jsonschema-form@0.3.0/dist/react-jsonschema-form-0.3.0.js"></script>
```

Source maps are available at [this url](https://npmcdn.com/react-jsonschema-form@0.1.0/dist/react-jsonschema-form-0.1.0.js.map).

Note that the CDN version **does not** embed *react* nor *react-dom*.

## Usage

```js
import React, { Component } from "react";
import { render } from "react-dom";

import Form from "react-jsonschema-form";

const schema = {
  title: "Todo Tasks",
  type: "object",
  required: ["title"],
  properties: {
    title: {type: "string", title: "Title", default: "A new task"},
    done: {type: "boolean", title: "Done?", default: false}
  }
};

const formData =  {
  title: "First task",
  done: true
};

const log = (type) => console.log.bind(console, type);

render((
  <Form schema={schema}
        formData={formData}
        onChange={log("changed")}
        onSubmit={log("submitted")}
        onError={log("errors")} />
), document.getElementById("app"));
```

### Alternative widgets

JSONSchema is limited for describing how a given data type should be rendered as an input component, that's why this lib introduces the concept of *UI schema*. A UI schema is basically an object literal describing which UI widget should be used to render a certain field

Example:

```js
const uiSchema =  {
  done: {
    widget: "radio" // could also be "select"
  }
};

render((
  <Form schema={schema}
        uiSchema={uiSchema}
        formData={formData} />
), document.getElementById("app"));
```

Here's a list of supported alternative widgets for different JSONSchema data types:

#### `boolean`

  * `radio`: a radio button group with `true` and `false` as selectable values;
  * `select`: a select box with `true` and `false` as options;
  * by default, a checkbox is used

#### `string`:

  * `textarea`: a `textarea` element
  * by default, a regular `input[type=text]` element is used.

## Development server

```
$ npm start
```

A [Cosmos development server](https://github.com/skidding/cosmos) showcasing components with hot reload enabled is available at [localhost:8080](http://localhost:8080).

## Tests

```
$ npm test
```

### TDD

```
$ npm run tdd
```

## License

Apache 2
