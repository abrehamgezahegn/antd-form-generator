**antd-form-generator**

This is a simple library built on top of [ant-design](http://ant.design) and [react-hook-form](https://react-hook-form.com)
That will a generate an ant design form when given a valid schema.

**Installation**
  
  npm install antd-form-generator 
  
  
  yarn add antd-form-generator
  


**_Usage_**

```javascript
import FormGenerator from "antd-form-generator";

ReactDOM.render(
  <FormGenerator
    innerClassName={"fields-container"}
    outerClassName={"form-container"}
    formSchema={[
      {
        type: "text",
        name: "firstName",
        defaultValue: "Simon",
        required: true,
        placeholder: "First name",
        label: "First name",
        fieldProps: { disabled: false },
        validation: {
          required: true,
          errorMessage: "Please make sure your input is correct",
          validate: value => value.toString().startsWith("A")
        }
      },
      {
        type: "number",
        name: "age",
        required: true,
        defaultValue: 21,
        placeholder: "Age",
        label: "Age",
        fieldProps: { disabled: false, style: { width: 300 } },
        validation: {
          required: true,
          errorMessage: "Please make sure your input is correct"
        }
      }
    ]}
    onSubmit={data => {
      // api call done here
      console.log(data);
    }}
    submitButton={handleSubmit => (
      <button className="button" onClick={() => handleSubmit()}>
        Submit
      </button>
    )}
  />,
  document.getElementById("root")
);
```

\***\*The Schema\*\***

The form schema should be structured like [this](https://github.com/simonsisay/react-hook-form-antdesign/blob/master/src/sampleFormSchema.js)

The following are all the available types of form-fields.
...\*

- text
- number
- email
- money
- percent
- select
- datepicker
- radio
  \*\*

You can pass

```javascript
[
 {
  type: "text",  // type of field
   name: "firstName", // name
   defaultValue: "Simon", // default value for the input.
   required: true,
   placeholder: "First name",
   label: "First name",
   fieldProps: { disabled: false },  // ant design props.
   validation: {  // validation object needs to be passed like this.
     required: true,
     errorMessage: "Please make sure your input is correct",
     validate: value => value.toString().startsWith("A")  // You can also pass a custom validation function.
   }
 },
 {
   type: "radio",
   name: "gender",
   options: ["Male", "Female"],  // this is an array of options for the radio.
   defaultValue: "Female",
   placeholder: "Gender",
   required: true,
   label: "Gender",
   validation: {
     required: true,
     errorMessage: "Please make sure your input is correct"
   },
   groupProps: { buttonStyle: "outline", size: "large" },
   // prop for the options container like
     <Radio.Group {...field.groupProps}><Radio /></Radio.Group>
    or
     <Select {...field.groupProps}><Option /></Select>

   fieldProps: {  // This one is for the individual options.
     disabled: false,
     style: { width: 150, textAlign: "center" }
   }
 }
]
```

\***_Styling_**

There are two props that we can pass to the component for styling

```javascript
<AlamaForm
  // the following props are best suited to do the form layout.
  innerClassName={"fields-container"} // wraps all inputs
  outerClassName={"form-container"} // wraps the whole form including the submit button passed as a render prop
/>
```

Other than that, we can pass a style object to each field inside the fieldProps object like

```javascript
    {
      type: "number",
      name: "age",
      fieldProps: {style: { width: 300, backgroundColor:"lightgrey", height:50, border:"none" } }
    }
```

**_Submitting form_**

The submitFormAsync prop takes a function that gets the user's inputs as an argument.

```javascript
<AlamaForm
  onSubmit={data => {
    // user's valid inputs. this function won't get fired unless all validations have passed.
    console.log(data);
  }}
/>
```

\***_Submit Button_**

Submit Button is passed as a renderProp through a prop named: submitButton
This will allow you to have a button of any type, with your own customized styling and layout.
Only exposing the click handler function for you.

```javascript
<FormGenerator
  submitButton={handleSubmit => (
    <MyButton onClick={() => handleSubmit()}>Submit Form</MyButton>
  )}
/>
```

| Props          | description                                                                      |
| -------------- | -------------------------------------------------------------------------------- |
| formSchema     | The json or array of objects of form structure                                   |
| outerClassName | a className for the the element that wraps the form fields and the submit button |
| innerClassName | a className for the fields container. Usually used to layout the form fields     |
| onSubmit       | submitHandler for the form. Gets the user's valid inputs as an argument          |
| submitButton   | takes the submit button component as a renderProp. Example is shown above.       |
