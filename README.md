# Ketan-Jain_Front-End

## Q1) Explain what the simple List component does.

Answer->
Lists can be created in a similar way as we create lists in JavaScript.The list component contains list items.<br>
List is used to store multiple items of the same and different datatype under a variable like array.<br>
Here single list item is stored inside WrappedSingleListItem.<br>
React.memo(WrappedListComponent) returns a new memoized component List.<br>
List render is memoized but the outputs of List is same content as the original WrappedListComponent component.items array is used to store these list items and then each item is looped through using map() function and displayed. The background color of text changes according to the isSelected state, which is dependent on selectedIndex.<br>
const [selectedIndex, setSelectedIndex] = useState(true); //Green color<br>
const [selectedIndex, setSelectedIndex] = useState(); //Red color<br>

## Q2) What problems / warnings are there with code ?

Using useState() the 'set' variable should be after the local variable

Answer->

Using useState() the 'set' variable should be after the local variable

setSelectedIndex used after selectedIndex.<br>
Insted of shapeOf we use arrayof<br>
WrappedListComponent.propTypes = {<br>
items: PropTypes.arrayOf(PropTypes.shape({<br>
text: PropTypes.string.isRequired,<br>
})),<br>
};<br>
Null Properties Issue:
Solution- This error states that the items array cannot be empty or Null.<br>
So Final code with solution is below:<br>
WrappedListComponent.defaultProps = {<br>
items: [{ text: "First Item" }, { text: "Second Item" }]<br>
};<br>

## Q3) Please fix, optimize, and/or modify the component as much as you think is necessary.

Answer->

Final Code with all the issues fixed and modified is below<br>
import PropTypes from "prop-types";<br>
import React, { useState, useEffect, memo } from "react";<br>

// single List Item

const WrappedSingleListItem = ({<br>
index,<br>
isSelected,<br>
onClickHandler,<br>
text<br>
}) => {<br>
return (<br>
  onClickHandler(Boolean(index))} > {text}<br>
);<br>
};<br>
WrappedSingleListItem.propTypes = {<br>
index: PropTypes.number,<br>
isSelected: PropTypes.bool,<br>
onClickHandler: PropTypes.func.isRequired,<br>
text: PropTypes.string.isRequired<br>
};<br>
const SingleListItem = memo(WrappedSingleListItem);<br>
// List Component<br>
const WrappedListComponent = ({ items }) => {<br>
const [selectedIndex, setSelectedIndex] = useState();<br>
useEffect(() => {<br>
setSelectedIndex(true);<br>
}, [items]);<br>
const handleClick = (index) => {<br>
setSelectedIndex(Boolean(index));<br>
console.log("This is index: " + index);<br>
};<br>
return (  <br>
    {items.map((item, index) => ( handleClick(index)} text={item.text} index={index} isSelected={selectedIndex} key={index} /> ))}<br>
    );<br>
    };<br>
    WrappedListComponent.propTypes = {<br>
    items: PropTypes.arrayOf( PropTypes.shape({<br>
    text: PropTypes.string.isRequired<br>
    })<br>
    )<br>
    };<br>
    WrappedListComponent.defaultProps = {<br>
    items: [{ text: "First Item" }, { text: "Second Item" }]<br>
    };<br>
    const List = memo(WrappedListComponent);<br>
export default List;<br>
