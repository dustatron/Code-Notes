# Redux Notes

## Install

[Documentation](https://redux.js.org/)

[Get Redux Dev Tools: ]( https://chrome.google.com/webstore/detail/redux-devtools/lmhkpmbekcpmknklioeibfkpmmfibljd?hl=en )- add configuration in index.js of your project when you create your store:

```shell
npm install redux@4.0.5 react-redux@7.1.3
```

1. Set-up index

   ```javascript
   import { createStore } from 'redux';
   import reducer from './reducers/ticket-list-reducer';
   import { Provider } from 'react-redux';
   
   const store = createStore(reducer); 
   
   const store = createStore(
     reducer, 
     window.__REDUX_DEVTOOLS_EXTENSION__ && window.__REDUX_DEVTOOLS_EXTENSION__()
   );
   
   ```

2. other commands

   ```javascipt
   createStore()
   getState()
   dispatch()
   ```

## Wire up Firebase

---

```javascript
useFirestoreConnect([ { collection: 'surveys' }, { collection: 'submissions' } ]);


firestoreConnect(() => [
{
collection: 'states',
doc: 'CA',
subcollections: [
{ collection: 'cities', doc: 'SF' },
{ collection: 'zips' }
]
}
])
```



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

