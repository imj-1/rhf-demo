## React Hook Form Notes

## Introduction

React Hook Form (RHF) is a performant, flexible, and extensible library for building forms in React applications. It leverages React Hooks to manage form state and provides a simple and intuitive API for working with forms.

[Official React Hook Form Docs](https://react-hook-form.com/docs)

## Key Concepts

### 1. useForm Hook

- `useForm` is the main hook provided by RHF for managing form state.
- It returns methods and state variables for managing form submission, validation, and error handling.

### 2. Registering Inputs

- Inputs are registered with the `register` function provided by `useForm`.
- Syntax: `register({ name: 'fieldName', ...validationRules })`
- Example: `register({ name: 'username', required: true })`

### 3. Handling Form Submission

- Form submission is handled using the `handleSubmit` function returned by `useForm`.
- Syntax: `handleSubmit(onSubmit)`
- `onSubmit` is a callback function invoked when the form is submitted.

### 4. Validating Inputs

- Inputs can be validated using built-in or custom validation rules.
- Built-in validation rules include `required`, `min`, `max`, `pattern`, etc.
- Custom validation rules can be defined using the `validate` option in `register`.

### 5. Error Handling

- Errors are tracked and displayed using the `errors` object returned by `useForm`.
- Errors can be displayed next to input fields or in a summary at th

### 6. Improved performance with controlled components

- Components do not re-render when you type into form fields unlike traditional react forms where every keystroke would cause the component an dits children to re-render

### Notes:

- noValidate attribute prevents browser validation to allow rhf to handle validation of the fields
- to add custom validation we add a key value pair to the options object passed into the register function as shown below:

```
{...register("email", {
        pattern: {
            value:
                /^[a-zA-Z0-9.!#$%&'*+/=?^_`{|}~-]+@[a-zA-Z0-9-]+(?:\.[a-zA-Z0-9-]+)*$/,
            message: "Invalid email format",
        },
        validate: {
            notAdmin: (fieldValue) => {
                return (
                    fieldValue !== "admin@example.com" ||
                    "Enter a different email address"
                );
            },
            notBlackListed: (fieldValue) => {
                return (
                    !fieldValue.endsWith("addomain.com") ||
                    "This domain is not supported"
                );
            },
        },
})}
```

- for object or array input data, it's recommended to use the validate function for validation as the other rules mostly apply to string, string[], number and boolean data types.
- for register fn use dot notation syntax only for typescript usage consistency, so bracket [] will not work for array form value.

```
Example:
    register('test.0.firstName'); // ✅
    register('test[0]firstName'); // ❌
```

- in order to render numbers as type number add the following to the options object in register function `valueAsNumber: true`

```
<div className="form-control">
    <label htmlFor="age">Age</label>
    <input
        type="number"
        id="age"
        {...register("age", {
        valueAsNumber: true,
        required: {
            value: true,
            message: "Age is required",
        },
        })}
    />
    <p className="error">{errors.age?.message}</p>
</div>
```

- getValues method is a more performant way of watching form values. Unlike watch,
  getValues will not trigger rerenders or subscribe to input changes making it a better option when a user clicks on a button or performs a specific action.
