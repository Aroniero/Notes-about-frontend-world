#  React testing Library - Instalation

```
npm install --save @testing-library/react @testing-library/jest-dom			CRA DOCS
npm install --save-dev @testing-library/react
```

Similar to `enzyme` you can create a `src/setupTests.js` file to avoid boilerplate in your test files:

```react
// react-testing-library renders your components to document.body,
// this adds jest-dom's custom assertions
import '@testing-library/jest-dom/extend-expect';
```

We can use 2 methods for testing (`it` and `test`). They are doing the same stuff:

```
it("test function", () => {

});

test("test function", () => {

});
```

