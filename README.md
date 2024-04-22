## React Hook Form Notes

## Introduction

React Hook Form (RHF) is a performant, flexible, and extensible library for building forms in React applications. It leverages React Hooks to manage form state and provides a simple and intuitive API for working with forms.

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
