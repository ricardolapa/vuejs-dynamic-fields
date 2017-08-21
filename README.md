# vuejs-dynamic-fields
fields for forms construction

## About this component
For dynamically buid forms on VueJS. This

### Instalation
npm install vuejs-dynamic-fields --save


### Options
To set this component as a complete form, set the 'fullForm' property to true. This way, you can have a complete form in one component.

Set to false if you only want to use it as fields and do the data logic outside the component.

```
<dynamic-fields :fullForm="true"></dynamic-fields>
```

If is set to false, put the component inside form tags. This way you can put sets of fields on different places of your app
```
<form action="/some/route" @submit="doSomething"
    <dynamic-fields :fullForm="true"></dynamic-fields>
</form>
```

Every field has a 'wrapper div' which can receive a css class if you use some framework like Bootstrap for form-groups. Beside the wrapper, each field can receive unlimited css classes.
```
{ cssClass: 'some-input othe-class input-error', }
```

Order:

All fields can be arranged by any order. Just refer the property to orderBy when placing the component. If not defined, the field will be arranged by the same order of the json object received
```
<dynamic-fields :fullForm="true" :order="'order'"></dynamic-fields>
```

This component is prepared to have some html objects between input fields. For example, error or success messages or separators of possible sections of your form.
The configuration is the same of any field:
```
{
    type: 'html',
    cssClass: 'some-class other-class',
    html: '<p>all fields are required</p>',
    (...)
}
```

### All fields options:

type: str - select, text, email, textarea, radio or checkbox
name: str - input name
buttonText -str
label: str - input label
showLabel: boolean
placeholder: str - input placeholder text
options: array - options if the input type is defined as 'Select', 'radio', or 'checkbox'
is_required: boolean
