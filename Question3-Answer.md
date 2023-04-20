# Please fix, optimize, and/or modify the component as much as you think is necessary.

## 🚀Modified and Optimised Code

```code
import React, { useState, useEffect, useCallback, useMemo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const SingleListItem = ({ index, isSelected, onClickHandler, text }) => {
  const handleClick = useCallback(() => {
    onClickHandler(index);
  }, [index, onClickHandler]);

  const backgroundColor = useMemo(() => {
    return isSelected ? 'green' : 'red';
  }, [isSelected]);

  return (
    <li
      style={{ backgroundColor }}
      onClick={handleClick}
    >
      {text}
    </li>
  );
};

SingleListItem.propTypes = {
  index: PropTypes.number.isRequired,
  isSelected: PropTypes.bool.isRequired,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

// List Component
const List = ({ items }) => {
  const [selectedIndex, setSelectedIndex] = useState(null);

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = useCallback((index) => {
    setSelectedIndex(index);
  }, []);

  const renderedItems = useMemo(() => {
    return items.map((item, index) => (
      <SingleListItem
        key={index}
        onClickHandler={handleClick}
        text={item.text}
        index={index}
        isSelected={index === selectedIndex}
      />
    ));
  }, [handleClick, items, selectedIndex]);

  return (
    <ul style={{ textAlign: 'left' }}>
      {renderedItems}
    </ul>
  );
};

List.propTypes = {
  items: PropTypes.arrayOf(
    PropTypes.shape({
      text: PropTypes.string.isRequired,
    })
  ).isRequired,
};

export default List;
```

## 💫Changes I made:-

1. I used `useCallback` to memoize the `handleClick` function in the `List` component, which is passed as a prop to the `SingleListItem` component. This improves performance by ensuring that the same function instance is used across renders unless its dependencies change.

2. Used `useMemo` to memoize the `backgroundColor` value in the `SingleListItem` component, which is derived from the `isSelected` prop. This avoids recomputing the background color on every render unless `isSelected` changes hence improving the performance of the component.

3. Memoized the `renderedItems` variable in the `List` component using `useMemo`. This avoids recreating the array of `SingleListItem` components on every render unless `items`, `handleClick`, or `selectedIndex` values change.

4. I removed the unnecessary `WrappedSingleListItem` and `WrappedListComponent` components, since they were not adding any value to the code.

5. Simplified the `List` component's `useEffect` hook to reset the selected index to `null` whenever `items` changes, rather than creating a new `setSelectedIndex` function.

6. Changed the PropTypes definition for the `items` prop to match the correct format of

```code
PropTypes.arrayOf(PropTypes.shape(...))
```

Overall, the changes made improve performance by reducing unnecessary function calls and rendering, and simplify the code by removing unnecessary components and simplifying the `useEffect` hook.

### ⚡Output running of the modified code with no errors/warnings:-

![image](https://user-images.githubusercontent.com/73993775/233456109-45149df6-1f62-401e-918f-bd7b5541d485.png)

The background color changes to green on clicking any item:<br><br>
![image](https://user-images.githubusercontent.com/73993775/233456132-9c5ce0b6-9ba0-4dc3-8a3a-763241ee11e6.png)
