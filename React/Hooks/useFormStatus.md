# useFormStatus

## Reference

```jsx
const { pending, data, method, action } = useFormStatus();
```

- gives status information of the last form submission
- reference: `useFormStatus()`
  - parameters:
    - does not take any parameters
  - returns:
    - **status** object with properties
      - **pending** - boolean, gives info is parent form is pending submission
      - **data** - object implementing `FormData interface` that contains the data parent `<form>` is submiting
        - null value if not active submission
      - **method** - possible values are 'get' or 'post' (`GET` or `POST` HTTP method)
        - by default form will use `GET` method
      - **action** - reference to the function passed to the **action** propon the parent `<form>`
        - property is null if there is no parent `<form>`
        - if there is URI value provided to the **action** prop, or no action prop specified, **status.action** is null

### Caveats

- must be called from the component that is rendered inside a `<form>`
- hook will only return status information for a parent `<form>`
  - will not return status information for any `<form>` rendered in that same component or children components

## Usage

### Display a pending state during form submission

**pitfall** - hook will not return status information for a `<form>` rendered in the same component

### Read the form data bein submitted
