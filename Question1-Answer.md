# Explain what does the simple `List` component does in the provided code.

The `List` component in the code defines a React component that renders an unordered list of items passed in as props. It maps over the `items` array prop and renders a `SingleListItem` component for each item in the array.
<br><br>

The `SingleListItem` component is defined within this code snippet which is responsible for rendering an individual item in the list.

- It receives props such as `index`, `isSelected`, `onClickHandler` and `text`, from the parent `List` component.
- It renders the text of the item in a `li` element, and applies a green background color to the `li` element if the item is selected (isSelected is true), otherwise, it applies a red background color.
- It also calls the onClickHandler function when the li element is clicked, passing in the index of the item as an argument.
<br><br>

The `List` component also uses React hooks such as `useState` and `useEffect` to manage the state of the selected index of the list item.

- It initializes the state of `selectedIndex` using the `useState` hook and sets the initial value to `null`.
- The `useEffect` hook is used to reset the `selectedIndex` state to `null` whenever the `items` prop changes. This ensures that the selected index is cleared if the items in the list change.
- The `handleClick` function is defined to set the `selectedIndex` state to the index of the clicked list item. This function is passed down to each `SingleListItem` component as a prop named `onClickHandler`.
<br><br>

The `List` component and the `SingleListItem` component is memoized using the `memo` HOC (Higher Order Component) to optimize rendering performance by preventing unnecessary re-renders of the component when its props haven`t changed.
<br><br>

Finally, the code uses PropTypes to define the expected shape of the `items` prop and the props passed to the `SingleListItem` component. This helps catch errors early in the development process and provides documentation for other developers working with the code.
<br><br>

The code demonstrates good use of React hooks and HOCs to manage state and optimize rendering performance, and also shows the use of PropTypes to ensure type safety and documentation.
