# Redux Notes

## Dev Readout

```javascript
const store = createStore(
  reducer, 
  window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
);

```

###  Update prop in state 

```javascript

Const newStateUpdate = Object.assign({}, state, {
       [id]: Object.assign({}, state[id], {issue: issue
    }
  )
```

-----

### Object.assign

```javascript
// Update state using Object.assign() 
const newStateUpdate = { ...state, [id]: { ...state[id], tags: { ...state[id].tags, [tagId]: { module: module, topic: topic} } }}
```

### Code Snippets Using Object.assign() and the Spread Operator

```javascript

export default (state = {}, action) => {
  const { names, location, issue, id } = action;
  switch (action.type) {
  case 'ADD_TICKET':
    // Update state using Object.assign()
    return Object.assign({}, state, {
      [id]: {
        names: names,
        location: location,
        issue: issue,
        id: id
      }
    });
    // Update state using the spread operator
    return {...state, 
        [id]: {
          names: names,
          location: location,
          issue: issue,
          id: id
      }
    };
    case 'UPDATE_TICKET_ISSUE':
      // Update state using Object.assign()
      const newStateUpdate = { ...state, [id]: { ...state[id], issue: issue } };
      // Update state using the spread operator
      const newStateUpdate = Object.assign({}, state, {
        [id]: Object.assign({}, state[id], {
          issue: issue
        })
      });
  }
```

