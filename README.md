# 🏁 Final Form

![Final Form](banner.png)

[![NPM Version](https://img.shields.io/npm/v/final-form.svg?style=flat)](https://www.npmjs.com/package/final-form)
[![NPM Downloads](https://img.shields.io/npm/dm/final-form.svg?style=flat)](https://www.npmjs.com/package/final-form)
[![Build Status](https://travis-ci.org/final-form/final-form.svg?branch=master)](https://travis-ci.org/final-form/final-form)
[![codecov.io](https://codecov.io/gh/final-form/final-form/branch/master/graph/badge.svg)](https://codecov.io/gh/final-form/final-form)
[![styled with prettier](https://img.shields.io/badge/styled_with-prettier-ff69b4.svg)](https://github.com/prettier/prettier)

✅ **Zero** dependencies

✅ Framework agnostic

✅ Opt-in subscriptions - only update on the state you need!

✅ 💥 **3.5k gzipped** 💥

---

## Installation

```bash
npm install --save final-form
```

or

```bash
yarn add final-form
```

## Getting Started

🏁 Final Form works on subscriptions to perform updates based on the
[Observer pattern](https://en.wikipedia.org/wiki/Observer_pattern). Both form
and field subscribers must specify exactly which parts of the form state they
want to receive updates about.

```js
import { createForm } from 'final-form'

// Create Form
const form = createForm({
  initialValues,
  onSubmit, // required
  validate
})

// Subscribe to form state updates
const unsubscribe = form.subscribe(
  formState => {
    // Update UI
  },
  { // FormSubscription: the list of values you want to be updated about
    dirty: true,
    valid: true,
    values: true
  }
})

// Subscribe to field state updates
const unregisterField = form.registerField(
  'username',
  fieldState => {
    // Update field UI
    const { blur, change, focus, ...rest } = fieldState
    // In addition to the values you subscribe to, field state also
    // includes functions that your inputs need to update their state.
  },
  { // FieldSubscription: the list of values you want to be updated about
    active: true,
    dirty: true,
    touched: true,
    valid: true,
    value: true
  }
)

// Submit
form.submit() // only submits if all validation passes
```

## Table of Contents

<!-- START doctoc generated TOC please keep comment here to allow auto update -->

<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

* [Examples](#examples)
  * [Simple React Example](#simple-react-example)
* [Libraries](#libraries)
  * [🏁 React Final Form](#-react-final-form)
* [API](#api)
  * [`createForm: (config: Config) => FormApi`](#createform-config-config--formapi)
  * [`fieldSubscriptionItems: string[]`](#fieldsubscriptionitems-string)
  * [`formSubscriptionItems: string[]`](#formsubscriptionitems-string)
  * [`FORM_ERROR: Symbol`](#form_error-symbol)
  * [`version: string`](#version-string)
* [Types](#types)
  * [`Config`](#config)
    * [`debug?: DebugFunction`](#debug-debugfunction)
    * [`initialValues?: Object`](#initialvalues-object)
    * [`mutators?: { [string]: Mutator }`](#mutators--string-mutator-)
    * [`onSubmit: (values: Object, callback: ?(errors: ?Object) => void) => ?Object | Promise<?Object> | void`](#onsubmit-values-object-callback-errors-object--void--object--promiseobject--void)
    * [`validate?: (values: Object) => Object | Promise<Object>`](#validate-values-object--object--promiseobject)
    * [`validateOnBlur?: boolean`](#validateonblur-boolean)
  * [`DebugFunction: (state: FormState, fieldStates: { [string]: FieldState }) => void`](#debugfunction-state-formstate-fieldstates--string-fieldstate---void)
  * [`Decorator: (form: FormApi) => Unsubscribe`](#decorator-form-formapi--unsubscribe)
  * [`FieldState`](#fieldstate)
    * [`active?: boolean`](#active-boolean)
    * [`blur: () => void`](#blur---void)
    * [`change: (value: any) => void`](#change-value-any--void)
    * [`data?: Object`](#data-object)
    * [`dirty?: boolean`](#dirty-boolean)
    * [`error?: any`](#error-any)
    * [`focus: () => void`](#focus---void)
    * [`initial?: any`](#initial-any)
    * [`invalid?: boolean`](#invalid-boolean)
    * [`length?: number`](#length-number)
    * [`name: string`](#name-string)
    * [`pristine?: boolean`](#pristine-boolean)
    * [`submitError?: any`](#submiterror-any)
    * [`submitFailed?: boolean`](#submitfailed-boolean)
    * [`submitSucceeded?: boolean`](#submitsucceeded-boolean)
    * [`touched?: boolean`](#touched-boolean)
    * [`valid?: boolean`](#valid-boolean)
    * [`value?: any`](#value-any)
    * [`visited?: boolean`](#visited-boolean)
  * [`FieldSubscriber: (state: FieldState) => void`](#fieldsubscriber-state-fieldstate--void)
  * [`FieldSubscription: { [string]: boolean }`](#fieldsubscription--string-boolean-)
    * [`active?: boolean`](#active-boolean-1)
    * [`data?: boolean`](#data-boolean)
    * [`dirty?: boolean`](#dirty-boolean-1)
    * [`error?: boolean`](#error-boolean)
    * [`initial?: boolean`](#initial-boolean)
    * [`invalid?: boolean`](#invalid-boolean-1)
    * [`length?: boolean`](#length-boolean)
    * [`pristine?: boolean`](#pristine-boolean-1)
    * [`submitError?: boolean`](#submiterror-boolean)
    * [`submitFailed?: boolean`](#submitfailed-boolean-1)
    * [`submitSucceeded?: boolean`](#submitsucceeded-boolean-1)
    * [`touched?: boolean`](#touched-boolean-1)
    * [`valid?: boolean`](#valid-boolean-1)
    * [`value?: boolean`](#value-boolean)
    * [`visited?: boolean`](#visited-boolean-1)
  * [`FormApi`](#formapi)
    * [`batch: (fn: () => void) => void)`](#batch-fn---void--void)
    * [`blur: (name: string) => void`](#blur-name-string--void)
    * [`change: (name: string, value: ?any) => void`](#change-name-string-value-any--void)
    * [`focus: (name: string) => void`](#focus-name-string--void)
    * [`getRegisteredFields: () => string[]`](#getregisteredfields---string)
    * [`getState: () => FormState`](#getstate---formstate)
    * [`initialize: (values: Object) => void`](#initialize-values-object--void)
    * [`mutators: ?{ [string]: Function }`](#mutators--string-function-)
    * [`submit: () => ?Promise<?Object>`](#submit---promiseobject)
    * [`subscribe: (subscriber: FormSubscriber, subscription: FormSubscription) => Unsubscribe`](#subscribe-subscriber-formsubscriber-subscription-formsubscription--unsubscribe)
    * [`registerField: RegisterField`](#registerfield-registerfield)
    * [`reset: () => void`](#reset---void)
  * [`FormState`](#formstate)
    * [`active?: string`](#active-string)
    * [`dirty?: boolean`](#dirty-boolean-2)
    * [`error?: any`](#error-any-1)
    * [`errors?: Object`](#errors-object)
    * [`initialValues?: Object`](#initialvalues-object-1)
    * [`invalid?: boolean`](#invalid-boolean-2)
    * [`pristine?: boolean`](#pristine-boolean-2)
    * [`submitError?: any`](#submiterror-any-1)
    * [`submitErrors?: Object`](#submiterrors-object)
    * [`submitFailed?: boolean`](#submitfailed-boolean-2)
    * [`submitSucceeded?: boolean`](#submitsucceeded-boolean-2)
    * [`submitting?: boolean`](#submitting-boolean)
    * [`valid?: boolean`](#valid-boolean-2)
    * [`validating?: boolean`](#validating-boolean)
    * [`values?: Object`](#values-object)
  * [`FormSubscriber: (state: FormState) => void`](#formsubscriber-state-formstate--void)
  * [`FormSubscription: { [string]: boolean }`](#formsubscription--string-boolean-)
    * [`active?: boolean`](#active-boolean-2)
    * [`dirty?: boolean`](#dirty-boolean-3)
    * [`error?: boolean`](#error-boolean-1)
    * [`errors?: boolean`](#errors-boolean)
    * [`initialValues?: boolean`](#initialvalues-boolean)
    * [`invalid?: boolean`](#invalid-boolean-3)
    * [`pristine?: boolean`](#pristine-boolean-3)
    * [`submitError?: boolean`](#submiterror-boolean-1)
    * [`submitErrors?: boolean`](#submiterrors-boolean)
    * [`submitFailed?: boolean`](#submitfailed-boolean-3)
    * [`submitSucceeded?: boolean`](#submitsucceeded-boolean-3)
    * [`submitting?: boolean`](#submitting-boolean-1)
    * [`valid?: boolean`](#valid-boolean-3)
    * [`validating?: boolean`](#validating-boolean-1)
    * [`values?: boolean`](#values-boolean)
  * [`InternalFieldState`](#internalfieldstate)
    * [`active: boolean`](#active-boolean)
    * [`blur: () => void`](#blur---void-1)
    * [`change: (value: any) => void`](#change-value-any--void-1)
    * [`data: Object`](#data-object)
    * [`error?: any`](#error-any-2)
    * [`focus: () => void`](#focus---void-1)
    * [`initial?: any`](#initial-any-1)
    * [`name: string`](#name-string-1)
    * [`pristine: boolean`](#pristine-boolean)
    * [`submitError?: any`](#submiterror-any-2)
    * [`touched: boolean`](#touched-boolean)
    * [`valid: boolean`](#valid-boolean)
    * [`value?: any`](#value-any-1)
    * [`visited: boolean`](#visited-boolean)
  * [`InternalFormState`](#internalformstate)
    * [`active?: string`](#active-string-1)
    * [`error?: any`](#error-any-3)
    * [`errors: Object`](#errors-object)
    * [`initialValues?: Object`](#initialvalues-object-2)
    * [`pristine: boolean`](#pristine-boolean-1)
    * [`submitError: any`](#submiterror-any)
    * [`submitErrors?: Object`](#submiterrors-object-1)
    * [`submitFailed: boolean`](#submitfailed-boolean)
    * [`submitSucceeded: boolean`](#submitsucceeded-boolean)
    * [`submitting: boolean`](#submitting-boolean)
    * [`valid: boolean`](#valid-boolean-1)
    * [`validating: number`](#validating-number)
    * [`values: Object`](#values-object)
  * [`MutableState: { formState: InternalFormState, fields: { [string]: InternalFieldState } }`](#mutablestate--formstate-internalformstate-fields--string-internalfieldstate--)
  * [`Mutator: (args: any[], state: MutableState, tools: Tools) => any`](#mutator-args-any-state-mutablestate-tools-tools--any)
  * [`RegisterField: (name: string, subscriber: FieldSubscriber, subscription: FieldSubscription, validate?: (value: ?any, allValues: Object) => ?any) => Unsubscribe`](#registerfield-name-string-subscriber-fieldsubscriber-subscription-fieldsubscription-validate-value-any-allvalues-object--any--unsubscribe)
  * [`Tools`](#tools)
    * [`Tools.changeValue: (state: MutableState, name: string, mutate: (value: any) => any) => void`](#toolschangevalue-state-mutablestate-name-string-mutate-value-any--any--void)
    * [`Tools.getIn: (state: Object, complexKey: string) => any`](#toolsgetin-state-object-complexkey-string--any)
    * [`Tools.setIn: (state: Object, key: string, value: any) => Object`](#toolssetin-state-object-key-string-value-any--object)
    * [`Tools.shallowEqual: (a: any, b: any) => boolean`](#toolsshallowequal-a-any-b-any--boolean)
  * [`Unsubscribe : () => void`](#unsubscribe----void)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## Examples

### [Simple React Example](https://codesandbox.io/s/q78r2oqq96)

Demonstrates how 🏁 Final Form can be used inside a React component to manage
form state. It also shows just how much
[🏁 React Final Form](https://github.com/final-form/react-final-form#-react-final-form)
does for you out of the box.

For more examples using React, see
[🏁 React Final Form Examples](https://github.com/final-form/react-final-form#examples).

## Libraries

### [🏁 React Final Form](https://github.com/final-form/react-final-form#-react-final-form)

A form state management system for React that uses 🏁 Final Form under the hood.

## API

The following can be imported from `final-form`.

### `createForm: (config: Config) => FormApi`

Creates a form instance. It takes a [`Config`](#config) and returns a
[`FormApi`](#formapi).

### `fieldSubscriptionItems: string[]`

An _à la carte_ list of all the possible things you can subscribe to for a
field. Useful for subscribing to everything.

### `formSubscriptionItems: string[]`

An _à la carte_ list of all the possible things you can subscribe to for a form.
Useful for subscribing to everything.

### `FORM_ERROR: Symbol`

A special `Symbol` key used to return a whole-form error inside error objects
returned from validation or submission.

### `version: string`

The current used version of 🏁 Final Form.

---

## Types

### `Config`

#### `debug?: DebugFunction`

#### `initialValues?: Object`

The initial values of your form. These will also be used to compare against the
current values to calculate `pristine` and `dirty`.

#### `mutators?: { [string]: Mutator }`

Optional named mutation functions.

#### `onSubmit: (values: Object, callback: ?(errors: ?Object) => void) => ?Object | Promise<?Object> | void`

Function to call when the form is submitted. There are three possible ways to
write an `onSubmit` function:

* Synchronously: returns `undefined` on success, or an `Object` of submission
  errors on failure
* Asynchronously with a callback: returns `undefined`, calls `callback()` with
  no arguments on success, or with an `Object` of submission errors on failure.
* Asynchronously with a `Promise`: returns a `Promise<?Object>` that resolves
  with no value on success or _resolves_ with an `Object` of submission errors
  on failure. The reason it _resolves_ with errors is to leave _rejection_ for
  when there is a server or communications error.

Submission errors must be in the same shape as the values of the form. You may
return a generic error for the whole form (e.g. `'Login Failed'`) using the
special `FORM_ERROR` symbol key.

#### `validate?: (values: Object) => Object | Promise<Object>`

A whole-record validation function that takes all the values of the form and
returns any validation errors. There are three possible ways to write a
`validate` function:

* Synchronously: returns `{}` or `undefined` when the values are valid, or an
  `Object` of validation errors when the values are invalid.
* Asynchronously with a `Promise`: returns a `Promise<?Object>` that resolves
  with no value on success or _resolves_ with an `Object` of validation errors
  on failure. The reason it _resolves_ with errors is to leave _rejection_ for
  when there is a server or communications error.

Validation errors must be in the same shape as the values of the form. You may
return a generic error for the whole form using the special `FORM_ERROR` symbol
key.

An optional callback for debugging that returns the form state and the states of
all the fields. It's called _on every state change_. A typical thing to pass in
might be `console.log`.

#### `validateOnBlur?: boolean`

If `true`, validation will happen on blur. If `false`, validation will happen on
change. Defaults to `false`.

### `DebugFunction: (state: FormState, fieldStates: { [string]: FieldState }) => void`

### `Decorator: (form: FormApi) => Unsubscribe`

A function that [decorates](https://en.wikipedia.org/wiki/Decorator_pattern) a
form by subscribing to it and making changes as the form state changes, and
returns an [`Unsubscribe`](#unsubscribe----void) function to detach itself from
the form. e.g.
[🏁 Final Form Calculate](https://github.com/final-form/final-form-calculate).

### `FieldState`

`FieldState` is an object containing:

#### `active?: boolean`

Whether or not the field currently has focus.

#### `blur: () => void`

A function to blur the field (mark it as inactive).

#### `change: (value: any) => void`

A function to change the value of the field.

#### `data?: Object`

A place for arbitrary values to be placed by mutators.

#### `dirty?: boolean`

`true` when the value of the field is `!==` the initial value, `false` if the
values are `===`.

#### `error?: any`

The current validation error for this field.

#### `focus: () => void`

A function to focus the field (mark it as active).

#### `initial?: any`

The initial value of the field. `undefined` if it was never initialized.

#### `invalid?: boolean`

`true` if the field has a validation error or a submission error. `false`
otherwise.

#### `length?: number`

The length of the array if the value is an array. `undefined` otherwise.

#### `name: string`

The name of the field.

#### `pristine?: boolean`

`true` if the current value is `===` to the initial value, `false` if the values
are `!===`.

#### `submitError?: any`

The submission error for this field.

#### `submitFailed?: boolean`

`true` if a form submission has been tried and failed. `false` otherwise.

#### `submitSucceeded?: boolean`

`true` if the form has been successfully submitted. `false` otherwise.

#### `touched?: boolean`

`true` if this field has ever gained and lost focus. `false` otherwise. Useful
for knowing when to display error messages.

#### `valid?: boolean`

`true` if this field has no validation or submission errors. `false` otherwise.

#### `value?: any`

The value of the field.

#### `visited?: boolean`

`true` if this field has ever gained focus.

### `FieldSubscriber: (state: FieldState) => void`

### `FieldSubscription: { [string]: boolean }`

`FieldSubscription` is an object containing the following:

#### `active?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `active`
value in `FieldState`.

#### `data?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `data`
value in `FieldState`.

#### `dirty?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `dirty`
value in `FieldState`.

#### `error?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `error`
value in `FieldState`.

#### `initial?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `initial`
value in `FieldState`.

#### `invalid?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `invalid`
value in `FieldState`.

#### `length?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `length`
value in `FieldState`.

#### `pristine?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `pristine`
value in `FieldState`.

#### `submitError?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the
`submitError` value in `FieldState`.

#### `submitFailed?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the
`submitFailed` value in `FieldState`.

#### `submitSucceeded?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the
`submitSucceeded` value in `FieldState`.

#### `touched?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `touched`
value in `FieldState`.

#### `valid?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `valid`
value in `FieldState`.

#### `value?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `value`
value in `FieldState`.

#### `visited?: boolean`

When `true` the `FieldSubscriber` will be notified of changes to the `visited`
value in `FieldState`.

### `FormApi`

#### `batch: (fn: () => void) => void)`

Allows batch updates by silencing notifications while the `fn` is running.
Example:

```js
form.batch(() => {
  form.change('firstName', 'Erik') // listeners not notified
  form.change('lastName', 'Rasmussen') // listeners not notified
}) // NOW all listeners notified
```

#### `blur: (name: string) => void`

Blurs (marks inactive) the given field.

#### `change: (name: string, value: ?any) => void`

Changes the value of the given field.

#### `focus: (name: string) => void`

Focuses (marks active) the given field.

#### `getRegisteredFields: () => string[]`

Returns a list of all the currently registered fields.

#### `getState: () => FormState`

A way to request the current state of the form without subscribing.

#### `initialize: (values: Object) => void`

Initializes the form to the values provided. All the values will be set to these
values, and `dirty` and `pristine` will be calculated by performing a
shallow-equals between the current values and the values last initialized with.
The form will be `pristine` after this call.

#### `mutators: ?{ [string]: Function }`

The state-bound versions of the mutators provided to [`Config`](#config).

#### `submit: () => ?Promise<?Object>`

Submits the form if there are currently no validation errors. It may return
`undefined` or a `Promise` depending on the nature of the `onSubmit`
configuration value given to the form when it was created.

#### `subscribe: (subscriber: FormSubscriber, subscription: FormSubscription) => Unsubscribe`

Subscribes to changes to the form. **The `subscriber` will _only_ be called when
values specified in `subscription` change.** A form can have many subscribers.

#### `registerField: RegisterField`

Registers a new field and subscribes to changes to it. **The `subscriber` will
_only_ be called when the values specified in `subscription` change.** More than
one subscriber can subscribe to the same field.

This is also where you may provide an optional field-level validation function
that should return `undefined` if the value is valid, or an error. It can
optionally return a `Promise` that _resolves_ (not rejects) to `undefined` or an
error.

#### `reset: () => void`

Resets the values back to the initial values the form was initialized with. Or
empties all the values if the form was not initialized.

### `FormState`

#### `active?: string`

The name of the currently active field. `undefined` if none are active.

#### `dirty?: boolean`

`true` if the form values are different from the values it was initialized with.
`false` otherwise. Comparison is done with shallow-equals.

#### `error?: any`

The whole-form error returned by a validation function under the `FORM_ERROR`
key.

#### `errors?: Object`

An object containing all the current validation errors. The shape will match the
shape of the form's values.

#### `initialValues?: Object`

The values the form was initialized with. `undefined` if the form was never
initialized.

#### `invalid?: boolean`

`true` if any of the fields or the form has a validation or submission error.
`false` otherwise. Note that a form can be invalid even if the errors do not
belong to any currently registered fields.

#### `pristine?: boolean`

`true` if the form values are the same as the initial values. `false` otherwise.
Comparison is done with shallow-equals.

#### `submitError?: any`

The whole-form submission error returned by `onSubmit` under the `FORM_ERROR`
key.

#### `submitErrors?: Object`

An object containing all the current submission errors. The shape will match the
shape of the form's values.

#### `submitFailed?: boolean`

`true` if the form was submitted, but the submission failed with submission
errors. `false` otherwise.

#### `submitSucceeded?: boolean`

`true` if the form was successfully submitted. `false` otherwise.

#### `submitting?: boolean`

`true` if the form is currently being submitted asynchronously. `false`
otherwise.

#### `valid?: boolean`

`true` if neither the form nor any of its fields has a validation or submission
error. `false` otherwise. Note that a form can be invalid even if the errors do
not belong to any currently registered fields.

#### `validating?: boolean`

`true` if the form is currently being validated asynchronously. `false`
otherwise.

#### `values?: Object`

The current values of the form.

### `FormSubscriber: (state: FormState) => void`

### `FormSubscription: { [string]: boolean }`

`FormSubscription` is an object containing the following:

#### `active?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `active`
value in `FormState`.

#### `dirty?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `dirty`
value in `FormState`.

#### `error?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `error`
value in `FormState`.

#### `errors?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `errors`
value in `FormState`.

#### `initialValues?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the
`initialValues` value in `FormState`.

#### `invalid?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `invalid`
value in `FormState`.

#### `pristine?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `pristine`
value in `FormState`.

#### `submitError?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the
`submitError` value in `FormState`.

#### `submitErrors?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the
`submitErrors` value in `FormState`.

#### `submitFailed?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the
`submitFailed` value in `FormState`.

#### `submitSucceeded?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the
`submitSucceeded` value in `FormState`.

#### `submitting?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `submitting`
value in `FormState`.

#### `valid?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `valid`
value in `FormState`.

#### `validating?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `validating`
value in `FormState`.

#### `values?: boolean`

When `true` the `FormSubscriber` will be notified of changes to the `values`
value in `FormState`.

### `InternalFieldState`

Very similar to the published [`FieldState`](#fieldstate).

#### `active: boolean`

Whether or not the field currently has focus.

#### `blur: () => void`

A function to blur the field (mark it as inactive).

#### `change: (value: any) => void`

A function to change the value of the field.

#### `data: Object`

A place for arbitrary values to be placed by mutators.

#### `error?: any`

The current validation error for this field.

#### `focus: () => void`

A function to focus the field (mark it as active).

#### `initial?: any`

The initial value of the field. `undefined` if it was never initialized.

#### `name: string`

The name of the field.

#### `pristine: boolean`

`true` if the current value is `===` to the initial value, `false` if the values
are `!===`.

#### `submitError?: any`

The submission error for this field.

#### `touched: boolean`

`true` if this field has ever gained and lost focus. `false` otherwise. Useful
for knowing when to display error messages.

#### `valid: boolean`

`true` if this field has no validation or submission errors. `false` otherwise.

#### `value?: any`

The value of the field.

#### `visited: boolean`

`true` if this field has ever gained focus.

### `InternalFormState`

Very similar to the published [`FormState`](#formstate), with a few minor
differences.

#### `active?: string`

The name of the currently active field. `undefined` if none are active.

#### `error?: any`

The whole-form error returned by a validation function under the `FORM_ERROR`
key.

#### `errors: Object`

An object containing all the current validation errors. The shape will match the
shape of the form's values.

#### `initialValues?: Object`

The values the form was initialized with. `undefined` if the form was never
initialized.

#### `pristine: boolean`

`true` if the form values are the same as the initial values. `false` otherwise.
Comparison is done with shallow-equals.

#### `submitError: any`

The whole-form submission error returned by `onSubmit` under the `FORM_ERROR`
key.

#### `submitErrors?: Object`

An object containing all the current submission errors. The shape will match the
shape of the form's values.

#### `submitFailed: boolean`

`true` if the form was submitted, but the submission failed with submission
errors. `false` otherwise.

#### `submitSucceeded: boolean`

`true` if the form was successfully submitted. `false` otherwise.

#### `submitting: boolean`

`true` if the form is currently being submitted asynchronously. `false`
otherwise.

#### `valid: boolean`

`true` if neither the form nor any of its fields has a validation or submission
error. `false` otherwise. Note that a form can be invalid even if the errors do
not belong to any currently registered fields.

#### `validating: number`

The number of asynchronous validators currently running.

#### `values: Object`

The current values of the form.

### `MutableState: { formState: InternalFormState, fields: { [string]: InternalFieldState } }`

A container for the [`InternalFormState`](#internalformstate) and an object of
[`InternalFieldState`](#internalfieldstate)s.

### `Mutator: (args: any[], state: MutableState, tools: Tools) => any`

A mutator function that takes some arguments, the internal form
[`MutableState`](#mutablestate), and some [`Tools`](#tools) and optionally
modifies the form state.

### `RegisterField: (name: string, subscriber: FieldSubscriber, subscription: FieldSubscription, validate?: (value: ?any, allValues: Object) => ?any) => Unsubscribe`

### `Tools`

An object containing:

#### `Tools.changeValue: (state: MutableState, name: string, mutate: (value: any) => any) => void`

A utility function to modify a single field value in form state. `mutate()`
takes the old value and returns the new value.

#### `Tools.getIn: (state: Object, complexKey: string) => any`

A utility function to get any arbitrarily deep value from an object using
dot-and-bracket syntax (e.g. `some.deep.values[3].whatever`).

#### `Tools.setIn: (state: Object, key: string, value: any) => Object`

A utility function to set any arbitrarily deep value inside an object using
dot-and-bracket syntax (e.g. `some.deep.values[3].whatever`). Note: it does
**not** mutate the object, but returns a new object.

#### `Tools.shallowEqual: (a: any, b: any) => boolean`

A utility function to compare the keys of two objects. Returns `true` if the
objects have the same keys and the values are `===`, `false` otherwise.

### `Unsubscribe : () => void`

Unsubscribes a listener.
