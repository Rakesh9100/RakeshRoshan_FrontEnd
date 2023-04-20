<h1 align="center">SteelEye Frontend Engineer Assignment</h1>

## React Component Code Review

### Based on the code below answer the following queries:

1. Explain what the simple List component does.<br>
[Question1-Answer](https://github.com/Rakesh9100/RakeshRoshan_FrontEnd/blob/main/Question1-Answer.md)<br><br>
2. What problems / warnings are there with code?<br>
[Question2-Answer](https://github.com/Rakesh9100/RakeshRoshan_FrontEnd/blob/main/Question2-Answer.md)<br><br>
3. Please fix, optimize, and/or modify the component as much as you think is necessary.<br>
[Question3-Answer](https://github.com/Rakesh9100/RakeshRoshan_FrontEnd/blob/main/Question3-Answer.md)<br><br>

### Code

```code
import React, { useState, useEffect, memo } from 'react';
import PropTypes from 'prop-types';

// Single List Item
const WrappedSingleListItem = ({
  index,
  isSelected,
  onClickHandler,
  text,
}) => {
  return (
    <li
      style={{ backgroundColor: isSelected ? 'green' : 'red'}}
      onClick={onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number,
  isSelected: PropTypes.bool,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [setSelectedIndex, selectedIndex] = useState();

  useEffect(() => {
    setSelectedIndex(null);
  }, [items]);

  const handleClick = index => {
    setSelectedIndex(index);
  };

  return (
    <ul style={{ textAlign: 'left' }}>
      {items.map((item, index) => (
        <SingleListItem
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={selectedIndex}
        />
      ))}
    </ul>
  )
};

WrappedListComponent.propTypes = {
  items: PropTypes.array(PropTypes.shapeOf({
    text: PropTypes.string.isRequired,
  })),
};

WrappedListComponent.defaultProps = {
  items: null,
};

const List = memo(WrappedListComponent);

export default List;
```
