# vuejs-dynamic-fields

A VueJs component for building dynamic form field or complete forms. With small json configuration or from an API builded on a backend, you create forms or partials of forms

### Installation and config
```
npm install vuejs-dynamic-fields
```
then import the to your root or parent component

To set this component as a complete form, set the 'fullForm' property to true. This way, you can have a complete form in one component.

Set to false if you only want to use it as partials of fields and do the data logic outside the component.

```
<dynamic-fields :fullForm="true"></dynamic-fields>
```

If is set to false, put the component inside form tags. This way you can put sets of fields on different places of your app
```
<form action="/some/route" @submit="doSomething"
    <dynamic-fields :fullForm="true"></dynamic-fields>
</form>
```

If used as a full complete form, when submited, it emits an event called 'posted' with all the data fields. This way you can process any logic on posted event.


### Options

```
[
    {
        property: 'attribute',
    }
]
```

Each object is an input field. It needs some basic properties to be defined.

## type, name, label and placehoder
The type property it's what defines the type of field, 'text', 'email', textarea, radio, ...
I will place on the bottom all the possible types of fields that are suported

```
[
    {
        type: 'text',
        name: 'adress',
        showlabel: true,
        label: 'Adress,
        placeholder: 'You Adress Here',
    }
]
```
## CSS .class
Every field has a 'wrapper div' which can receive a css class if you use some framework like Bootstrap for form-groups. Beside the wrapper, each field can receive unlimited css classes.

```
[
    {
        type: 'text',
        name: 'adress',
        showlabel: true,
        label: 'Adress,
        placeholder: 'You Adress Here',
        cssClass: 'some-input-class othe-class input-error',
        wrapperClass: 'main-form-fields'
    }
]
```


## Order

All fields can be arranged by any order. Just refer the property to orderBy when placing the component. If not defined, the field will be arranged by the same order of the json object received.

On the markup:
```
<dynamic-fields :fullForm="true" :order="'order_id'"></dynamic-fields>
```

On the object
```
[
    {
        type: 'text',
        name: 'adress',
        showlabel: true,
        label: 'Adress,
        placeholder: 'You Adress Here',
        cssClass: 'some-input-class othe-class input-error',
        wrapperClass: 'main-form-fields',
        order_id: 2,
    }
]
```
## Validation

Of course I don't advise to make validations only with HTML5 data atrtributes, but you can add the require attribute simply addind: is_required: boolean

```
[
    {
        type: 'text',
        name: 'adress',
        showlabel: true,
        label: 'Adress,
        placeholder: 'You Adress Here',
        cssClass: 'some-input-class othe-class input-error',
        wrapperClass: 'main-form-fields',
        order_id: 2,
        is_required: boolean
    }
]
```

## Select, Radio buttons and Checkbox

If a field is defined like any of these types, it has to be defined the options. Here is an example:

```
[
    {
        type: 'select',
        options: [
            'Portugal',
            'Spain',
            'France'
        ],
        name: 'country',
        wrapperClass: 'main-form-fields',
        order_id: 3,
    }
]
```
## Button

To define a field like a button to submit, in case you use as a complete form, it has to have the 'buttonText' property, in addition to others like 'cssClass' or 'wrapperClass':

```
[
    {
        type: 'button',
        name: 'button',
        buttonText: 'SEND'
        wrapperClass: 'main-form-fields',
        order_id: 12,
    }
]
```

## HTML blocks

This component is prepared to have some html objects between input fields. For example, error or success messages or separators of possible sections on your form.
The configuration is the same of any field:

```
{
    type: 'html',
    cssClass: 'some-class other-class',
    html: '<p>all fields are required</p>',
    (...)
}
```
### All possible types of fields:
*text

*textarea

*email

*password

*select

*checkbox

*radio

*button

*hidden
