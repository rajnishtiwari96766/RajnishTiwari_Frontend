Name:Rajnish Tiwari
Reg. No.:12015988
Pdf link:https://docs.google.com/document/d/1HF4Jjeyu45hFDBClHr_Sil70hmTu6IgABt0zlrZpq5c/edit#


Q1.Explain what the simple List component does.
Ans: The simple List component is a React functional component that displays a list of items passed in the form of an array via the items prop. The component has two child components, SingleListItem and ListComponent.The SingleListItem component is responsible for rendering an individual list item. It receives props such as index , isSelected determines , onClickHandler, and text . It renders an li element with the text content and a background color that depends on the isSelected prop.The ListComponent is responsible for rendering the list of items. It receives the items prop and maps through the array to render a SingleListItem for each item. It also defines the state variable selectedIndex using the useState hook, which keeps track of the index of the currently selected item. It also defines a handleClick function that updates the selectedIndex state variable when an item is clicked.Finally, the List component wraps the ListComponent in a memo HOC to improve performance by avoiding unnecessary re-renders when the items prop hasn't changed. The component also defines the propTypes and defaultProps for the items prop.

Q2.What problems / warnings are there with code?
Ans: a: In the WrappedListComponent, the useState hook is not used correctly. Instead of calling useState with the initial state value, the setSelectedIndex function is passed as the initial state value. To fix this, the useState hook should be called like this: const [selectedIndex, setSelectedIndex] = useState(null); .

b:In the SingleListItem component, the onClick handler is not defined correctly. It should be a function that is called when the item is clicked, not a function that is immediately called and returns another function. To fix this, change the onClick handler to: onClick={() => onClickHandler(index)}.

c:In the WrappedListComponent component, the propTypes definition for the items prop is incorrect. The correct syntax for defining the propTypes for an array of objects is:items: PropTypes.arrayOf(PropTypes.shape({ text: PropTypes.string.isRequired })) This ensures that each item in the items array is an object with a text property that is a required string.

d:In the WrappedListComponent component, the defaultProps definition for the items prop is incorrect. The defaultProps should be an object that sets the default value for the items prop, not null. To fix this, change the defaultProps to: WrappedListComponent.defaultProps = { items: [] }; This sets the default value for the items prop to an empty array.

e: Items in the WrappedListComponent cannot be null.It should be :
WrappedListComponent.defaultprops={items:[{text""Rajnish Tiwari"},{text:"12015988"},{text:B.Tech Cse"},{text:"Frontend Assignment"}],y};

Q3. Please fix, optimize , and/or modify the component as much as you think is necessary.
Ans:

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
      onClick={()=>onClickHandler(index)}
    >
      {text}
    </li>
  );
};

WrappedSingleListItem.propTypes = {
  index: PropTypes.number.isRequired,
  isSelected: PropTypes.bool.isRequired,
  onClickHandler: PropTypes.func.isRequired,
  text: PropTypes.string.isRequired,
};

const SingleListItem = memo(WrappedSingleListItem);

// List Component
const WrappedListComponent = ({
  items,
}) => {
  const [selectedIndex, setSelectedIndex] = useState(0);

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
          key={index}
          onClickHandler={() => handleClick(index)}
          text={item.text}
          index={index}
          isSelected={index===selectedIndex}
        />
      ))}
    </ul>
  )
};

WrappedListComponent.propTypes = {
  items: PropTypes.arrayOf(PropTypes.shape({
    text: PropTypes.string.isRequired,
  })),
};

WrappedListComponent.defaultProps = {
  items: [{text: "Rajnish Tiwari"}, {text: "12015988"}, {text: "B.Tech CSE"}, {text: "Frontend Assignment"}],
};

const List = memo(WrappedListComponent);

export default List; ```