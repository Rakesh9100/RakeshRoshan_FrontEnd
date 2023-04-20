# What problems / warnings are there with code?

## ⚡Compilation Warnings received on the npm cmd terminal:-

```warnings
Compiled with warnings.

[eslint]
src\List.js
  Line 39:6:  React Hook useEffect has a missing dependency: 'setSelectedIndex'. Either include it or remove the dependency array  react-hooks/exhaustive-deps

Search for the keywords to learn more about each warning.
To ignore, add // eslint-disable-next-line to the line before.

WARNING in [eslint]
src\List.js
  Line 39:6:  React Hook useEffect has a missing dependency: 'setSelectedIndex'. Either include it or remove the dependency array  react-hooks/exhaustive-deps

webpack compiled with 1 warning
```

## 💥Errors received on the localhost:3000:-

```errors
Compiled with problems:

ERROR
prop_types__WEBPACK_IMPORTED_MODULE_2___default(...).shapeOf is not a function
TypeError: prop_types__WEBPACK_IMPORTED_MODULE_2___default(...).shapeOf is not a function
    at ./src/List.js (http://localhost:3000/static/js/bundle.js:178:116)
    at options.factory (http://localhost:3000/static/js/bundle.js:42388:31)
    at __webpack_require__ (http://localhost:3000/static/js/bundle.js:41812:33)
    at fn (http://localhost:3000/static/js/bundle.js:42045:21)
    at ./src/App.js (http://localhost:3000/static/js/bundle.js:17:63)
    at options.factory (http://localhost:3000/static/js/bundle.js:42388:31)
    at __webpack_require__ (http://localhost:3000/static/js/bundle.js:41812:33)
    at fn (http://localhost:3000/static/js/bundle.js:42045:21)
    at ./src/index.js (http://localhost:3000/static/js/bundle.js:239:62)
    at options.factory (http://localhost:3000/static/js/bundle.js:42388:31)
```
<br>

1. In the `WrappedListComponent`, the `setSelectedIndex` should be declared as a function that will set the selected index. Currently, it is being used as a variable, which will not update the state properly.
2. The PropTypes definition for the `items` prop in `WrappedListComponent` is not correct. The correct syntax for defining an array of objects is

```code
PropTypes.arrayOf(PropTypes.shape({...}))
```

3. The `isSelected` prop in the `SingleListItem` component is expected to be a boolean, but it is being passed the selectedIndex state value which is a number. This could lead to unexpected behavior and should be updated to check whether the index prop is equal to the selectedIndex state value, like this:

```code
isSelected={index === selectedIndex}
```

4. In the WrappedListComponent, the setSelectedIndex variable name should be changed to selectedIndex to match the useState hook call.
5. The `onClickHandler` prop for the `WrappedSingleListItem` component is being called immediately with the `index` argument instead of passing a function that will be called when the item is clicked. This will result in the function being called every time the component is rendered, which is not the intended behavior. Instead, it should be passed as a function that takes the index as an argument and is only called when the item is clicked. This should be updated to pass a reference to the function, like this:

```code
onClick={() => onClickHandler(index)}
```

6. The `items` prop in `WrappedListComponent` is set to a default value of `null`, but this could lead to unexpected behavior if the component is used without providing the `items` prop. It would be better to set a default value of an empty array instead.
7. The `memo` HOC is used for both `SingleListItem` and `WrappedListComponent`, but it may not be necessary as these components are already relatively simple and not likely to cause unnecessary re-renders.
